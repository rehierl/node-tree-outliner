
<!-- ======================================================================= -->
# Design (2) - States of a section

Similar to output streams, any section has the following states:

<!-- ======================================================================= -->
## initialized state

As soon as a sectioning node is known, it is technically possible to, beginning
with the current node, associate any subsequent node with it. Because of that,
and if a section had no delayed start, a sectioning node would have to be
associated with its own section.

Consequently, a section's "initialized" state means that: (1) the section is
known and (2) an algorithm must start associating nodes with it at some later
point in time.

<!-- ======================================================================= -->
## open state

Once a section's first node is entered, this first node and any subsequent node
must be associated with it. An algorithm therefore needs additional rules that
enable it to determine when to begin associating nodes with a section.

A section is considered to be "open" as soon as the next subsequent node must
be associated with it.

<!-- ======================================================================= -->
## closed state

Any section must eventually end at some point. By default, that point is reached
when the initial root node of the process is being exited. That is, because
there is no subsequent node with regards to this exit event.

This default case is obviously insufficient, because the very last node of
a node sequence would then always have to be associated with all the known
sections. An algorithm therefore needs additional rules that enable it to
determine, when it is no longer allowed to associate any subsequent node
with a section.

A section is considered to be "closed" as soon as it is no longer allowed to
associate any more nodes with it.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Once closed, a section is fully defined/specified. That is, because no
subsequent node will, by definition, have any further effect on it.

**CLARIFICATION**
A section can not be re-opened.

The "closed" state, and the corresponding rules, can therefore also be seen
to represent a guarantee, that a closed section will not change any further.

This guarantee is critical to an efficient TOC generator, because it allows to
drop a section object once the corresponding section is closed and once the the
information it holds has been extracted. After that, any attempt to execute any
kind of operation on a dropped section object will result in an access violation
error.

Re-opening a section for additional associations would therefore be in conflict
with the above guarantee. Because of that, such an operation must be seen to
represent an attempt to suspend and resume a section.

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

In addition to that, the intermediate nodes in between the separate parts of a
strictly suspended section can still be seen to be in relationship with it. That
is, because the very reason, as to why these intermediate nodes would have to be
excluded, puts these intermediate nodes into a relationship with said section.
After all, they would be a reason as to why they are surrounded by the section's
parts. Because of that, the ultimate goal of such an attempt (i.e. completely
unrelated nodes) can't even be reached without producing a conflict.

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
order of nodes, and, as such, a deviation of the tree's semantics. Consequently,
associating any nodes with sections while they are being exited can in principle
not result in sections that accurately represent the contents of a tree.

Apart from that, the location of a node (in terms of a tree's sections) could
also be affected by nodes that are subsequent to it. Because of that, a node
could turn out to have an effect on nodes that are presequent to it.

**CLARIFICATION**
A section is a sequence of subsequent nodes.

That is, because any node must be associated with a section while it is being
entered. Consequently, the node order of a section corresponds with the node
sequence of a tree.

**CLARIFICATION**
A section is a sequence of strictly subsequent nodes.

That is, because a section corresponds with the node sequence of a tree, and
because a section has no gaps in between any two adjacent nodes.
