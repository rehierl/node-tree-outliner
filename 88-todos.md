
<!-- ======================================================================= -->
# List of things to do

**TODO**
no conflict in location of a section -
sectioning node, first node, last node, etc.

**CLARIFICATION**
No two sections within a single tree have identical reduced sequences.
These are unique to a section.

* Each sectioning node declares its own section.
* Each first node is strictly subsequent to the corresponding event.
* No two sections have the exact same first node.

**TODO**
type-1 section -
all child nodes, or just the first ones? -
allow a type-1 section to end inside of its container? -
with regards to the root node

**TODO**
describe the purpose of a sectioning node inside of presequent sections -
not associated with its declared section

**TODO**
don't associate sectioning nodes with the sections they declare -
`Section Node.parentSection` property would be inconsistent -
requires hierarchy of sections

**TODO**
can a running algorithm easily store references to all top-level nodes? -
is it possible to avoid having to determine them manually by providing
a list of top-level nodes?
