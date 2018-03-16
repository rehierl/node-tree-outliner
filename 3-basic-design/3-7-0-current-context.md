
<!-- ======================================================================= -->
# Design - current context

the current section (represents the current path of sections),
represents the algorithm's relevant current knowledge -

**TODO**
define an algorithm's current context -
should also include its current node -

goal -
provide a general overview of what it can and can not do

In essence, an algorithm is executed on the tree's node sequence. That is, it
enters one node after another and, at some point, enters the next subsequent
sectioning node. At that point, the algorithm's current context contains the
current rooted path of nodes (begins in the node tree's root and ends in the
current sectioning node being entered) and the current path of sections
(begins in the root section and ends in the current section).

Note that the current path of nodes holds all parent containers of all sections
in the current path of sections. That is, because otherwise those sections would
no longer be open. In contrary to that, the current path of nodes does not
necessarily hold all the corresponding sectioning nodes. That is, because all
presequent type-2 sectioning nodes will have been exited by then.

Note that all nodes in the current rooted path of nodes have been entered,
but not yet exited. ...
