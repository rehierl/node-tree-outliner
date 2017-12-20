
<!-- ======================================================================= -->
# List of things to do

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
all child nodes, or just the first ones? -
allow a type-1 section to end inside of its container? -
with regards to the root node

**TODO**
no conflict in location of a section -
sectioning node, first node, last node, etc.

**TODO**
describe the purpose of a sectioning node inside of presequent sections -
not associated with its declared section

**TODO**
don't associate sectioning nodes with the sections they declare -
`Section Node.parentSection` property would be inconsistent -
requires hierarchy of sections
