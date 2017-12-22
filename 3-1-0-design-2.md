
<!-- ======================================================================= -->
# Design (2) - States of a section

Similar to output streams, any section has the following states:

<!-- ======================================================================= -->
## initialized state

As soon as a sectioning node is known, it is technically possible to, including
the current sectioning node, associate any subsequent node with it. Because of
that, and if a section had no delayed start, a sectioning node would have to be
associated with its own section.

Consequently, a section's "initialized" state means that: (1) the section is
created/initialized and (2) an algorithm will, at some later point in time,
begin associating nodes with it.

(-> initialized)
A section's "initialized" state is a section's first/initial state.

<!-- ======================================================================= -->
## open state

Once a section's first node is entered, this first node and any subsequent node
must be associated with it. An algorithm therefore needs additional rules that
enable it to determine when to begin with the association of nodes.

A section is considered to be "open" as soon as the next subsequent node
must be associated with it.

(initialized -> open)
A section can only change to its "open" state,
if its current state is "initialized".

<!-- ======================================================================= -->
## closed state

Any section must eventually end at some point. By default, that point is
reached when the initial root node of the process is being exited. That is,
because the root node has no node that is subsequent to it.

This default case is obviously insufficient, because the very last node of
a node sequence would then always have to be associated with all the known
sections. An algorithm therefore needs additional rules that enable it to
determine, when it is no longer allowed to associate any other subsequent
nodes with a section.

A section is considered to be "closed" as soon as it is no longer allowed
to associate any further nodes with it.

(open -> closed)
A section can only change to its "closed" state,
if its current state is "open".

<!-- ======================================================================= -->
## set of open sections

As mentioned earlier, and without the ability to limit a section's scope, the
last subsequent node of a tree would have to be associated with all the known
sections. Obviously, authors need the means to tell an algorithm when it is
no longer allowed to associate any more nodes with a given section. Once such
a statement is detected, an algorithm must mark the corresponding section, or
multiples thereof, as being "closed".

Consequently, and at any given point in time, any section within the set of
known sections is "initialized", "open" or "closed". Because of that, the set
of known sections `S` can be broken apart into three disjunct sets of sections
(with each subset containing only those sections that are in the corresponding
state):

* the set of initialized sections `IS`
* the set of open sections `OS`
* the set of closed sections `CS`.

With regards to associations, a section's "initialized" and "closed" states
appear to be semantically equivalent. That is, because no associations are
allowed unless a section's state is set to be "open".

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
A closed section can only be understood to represent an empty section, if
it was opened and then closed without associating any nodes with it.

Consequently, it must be considered to be an error, if the section's state
is "initialized" when it is about to be closed. Otherwise, the contents of
a section would have to be understood as being "undefined". That is, no
statements can be made about the contents of a closed section that was
never open. After all, "undefined" is not equal to "empty".

**CLARIFICATION**
It is not allowed to re-initialize, or re-open a closed section.

The "closed" state, and the corresponding rules, can therefore also be seen
to represent a guarantee that a closed section will not change any further.

This guarantee is critical to an efficient TOC generator, because it allows to
drop a section object once the corresponding section is closed and once the the
information it holds has been extracted. After that, any attempt to execute any
kind of operation on a dropped section object will result in an access violation
error.

Re-opening a section for additional associations would therefore be in conflict
with the above guarantee. Because of that, such an operation must be seen to
represent an attempt to suspend and then resume a section.

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
associated with it, and that section `s` would have to be resumed beginning with
some node `nr`. This would in return mean that, in between both nodes, there
need to be any number of nodes that are supposed to be completely unrelated to
this section (hence, strictly suspended).

Note that these considerations do not take the definition of nodes into account,
that would allow to clearly define when a section has to be suspended and when
it has to be resumed.

Such a section would then consist of multiple subsequent parts that are separate
from each other. Due to the gaps in between the section's parts, an algorithm
would then have no means to treat a section as as one entity by grouping all of
the section's nodes, which would obviously be in conflict with the initial
requirements.

In addition to that, the intermediate nodes in between the separate parts of
a strictly suspended section can still be seen to be in relationship with it.
That is, because the very reason, as to why these intermediate nodes would have
to be excluded, puts these intermediate nodes into a relationship with said
section. After all, they would be a reason as to why they are surrounded by the
section's parts. Because of that, the ultimate goal of such an attempt (i.e.
completely unrelated nodes) can't even be reached without producing a conflict.

Finally, the subsequent parts of a strictly suspended section can also be seen
to represent sections of its own. Hence, the nodes that would be required in
order to tell an algorithm that it has to resume a section can themselves be
seen to represent separate sectioning nodes. The separate parts can then be
seen to represent separate sections.

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
