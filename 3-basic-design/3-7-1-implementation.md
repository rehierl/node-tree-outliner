
<!-- ======================================================================= -->
# Design (8) - how to implement ...

The following content is intended to clarify implementation specific aspects.

<!-- ======================================================================= -->
## parent containers

The focus of this part is on the implementation of:
Close one or more sections when exiting a parent container.

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
   (i.e. same routine, but with regards to another parent container).
2. `n0` is the parent container of inner sections, but some non-default
   rule applies. These sections will be closed before the exit event of
   `n0` is entered.
3. `n0` is the parent container of inner sections, and no non-default rule
   applies. The exit event of `n0` must close these remaining open sections.

In short, the exit event of a given parent container must only close those
sections that remain to be open by the time the parent container is being
exited. All other independent inner sections can and will be ignored.

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
  parent container's parent section reference is always and already set
  (Note that the root node must be associated with the universal section).
* the remaining open inner sections will be closed in reverse order. That is,
  subsections will be closed before their ancestor sections are closed.
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

<!-- ======================================================================= -->
## implicit associations

The focus of this part is on the implementation of:
Always treat a section as a subsection of some presequent section
(regardless of any other definition), if its sectioning node is a
descendant of an associated parent node.

Put differently: How not to be in conflict with implicit associations?

Therefore, the most important question that needs to be answered is:
How is it possible to efficiently detect whether implicit associations
have precedence over any other definition?

```
      n0
================
n1 n2         n5
   --------
      n3 n4
```

Note that the node level of a node is defined as "1 + the number of edges in
between the node and the tree's root". That is, the root node has a node level
of 1, its child nodes a node level of 2, and their children a node level of 3.
In short: The higher the node level, the deeper within the node tree's hierarchy
a node is located.

Note that the universal section has no existing (i.e. virtual) parent container.

the node level of a sectioning node acts as a rank-like value -
which must have precedence over any user-defined rank value -

the node level of the top-level content nodes can be derived
from the definition of the corresponding sectioning node -
+1 in case of type-1, +0 in case of type-2

plot twist: its the parent container, not the node level -
even better for implementations

two type-1 sections can't have the same parent container -
the subsequent type-1 section is a subsection

what about type-2 sections ...

<!-- ======================================================================= -->
## top-level nodes

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