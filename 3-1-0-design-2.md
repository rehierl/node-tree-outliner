
<!-- ======================================================================= -->
# Design (2) - States of a section

Similar to output streams, any section has the following states:

<!-- ======================================================================= -->
## initialized state

As soon as a sectioning node is known, it is technically possible to associate
any subsequent node, including the current sectioning node, with it. Because
of that, and if a section had no delayed start, a sectioning node would have
to be associated with its own section.

Consequently, a section's "initialized" state means that: (1) the section is
created/initialized and (2) an algorithm will, at some later point in time,
begin associating nodes with it.

(-> initialized)
A section's "initialized" state is a section's first/initial state,
which needs to be set once a section object is created.

<!-- ======================================================================= -->
## open state

Once a section's first node is entered, this first node and any subsequent node
must be associated with it. An algorithm therefore needs additional rules that
enable it to determine when to begin with the association of nodes.

A section is considered to be "open" as soon as the next subsequent node
must be associated with it.

(initialized -> open)
A section can only change to its state to "open",
if its current state is "initialized".

<!-- ======================================================================= -->
## closed state

Any section must eventually end at some point. By default, that point is
reached when the root node of the process is being exited. That is, because
the root node has no node that is subsequent to it.

This default case is obviously insufficient, because the very last node of
a node sequence would then always have to be associated with all the known
sections. An algorithm therefore needs additional rules that enable it to
determine, when it is no longer allowed to associate any other subsequent
nodes with a section.

A section is considered to be "closed" as soon as it is no longer allowed
to associate any further nodes with it.

(open -> closed)
A section can only change to its state to "closed",
if its current state is "open".

<!-- ======================================================================= -->
## set of open sections

As mentioned earlier, an algorithm needs rules that enable it to determine
when it is no longer allowed to associate any more nodes with a section.
Once such a rule applies, an algorithm must mark the corresponding section,
or multiples thereof, as being "closed".

At any given point in time, any section within the set of known sections is
either "initialized", "open" or "closed". Because of that, the set of known
sections `S` can be broken up into three disjunct sets of sections (with each
subset containing only those sections that have the corresponding state):

* the set of initialized sections `IS`
* the set of open sections `OS`
* the set of closed sections `CS`.

With regards to associations, a section's "initialized" and "closed" states
appear to be semantically equivalent. That is, because no associations are
allowed unless a section's state is "open".

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The event used to create a new section object (e.g. the enter event of its
sectioning node) is said to represent a section's "create" event. Likewise,
the event used to open a section is referred to as a section's "open" event,
and the event that is used to close a section as the section's "close" event.

Unless defined otherwise, no other operation, with regards to the section in
question, is allowed to be executed. That is, an algorithm is not allowed to
associate any node with the corresponding section (i.e. add nodes to it) during
the execution of the above mentioned events. These events are only allowed to
change a section's state.

**CLARIFICATION**
A closed section can only be understood to represent an empty section, if
it was opened and closed without associating any nodes with it.

The contents of a section, that still counts as being "initialized", must be
understood to be "undefined". That is, because the section's "open" event was
not yet triggered. Because of that, no statements can be made with regards to
the contents of such a section. Consequently, a section that was never opened
can also not be seen to be "empty". After all, an "initialized" section can
still be opened, and nodes can still be associated with it. Any attempt to
close an "initialized" section must be understood to represent an error.

**CLARIFICATION**
It is not allowed to re-initialize, or re-open a closed section.

A section's "close" event, and the corresponding rules, can therefore also
be seen to represent a guarantee that a section will not change any further.

This guarantee is critical to an efficient TOC generator, because it allows to
drop a section object once the corresponding section is closed and once the the
information it holds has been extracted. After that, any attempt to execute any
kind of operation on a dropped section object will result in an access violation
error.

Re-opening a section for additional associations would be in conflict with the
above guarantee. Because of that, such an operation must be understood as an
attempt to suspend and then resume a section.

**CLARIFICATION**
Once closed, a section is fully defined/specified. That is, because no
subsequent node will, by definition, have any further effect on it.

**CLARIFICATION**
A section can not be strictly suspended.

Note that it is assumed, that a "resume" operation must always follow a
"suspend" operation ("suspend" would otherwise be equivalent to "close").

Technically, it would be possible to define rules that tell an algorithm to
suspend and then, at some later point in time, resume associating nodes with a
section. However, this does not mean that it would be reasonable to allow such
an operation.

Assumed that section `s` would have to be suspended after some node `ns` was
associated with it, and that section `s` would have to be resumed beginning
with some node `nr`. This would in return mean that, in between both nodes,
there need to be any number of nodes that are supposed to be completely
unrelated to this section (hence, strictly suspended).

Note that these considerations do not take the definition of nodes into account,
that would allow to clearly define when a section has to be suspended and when
it has to be resumed.

A section would, if suspend-and-resume operations were allowed, consist of
multiple subsequent parts that are separate from each other. Due to the gaps
in between the separate parts of a section, an algorithm would have no means
to treat a section as as one entity by grouping all of the section's nodes,
which would obviously be in conflict with the initial requirements.

In addition to that, the intermediate nodes in between the separate parts of
a strictly suspended section can still be seen to be in relationship with it.
That is, because the very reason, as to why these intermediate nodes would
have to be excluded, puts these intermediate nodes into a relationship with
said section. After all, there would have to be a reason as to why they are
surrounded by the separate parts of a section. Because of that, the ultimate
goal of such an attempt (i.e. completely unrelated nodes) can't even be reached
without producing a conflict.

Finally, the subsequent parts of a strictly suspended section can also be seen
to represent sections of their own. Hence, the nodes that would be required in
order to tell an algorithm that it has to resume a section can themselves be
seen to represent additional sectioning nodes. The separate parts can then be
understood to represent separate sections.

**CLARIFICATION**
A section has no gaps.

Because of that, any node belongs to a section, if it is subsequent to the
section's first and presequent to the section's last node.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
All nodes must be associated while they are being entered.

Because exit events will be executed in reverse order, associating any nodes
while they are being exited would constitute a deviation of the tree traversal's
order of nodes, and as such, a deviation of the tree's semantics. Consequently,
associating any nodes with sections while they are being exited can in principle
not result in sections that accurately represent the contents of a tree.

Apart from that, the location of a node (in terms of a tree's sections) could
also be affected by nodes that are subsequent to it. Because of that, a node
could end up having an effect on nodes that are presequent to it.

**CLARIFICATION**
A section is a sequence of subsequent nodes.

That is, because any node must be associated with a section while it is being
entered. Consequently, the node order of a section corresponds with the node
sequence of a tree.

**CLARIFICATION**
A section is a sequence of strictly subsequent nodes.

That is, because a section corresponds with the node sequence of a tree, and
because a section has no gaps in between any two of its adjacent nodes.
