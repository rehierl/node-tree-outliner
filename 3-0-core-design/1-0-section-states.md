
<!-- ======================================================================= -->
# Design - section states

Similar to output streams, any section has the following states:

<!-- ======================================================================= -->
## initialized state

As soon as a section is known, it is technically possible to associate
any subsequent node with it (including the section's sectioning node).

Consequently, a section's "initialized" state means that: (1) the section is
created/initialized/known and (2) an algorithm needs to, at some later point
in time, begin associating nodes with it.

(-> initialized)
As soon as a new section object is created, it must be marked as being
"initialized". A section's "initialized" state is the first/initial state
of a section.

<!-- ======================================================================= -->
## open state

Once a section's first content node is entered, this first node and any
subsequent node must be associated with that section until it is closed. An
algorithm therefore needs additional rules that enable it to determine when
to begin with the association of nodes.

A section is considered to be "open" as soon as the next subsequent node
must be associated with it.

(initialized -> open)
A section can only change its state to "open",
if its current state is "initialized".

<!-- ======================================================================= -->
## closed state

Any section must eventually end at some point. By default, that point is
reached when the root node of the tree is being exited. That is because
the root node has no node that is subsequent to it.

This default case is obviously insufficient, because the very last node of
a node sequence would then always have to be associated with all the known
sections. An algorithm therefore needs rules that allow it to determine,
when it is no longer allowed to associate any further subsequent nodes with
a known section.

A section is considered to be "closed" as soon as it is no longer allowed
to associate any further subsequent nodes with it.

(open -> closed)
A section can only change its state to "closed", if its current state is "open".
A section's "closed" state is the final state of a section. That is, once a
section's state is "closed", no further state transitions are allowed.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The node event that is used to create and initialize a new section object
(e.g. the enter event of its sectioning node) is said to represent a section's
"create" event. Likewise, the event used to open a section is referred to as the
section's "open" event, and the event used to close a section as the section's
"close" event.

No other operation with regards to the corresponding section is allowed to
be executed during such an event. That is, an algorithm is not allowed to
associate any nodes with the corresponding section (i.e. add nodes to it)
during the execution of one of the above mentioned events. These node events
are only allowed to change the state of a section.

However, a single node event can still be used to execute multiple section
events. A node event can be used to create, initialize and open a declared
section. Also, a single node event could technically open and close a section.
Obviously, and in the latter case, such a section would then always be empty.

**CLARIFICATION**
A section that counts as being "initialized" is neither "open" nor "closed".

The goal must be to have clear definitions, for each and every section, which
state when a section has to be opened and when it has to closed. That is, it
must count as an implementation, or even a design error, if an implementation
would try to execute an undefined state transition (e.g. re-open an already
closed section).

The contents of a section, that still counts as being "initialized", must be
understood to be "undefined". As such, no statements can be made with regards
to the contents of such a section. That is because the section's "open" event
was never executed. Consequently, a section that was never opened can also not
be understood to be "empty". After all, an "initialized" section can still be
opened, and nodes can still be associated with it. Any attempt to close an
"initialized" section, without first changing its state to being "open", must
be understood to represent an error.

In short: No other transitions, except for the above mentioned, are allowed.
In addition to that, no statements can be made with regards to the contents
of a section, unless the section's state is "closed".

<!-- ======================================================================= -->
## set of open sections

At any given point in time, any section within the set of known sections is
either "initialized", "open" or "closed". Because of that, the set of known
sections `S` can be broken apart into three disjunct subsets (with each
subset containing only those sections that have the corresponding state):

The set of ...

* initialized sections `IS`
* open sections `OS`
* closed sections `CS`.

With regards to associations, a section's "initialized" and "closed" states
appear to be equivalent. That is because no associations are allowed unless
a section's state is "open".

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
It is not allowed to re-initialize, or re-open a closed section.

A section's "close" event, and the corresponding rules, can be understood
to represent a guarantee that a section will not change any further.

This guarantee is critical to an efficient TOC generator, because it allows to
drop a section object once the corresponding section is closed and once the
information it holds has been extracted. After that, any attempt to execute any
kind of operation on a dropped section object will result in an access violation
error.

Re-opening a section for additional associations would obviously be in conflict
with that guarantee. Because of that, such an operation must be understood as
an attempt to suspend and then resume a section.

**CLARIFICATION**
A section can not be strictly suspended.

Note that it is assumed, that a "resume" operation must always follow a
"suspend" operation ("suspend" would otherwise be equivalent to "close").

Technically, it would be possible to define rules that tell an algorithm to
suspend and then, at some later point in time, resume associating nodes with
a section. However, this does not mean that it would be reasonable to allow
such an operation.

Assumed that section `s` would have to be suspended after some node `ns` was
associated with it, and that section `s` would have to be resumed beginning
with some other node `nr`. This would in return mean that, in between both
nodes, there could be any number of intermediate nodes that are supposed to
be completely unrelated to that section (hence, strictly suspended).

A section would therefore, if suspend-and-resume operations were allowed,
consist of multiple subsequent parts that are separate from each other. Due
to these gaps in between the separate parts, an algorithm would then have
no means to treat a section as one entity by grouping together all of the
section's content nodes. Because of that, suspend-and-resume operations are
in conflict with the initial requirements.

In addition to that, the subsequent parts of a strictly suspended section
can also be seen to represent separate sections of their own. Hence, the
nodes that would be required to tell an algorithm that it has to resume a
section can be understood to represent additional sectioning nodes. From
that perspective, these nodes appear as sectioning nodes, but are not
treated as such. Consequently, strict suspend-and-resume operations can
be seen to add inconsistency to a design.

In short: It does not seem to be reasonable to support
strict suspend-and-resume operations.

**CLARIFICATION**
A section has no gaps.

Because of that, any node belongs to a section, if it is subsequent
to the section's open and presequent to the section's close event.

**CLARIFICATION**
Once closed, a section is fully defined/specified. That is because no
subsequent node will, by definition, have any further effect on it.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
All nodes must be associated while they are being entered.

Because exit events will be executed in reverse order, associating any nodes
while they are being exited would constitute a deviation of the tree traversal's
order of nodes, and as such, a deviation of the tree's semantics. Consequently,
adding nodes to sections while they are being exited can in principle not result
in sections that accurately represent the contents of a tree.

Apart from that, the logical location of a node (i.e. with regards to the
sections of a tree) could also be affected by nodes that are subsequent to
it. Because of that, a node could end up having an effect on nodes that are
presequent to it.

**CLARIFICATION**
All nodes entered in between a section's open and close events
are said to be the content nodes of a section.

Note that this clarification is necessary, because the descendants of a type-2
sectioning node are not supposed to contribute to the content of such a section.
This would otherwise be inconsistent with the initial requirement that it must
be possible to treat a section as a whole. That is because of not associating
sectioning nodes with their own section.

**CLARIFICATION**
A section is a sequence of subsequent nodes.

That is because any node must be associated with a section while it is being
entered. Consequently, the node order of a section corresponds with the node
order of the tree.

Note that "subsequent" always is with regards to the tree's node sequence.

**CLARIFICATION**
A section is a subsequence of the tree's node sequence.

Because a section is a sequence of subsequent nodes, and because a section has
no gaps in between any two of its adjacent nodes, a section is a sequence of
strictly subsequent nodes. Consequently, a section is a subsequence of the
tree's node sequence.
