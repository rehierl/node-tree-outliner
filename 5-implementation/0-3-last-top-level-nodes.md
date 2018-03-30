
<!-- ======================================================================= -->
# Implementation - last top-level nodes

**TODO**
(related to the support of transformations)

<!-- ======================================================================= -->

add a similar note to "reduced sequences" -
add a `lastTopLevelNode` property definition -
see the extensions chapter -

could also define a `Node Section.closeReason` property -
and then compare it with a `Section.parentContainer` property -
advantage is that this would support empty sections -
better use `null` references instead of `parentContainer`

or define a `Node Section.endMarkerNode` property -

<!-- ======================================================================= -->
## top-level nodes

associating a node (strict association) with a section is equivalent to
associating a whole subtree of nodes (implicit associations). -

two levels of implicitness -
implicitly with the explicitly associated section (associate a subtree),
and implicitly with the implicitly associated section (one section only)

can an algorithm easily store references to all top-level nodes? -
issue: associate with one section only (not that easy) -
issue: subsequent t2 with equal or higher rank (tricky) -

when a section is being closed, or as an on demand feature? -
is it possible to avoid having to determine them as a post-process
by providing a list of top-level nodes? -
e.g. `Node[] Section.getTopLevelNodes()` -

the first top-level node is easy to determine (entering) -
the last top-level node could be determined when closing a section -
after all, each section does have its own close event -
last child if closed by a parent container -
previous sibling when closed by a t2 sectioning node -

t2 -> t1 transformations must take into account, that
they could be the cause for new first and/or last top-level nodes -
the corresponding node references, if any, need to be updated
