
<!-- ======================================================================= -->
# List of things to do

The ultimate goal is to leave no question unanswered.

A painfully slow and nerve wrecking process ...
It looks like, I'm just too darn stubborn to give up ...
"Ain't No Mountain High Enough" :)

**TODO**
No two sections within a single tree have identical
complete or even reduced sequences. These are unique to a section. -
No two sections have identical first nodes.

**TODO**
better terms for type-1/2 sectioning nodes? -
sectioning container node (ok) -
sectioning offset/open node (?) -
sectioning end/close node, or end marker node -

**TODO**
can an algorithm easily store references to all top-level nodes? -
is it possible to avoid having to determine them as a post-process
by providing a list of top-level nodes? -
won't work on the fly (associate with one section only) -
when a section is being closed, or an on demand feature?

**TODO**
HTML's sectioning content nodes are defined as -
subsection-of the nearest ... -
if deep into the structure, then close multiple sections -
if shallow, then close just a few, if any -
can be seen to be context-dependent (i.e. inconsistent) -

**TODO**
describe multistep transformations -
already done ?

**TODO**
"executing" an algorithm on a node sequence (event sequence)
feels a lot like a turing machine

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
## type-1 sectioning nodes

**TODO** -
`Section SectioningNode.declaredSection` - singular, not plural -
in conflict with "one or more (i.e. a list of) sections"

Note that this does not mean that a sectioning node is not allowed to hold
a reference to the section it declares, which still is a single section only.

<!-- ======================================================================= -->
## the current section variable

**TODO**
explain the `currentSection` variable -
used to associate each node with a single section -
in combination with a stack-of-open-sections

<!-- ======================================================================= -->
## list/path/stack of open sections

**CLARIFICATION**
The path/stack of open sections is a rooted path in the tree of sections.

* contains all currently open sections
* connects the root section with the current section
* a presequent path of sections contains closed sections
* a subsequent path of sections contains subsequent sections

<!-- ======================================================================= -->
## implementation specific

(with regards to - implicit associations)

the node level of a sectioning node acts as a rank-like value -
which must have precedence over any user-defined rank value -

the node level of the top-level content nodes can be derived from the
definition of the corresponding sectioning node

<!-- ======================================================================= -->
## implementation specific

(with regards to - parent containers)

`Section Node.parentSection` -
a hint towards how it has to be implemented.

An implementation does not have to keep references to
all open sections at hand - i.e. as an ordered list of sections.

An algorithm only needs to know what the parent section of the
next subsequent node is -
then use the `Section Section.parentSection` property -

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

close the inner sections in reverse order until the parent container's
parent section is reached, i.e. close the open presequent sections upwards,
in the direction of the root section

<!-- ======================================================================= -->
## tree of sectioning nodes

In order to avoid unexpected results due to implicit associations,
a node tree should contain a tree of sectioning nodes.

Take a node tree and remove all inactive nodes and those edges that begin or
end in such a node. The resulting relation should (A) contain the original
root node, and (B) define a single rooted tree of sectioning nodes.

the parent node of a type-1 sectioning node always is a type-1 -
the parent node of a type-2 sectioning node always is a type-1 -
a type-1 sectioning node can be a parent or a leaf -
a type-2 sectioning node always is a leaf node -

issue with tables? table/tr/td (sectioning root) -

<!-- ======================================================================= -->
## optional end marker nodes?

The definition of optional end marker nodes (e.g. `<close/>`) must not define
these nodes to be associated with the sections they are supposed close.

That is, because it would be inconsistent with not associating sectioning
nodes with the sections they declare. The subsection's "frame" belongs to
the parent section.

In addition to that, and if such an end marker would be allowed to close
multiple sections at once, then there would be the issue to decide with
which of the to-be closed sections it would have to be associated.

The issue with such nodes is that they could be placed inside of a type-1
section. To which section does a subsequent node belong? That is, user/input
errors must be taken into account.

<!-- ======================================================================= -->
## other applications

**filesystems** -
issue with folder/file node types? -
similar to browser bookmarks, etc -
could allow a "different" view -
similar to views in databases

**compilers** -
headings <=> variable/parameter declarations -
sections <=> scopes/blocks -
