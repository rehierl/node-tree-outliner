
<!-- ======================================================================= -->
# Implementation - parent containers

The focus of the following content is on the implementation of parent
containers: How to close inner sections when exiting such a node?

```
n0
=========
n1 n2 ...
```

* `n0` is an inactive node (associated with `s0`)
* for `(i >= 1)`: `ni` is a type-2 sectioning node (declares `si`)

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
Because of that, an implementation must essentially restore the sequence of
sections when exiting a parent container.

As mentioned before, any parent node may in principle act as the parent
container of one or more sections. The only exception to that rule are the
type-1 sectioning nodes: These are always parent containers. Because of that,
and when exiting any parent node, an implementation must test whether inner
sections need to be closed.

1. Inner sections may have parent containers that are distant descendants to
   `n0`. The inner sections of these parent containers will be closed before
   the exit event of `n0` is reached (i.e. the same issue, but with regards
   to descendant parent containers). That is, this case is considered to be
   dealt with by the time `n0` is being exited.
2. `n0` is the parent container of inner sections, but some end-marker node
   applied. Obviously, these sections will be closed before the exit event
   of `n0` is reached.
3. `n0` is the parent container of inner sections, and no close modifier
   applied. The exit event of `n0` must close these remaining open sections.

In short, the exit event of a given parent container must only close those
sections that remain to be open by the time the parent container is being
exited. All other closed inner sections can and will be ignored (i.e those
are no longer relevant).

Because they are still open, all relevant sections are part of the current path
of sections. Furthermore, and because all those sections are subsections to the
section, with which the parent container is associated, the relevant sections
all are located at the very end of the current section sequence. Consequently,
an implementation must only pop and close the top-most sections from the section
stack until the current section matches the parent container's parent section:

```
onExitParentContainer(Node container) begin
  //- currentSection is a global reference
  while(currentSection !== container.parentSection) begin
    parentSection = currentSection.parentSection
    currentSection.close()
    currentSection = parentSection
  end
end
```

Note that ...

* all nodes are associated while they are being entered. Because of that,
  a parent container's `Node.parentSection` property is always set to a
  non-null section reference when the parent container is being exited.
* the root node must be associated with the universal section. This edge case
  must be taken into account when an implementation exits the root node.
* the remaining open inner sections will be closed in reverse order. That
  is, subsections will be closed before their ancestor sections are closed.
* an implementation does not have to know how many sections need to be closed.
* the close operation of an implementation could have implicit side effects
  (e.g. due to releasing locked resources).

With regards to efficiency, it does not appear to be possible to gain anything
from setting a boolean `Node.isParentContainer` property. Therefore, and apart
from gaining some amount of additional clarity, an implementation does not have
to test beforehand (e.g. by the use of an `if-then` construct), whether the node
in question is indeed a parent container. That is, one test must always be
executed either way (i.e. even if the corresponding parent node is actually not
even a parent container).
