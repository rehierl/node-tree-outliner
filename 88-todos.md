
<!-- ======================================================================= -->
# List of things to do

**TODO**
`currentSection` variable

**TODO**
better terms for type-1/2 sectioning nodes? -
sectioning container node (ok) -
sectioning offset/open node (?) -
sectioning end/close node (see end marker nodes) -

**TODO**
can an algorithm easily store references to all top-level nodes? -
is it possible to avoid having to determine them as a post-process
by providing a list of top-level nodes? -
won't work on the fly (associate with one section only) -
when a section is being closed, or an on demand feature

**TODO**
No two sections within a single tree have identical
complete or even reduced sequences. These are unique to a section. -
No two sections have identical first nodes.

**TODO**
HTML's sectioning content is defined as - subsection-of the nearest -
if deep into the structure, then close multiple sections -
if shallow, then close just a few, if any -
can be seen to be inconsistent

**TODO**
describe multistep transformations -
already done ?

**TODO**
tree of sectioning nodes -
the parent node of a type-1 sectioning node always is a type-1 -
the parent node of a type-2 sectioning node always is a type-1 -
a type-1 sectioning node can be a parent or a leaf -
a type-2 sectioning node always is a leaf node -
issue with tables? table/tr/td (sectioning root) -

<!-- ======================================================================= -->
## type-1 sectioning nodes

**TODO** -
`Section SectioningNode.declaredSection` is singular, not plural -
in conflict with "one or more (i.e. a list of) sections"

Note that this does not mean that a sectioning node is not allowed to hold
a reference to the section it declares, which still is a single section only.

<!-- ======================================================================= -->
## implementation specific

`Section Node.parentSection` -
a hint towards how it has to be implemented.

An implementation does not have to keep references to
all open sections at hand - i.e. as an ordered list.

An algorithm only needs to know what the parent section of the
next subsequent node is - use `Section Section.parentSection`.

**TODO** -
similar to if-then-else constructs in a programming language -
rethink that thought! - sibling sections? -
sectioning nodes belong to the parent section? -

**TODO** -
The exit event of any container node needs to check
if one or more sections end with it.

* any container node could be the parent container of a section.
* any number of sections may have the same parent container.
* a declared section may already be closed due to a non-default definition.

<!-- ======================================================================= -->
## rank of a section

**DEFINITION**
The rank of a section is the number of its ancestor sections -
or better outline depth

Note that the universal section is always included. That is, the root section
has rank 1 and the universal section has rank 0. Note also that this is similar
to a node's node level within a tree of nodes. That is, the root node has node
level 1.

<!-- ======================================================================= -->
## other applications

**filesystems** -
issue with folder/file node types? -
similar to browser bookmarks, etc -
could allow a "different" view -

**compilers** -
headings <=> variable/parameter declarations -
sections <=> scopes/blocks -

<!-- ======================================================================= -->
## optional end marker nodes

The definition of optional end marker nodes (e.g. `<close/>`) must not define
these nodes to be associated with the sections they are supposed close.

That is, because it would be inconsistent with not associating sectioning
nodes with the sections they declare.

In addition to that, and if such an end marker would be allowed to close
multiple sections at once, then there would be the issue to decide with
which of the to-be closed sections it would have to be associated.

The issue with such nodes is that they could be placed inside of a type-1
section. To which section does a subsequent node belong? That is, user/input
errors must be taken into account.
