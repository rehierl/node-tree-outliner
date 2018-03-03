
<!-- ======================================================================= -->
# How to implement ...

The following content is intended to clarify implementation specific aspects.

<!-- ======================================================================= -->
## implicit associations

(related to the implementation of close modifiers)

The focus of this part is on the implementation of:
Section `s1`, which is declared by a sectioning node `n1`, is a subsection to
`s0` (i.e. regardless of any non-default definition), if `n1` is a descendant
of a node that is associated with `s0`.

In short: How to avoid conflicts due to implicit associations?

```
      n0
================
n1 n2         n5
   --------
      n3 n4
```

* `n0` represents a type-1 sectioning node
* `n1, n3-5` represent type-2 sectioning nodes
* `n2` represents an inactive parent container

Note that `s3` is, first and foremost due to its structural relationship, a
subsection to `s1`. That is the case even if an extension to the definition of
`n3` would define its declared section to be the next sibling section of `s1`.
That is, under these circumstances, the non-default definitions would have to
be ignored. Which is, because structural relationships can not be undefined.
Because of that, implicit associations have precedence over any non-default
definition, if both sections have different parent containers (e.g. `n0` vs.
`n2`).

Note that the universal section has no existing parent container (i.e. virtual).

two type-1 sections can't have the same parent container -
the subsequent type-1 section is a subsection

what about type-2 sections ...

<!-- ======================================================================= -->
## top-level nodes

(related to the support of transformations)

associating a node (strict association) with a section is equivalent to
associating a whole subtree of nodes (implicit associations). -

two levels of implicitness -
implicitly with the explicitly associated section (associate a subtree), and
implicitly with the implicitly associated section (one section only)

can an algorithm easily store references to all top-level nodes? -
issue: associate with one section only (not that easy) -
issue: subsequent t2 with equal or higher rank (tricky) -
i.e. two levels of implicitness -

when a section is being closed, or as an on demand feature? -
is it possible to avoid having to determine them as a post-process
by providing a list of top-level nodes? -
e.g. `Node[] Section.getTopLevelNodes()` -

the first top-level node is easy to determine (entering) -
the last top-level node could be determined when closing a section -
after all, each section does have its own close event -
last child if closed by a parent container -
previous sibling when closed by a t2 sectioning node -

<!-- ======================================================================= -->
## parent containers

(related to the implementation of sectioning nodes)

The focus of this part is on the implementation of:
Close one or more inner sections when exiting a parent container.

```
n0
=========
n1 n2 ...
```

* `n0` represents an inactive parent container
* `n0` is associated with section `s0`
* `n1,n2` represent type-2 sectioning nodes
* `n1,n2` declare sections `s1,s2`

By definition, the trace of section sequences is:

```
trace of sequences:     -  node event:
======================  -  ====================
(s0)                    -  just before entering n0
(s0,s1)                 -  just after exiting n1
(s0,s1,s2)              -  just after exiting n2
...                     -  ...
(s0,s1,s2)              -  just before exiting n0
(s0,s1)                 -  while exiting n0
(s0)                    -  just after exiting n0
```

Note that the sequence of sections just before entering the parent container
is identical to the sequence of sections just after exiting said container.
Because of that, an implementation must restore the sequence of sections
when exiting a parent container.

As mentioned before, any parent node can in principle act as the parent
container of one or more sections. The only exception to that rule are the
type-1 sectioning nodes: These are always parent containers. Because of that,
and when exiting any parent node, an implementation must always test whether
inner sections need to be closed.

1. Inner sections may have parent containers that are descendants to `n0`.
   These sections will be closed before the exit event of `n0` is reached
   (i.e. same issue, but with regards to an inner parent container).
2. `n0` is the parent container of inner sections, but some non-default
   rule applies. These sections will be closed before the exit event of
   `n0` is entered.
3. `n0` is the parent container of inner sections, and no non-default rule
   applies. The exit event of `n0` must close these remaining open sections.

In short, the exit event of a given parent container must only close those
sections that remain to be open by the time the parent container is being
exited. All other closed independent inner sections can and will be ignored
(i.e those are no longer relevant).

Because of that, all relevant sections are part of the current section sequence.
Furthermore, and because all those sections are subsections to the section, with
which the parent container is associated, the relevant sections are located at
the very end of the current section sequence. Consequently, an implementation
must only close and pop the top-most sections from the section stack until the
current section matches the parent container's parent section:

```
onExitParentContainer(Node container) begin
  //- currentSection is a global reference
  while(currentSection !== container.parentSection) begin
    parentSection = currentSection.parentSection
    currentSection.close()
    currentSection = parentSection
  end
onExitParentContainer end
```

Note that ...

* any node is associated while it is being entered. Because of that, the
  parent container's parent section reference is always set when a parent
  container is being exited. Note that the root node must be associated
  with the universal section.
* the remaining open inner sections will be closed in reverse order. That
  is, subsections will be closed before their ancestor sections are closed.
* an implementation does not have to know how many sections need to be closed.
* the close operation of an implementation could have unexpected side effects
  (e.g. due to releasing locked resources).

With regards to efficiency, it does not appear to be possible to gain anything
from maintaining a boolean `isParentContainer` flag variable. Therefore, and
apart from gaining some amount of additional clarity, an implementation does
not have to test beforehand (e.g. by the use of an `if-then` construct),
whether the node in question is indeed a parent container. That is, one test
must always be executed either way (i.e. even if the corresponding node is
actually not a parent container).
