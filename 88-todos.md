
<!-- ======================================================================= -->
# List of things to do

**TODO**
are there better terms for "type-1/2 sectioning node"? -
e.g. section container node, section starter node

**TODO**
can a running algorithm easily store references to all top-level nodes? -
is it possible to avoid having to determine them manually by providing
a list of top-level nodes? -
one association only vs. reduced node sequence

**TODO**
describe multistep transformations

**TODO**
tree of sectioning nodes -
issue with tables?: table/tr/td

**CLARIFICATION**
No two sections within a single tree have identical reduced sequences.
These are unique to a section.

* Each sectioning node declares its own section.
* Each first node is strictly subsequent to the corresponding event.
* No two sections have the exact same first node.

**TODO**
a section corresponds to some nodes in the tree -
i.e. a section is an arbitrary set/group of nodes -
they simply ignore the node order of a section! -
you can not bend the rules of science, science bends you! -
stop the pillow fight and find a consistent solution!

<!-- ======================================================================= -->

**DEFINITION**
The rank of a section is the number of its ancestor sections.

Note that the universal section is always included. That is, the root section
has rank 1 and the universal section has rank 0. Note also that this is similar
to a node's node level within a tree of nodes. That is, the root node has node
level 1.

<!-- ======================================================================= -->
## type-1 sectioning nodes

**TODO** -
`declaredSection` is singular, not plural -
in conflict with "one or more sections"

```
Section SectioningNode.declaredSection
```

Note that this does not mean that a sectioning node is not allowed to hold
a reference to the section it declares.

<!-- ======================================================================= -->
## implementation specific

`Section Node.parentSection` -
a hint towards how it has to be implemented.

**CLARIFICATION**
(2) the section's default scope ends with the first exit event of a
presequent (i.e. with regards to the first node) and unassociated node.

**CLARIFICATION**
Because an implementation does not always have to keep references to
all open sections at hand. That is, because an algorithm only needs to
know what the parent section of the next subsequent node is. 

**CLARIFICATION**
similar to if-then-else constructs in a programming language -

* any parent node could be the parent container of a type-2 section.
* any number of sections may have the same parent container.
* a declared section may already be closed by some non-default definition.

<!-- ======================================================================= -->
## optional end marker nodes

**CLARIFICATION**
The definition of optional end marker nodes (e.g. `<close/>`) must not define
these nodes to be associated with the sections they are supposed close.

That is, because it would be inconsistent with not associating sectioning
nodes with the sections they declare.

In addition to that, and if such an end marker would be allowed to close
multiple sections at once, then there would be the issue to decide with
which of the to-be closed sections it would have to be associated.

-> parent section -> frame/window
