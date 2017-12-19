
<!-- ======================================================================= -->
# List of things to do

**TODO**
split design-2 into two documents -
states and types

**TODO**
don't associate sectioning nodes with the sections they declare -
`Section Node.parentSection` property would be inconsistent

**TODO**
allow a type-1 section to end inside of its container?

**CLARIFICATION**
No two sections within a single tree have identical reduced sequences.
These are unique to a section.

* Each sectioning node declares its own section.
* Each first node is strictly subsequent to the corresponding event.
* No two sections have the exact same first node.

**TODO**
what type of sectioning node is the root node?

**TODO**
type-1 section -
all child nodes, or just the first ones?

**TODO**
location of a section -
sectioning node, first node, last node, etc.

**TODO**
describe the purpose of a sectioning node inside of presequent sections -
not associated with its declared section

<!-- ======================================================================= -->

Note that, in an ordered tree of nodes, it is technically possible to allow
a type-1 sectioning node to not end with its last child node. This would only
be consistent, if the sectioning node would not belong to its own section (see
loose associations). This would however be inconsistent with the type-1
sectioning node of an unordered tree.
