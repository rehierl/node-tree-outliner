
<!-- ======================================================================= -->
# Design - current context

the current section (represents the current path of sections),
represents the algorithm's relevant current knowledge -

define an algorithm's current context -
should also include its current node -

goal -
provide a general overview of what an algorithm,
in the context of this design, can and can not do

In essence, an algorithm is executed on the tree's node sequence. That is, it
enters one node after another and, at some point, enters the next subsequent
sectioning node. At that point, the algorithm's current context contains the
current rooted path of nodes (begins in the node tree's root and ends in the
current sectioning node being entered) and the current path of sections
(begins in the root section and ends in the current section).

Note that the current path of nodes holds all parent containers of all sections
in the current path of sections. That is, because otherwise those sections
would no longer be open. In contrary to that, the current path of nodes does
not necessarily hold all the corresponding sectioning nodes. That is, because
all presequent type-2 sectioning nodes will have been exited by then.

Note that all nodes in the current rooted path of nodes have been entered,
but not yet exited. ...

**TODO**
we have atomic events -
i.e. events are executed isolated from one another -
i.e. an event is executed completely, before the next one is started -
we need atomic/fundamental operations -
i.e. non-interruptable operations -

<!-- ======================================================================= -->
##

need a current path of nodes - 
essentially due to the current node's required node level -
the ancestors themselves aren't exactly required -

When a sectioning node is being entered, an algorithm has in principle knowledge
of all those nodes that it has already visited. Because of that, it knows about
all those sections that are presequent to the current sectioning node (i.e. the
closed and the open presequent sections). In contrary to that, an algorithm is
unaware of any subsequent node. Those might, or might not exist (i.e. there is
no guarantee that there are further subsequent nodes or sections).

As closed presequent sections were closed even before the current subsequent
sectioning node was be entered, the declared subsequent section is by default
independent to these presequent sections. Hence, and with regards to closed
sections, all that modifiers could do would be to define the subsequent section
to be a subsection to them. But, as the `subsection-of` relationship is formally
based upon multiple associations per node (i.e. a node must be associated with
both sections), any attempt to define a subsequent section to be a subsection to
closed presequent sections would represent an attempt to alter closed sections
and consequently be in conflict with the definition of a section's closed state.

Note that any other available option, besides closing presequent sections,
is not relevant for the current considerations (e.g. section properties that
are not relevant to the section hierarchy, e.g. a section's title).

<!-- ======================================================================= -->
##

Note that open sections can not be closed arbitrarily. That is, because any
ancestor section must remain open for as long as any of its subsections are
open. Open sections must therefore be closed in an orderly, bottom-up fashion.
