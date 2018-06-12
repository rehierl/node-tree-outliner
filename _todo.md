
<!-- ======================================================================= -->
# List of things to do

The ultimate goal is to leave no question unanswered -
develop a design that can be used to explain all possible circumstances -

A painfully slow and nerve wrecking process -
It looks like, I'm just too darn stubborn to give up -

always having to look/backwards -
in order to know where and how to continue -
like crawling up a mountain by moving butt first

<!-- ======================================================================= -->
## minor/isolated/mixed

- a section is a subset of the tree's set of nodes
- a section is a strict subset of the root's outer set of nodes
- a section is a subset of the root's inner set of nodes -
  that is, a section may be identical to the root's inner set
- a section either is identical to the inner set of a node,
  or a union of the outer sets of one or more subsequent siblings
- if a section is identical to the inner set of a node, then that section
  is also the union of all of the outer sets of that node's child nodes

conclusions
- sections either have no nodes in common (e.g. sections B and C),
  or one section is embedded within the other (e.g. sections B into A)
- a section is a subset of another section, if it is embedded into it
- the tree of sections must be consistent with the node tree's
  hierarchy of sets/sequences- why?

**TODO**
the tree of sections will have identical structure to the initial node tree,
if each node of the node tree is understood to represent a rank-less type-1
sectioning node.

**TODO**
closing a section when the next heading was about to be entered did work
for as long as our documents were flat. however, it no longer works because
our documents are no longer flat (we now use node trees). - closing a section
when the next heading is entered may be in conflict with a node tree's
hierarchy of sets/sequences. some sections must be closed before the next
heading is entered.

**TODO**
one node tree may have multiple different outlines at the same time -
read the "red", or the "blue" outline -
but may also have a hierarchical listing of outlines -
i.e. a tree of outlines within a document -

**TODO**
The issue with end-marker nodes is that they can be placed inside of a type-1
section. To which section does a subsequent node belong? What happens in
case of user/input errors?

**TODO**
closing a subsection does not necessarily mean that ancestor sections are
closed as well - in contrary to that, closing an ancestor section requires
that all subsections are also closed -
proof that those nodes must be associated with the parent section of the
most significant section being closed? -
wouldn't add up with close modifiers

**TODO**
a path of nodes is a rooted tree of nodes -
the path as a single root and each node has a parent -
in addition to that, each parent has a single child -
the definition of the node order of a tree must also include such a tree -
so yes, each parent *is presequent* to all of its descendants -
that is, because it is independent of which rooted path was selected -
then, add a sibling to one of the nodes in the path -
the first child of a node is still presequent to the parent's last child -
question is, are the descendants of a sibling
presequent to its subsequent siblings? -
if yes, then the series of enter events truly represents
the node order of the corresponding node tree -
start with the tag sequence of a node tree -
then remove those start xor end tags of a node
that do not represent a node's true position -

**TODO**
with regards to `Node.parentSection` -
maintain a global list of all sections -
define `Node.parentSectionIndex` instead -
i.e. use index values instead of node references -
i.e. use index values to reduce the memory footprint -

**TODO**
transformations -
replace multiple nodes with a single node -
that contains the previous nodes as its descendants -
and which acts as the representative of the replaced content -
similar to that, a sectioning node acts as a representative -

**TODO**
a node represents a set of nodes (descendants) -
of which it is itself not a part -
consistent with leaf nodes (empty set) -

**TODO**
a section tree is just another node tree -
fundamental conclusions drawn based on the section tree
will also have to apply to any other node tree -

**TODO**
parent containers, a definition by choice? -
is there a formal/mathematical reason why they are needed? -
i.e. allow to find a contradiction in the statements that
are related to those paths in `S{+}N{+}`? -

**TODO**
coin the term "a design's structural integrity"? -
i.e. a design must be in itself consistent -

**TODO**
an algorithm can in principle start at any node -
the root node must be treated as a type-1 sectioning node -
could that type-switching even be implemented? -
sure: if exiting at node level 1 -
any node can be understood to have an outline -
issue header element in combination with reusing heading elements -
i.e. a 1st header element can not always be recognized to be with
regards to a presequent (possibly outside of corresponding subtree)
type-1 sectioning node -
not the case when reusing the title element -

<!-- ======================================================================= -->
## subset/subsequence <=> node tree/hierarchy

set-subset => tree of sections -
the set-subset relationship defines a tree of nodes/sections -

tree of nodes ?> set-subset relationship -
question is: can a node tree be understood to define a set-subset relation? -

each node in a tree can be understood to declare a subset of nodes? -
equivalent with the contains relation? -
hence the similarity with type-1 sectioning nodes -

likewise, each node in a tree can be understood
to declare a list/sequence of child nodes? -

a bridge towards sectioning nodes not belonging
to the sections they declare? -
because a node is not an element of the set of nodes
it can be understood to declare? -

<!-- ======================================================================= -->
## transformations

(type-1 <=> type-2)

interchangeable/synonymous under the default definitions? -
if so, then the extended definitions must not deviate

not quite -
t1 sections are in general closed -
t2 sections are in general open -

describe multistep transformations -
already done ?

usability perspective => use t2 over t1 -
especially due to close modifiers -
algorithmic perspective => use t1 over t2 -
consistent transformations are a must have

**TODO**
top-level nodes -
with regards to the support of transformations -
-> expand in 3-8-1-implementation

**TODO**
transformations require a null/sandbox-container -
i.e. a container without a meaning other than to group nodes -
e.g. HTML's `<div>` container element -

<!-- ======================================================================= -->
## type-1 sectioning nodes

(close modifiers vs. type-1 sections)

`Section SectioningNode.declaredSection` - singular, not plural -
in conflict with "one or more (i.e. a list of) sections" -

Note that this does not mean that a sectioning node is not allowed to hold
a reference to the section it declares, which still is a single section only.

an outline object type (singular) can be used to represent such a list -
but that requires an additional type of object -
thus, there must be a good/solid reason to justify an additional object type -

**TODO**
extended definitions must be consistent with the default definitions -
would that be an argument against closing a type-1 section? -
don't close type-1 sections if it is inconsistent with the default definitions? -
are transformations possible? -

**TODO**
Note that no definition, not even a modified definition, can close the
theoretical, omnipresent universal section. However, non-default definitions
may still be allowed to close the root section (which does not mean that it
would be reasonable).

**TODO**
could it be that the definition of sectioning content elements is unspecific -
because the definition of heading content elements is unspecific -
"a /parent b" - a heading's section contains "b" -
so the section of a sectioning content element must also contain "b"? -
an attempt to be consistent with old definitions? -
indicates that transformations are not consistent (under these definitions)? -

**TODO**
Note that the `subsection-of` relationship does not support sibling sections
at the very top. The underlying `subset-of` relationship does not support
that. Feels like a solid/formal reason to not close type-1 sections.

**TODO**
use/compare node levels of sectioning nodes (not parent containers) -
depends on: allow/disallow closing type-1 sections -
-> expand in 3-8-1-implementation

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
a type-2 sectioning node always is a leaf node - nope, data nodes -

issue with tables -
table/tr/td (sectioning root) -
can only be a rule of thumb -
all td-sections are subsections of the section with which a table is associated

<!-- ======================================================================= -->
## general thoughts

**TODO**
the outline, an overlay or an embedded perspective?
does the logical hierarchy act as a flat overlay on top of the node tree -
is the logical hierarchy embedded into the node tree? -
put differently, is the logical structure an integral part of the node tree? -
the overlay perspective is similar to looking through a window -

a different perspective -
all sectioning nodes shifted to the top of the tree -
so it seems that the logical layer can always be understood
to be embedded into the node tree -
the global scope is the content of the root node -

**TODO**
"executing" an algorithm on a node sequence (event sequence)
feels a lot like a turing machine

**TODO**
mobile - crib mobile -
just a visual image for a node tree -

**compilers** -
headings <=> variable/parameter declarations -
sections <=> scopes/blocks -

**file systems** -
alphabetical order vs. order of appearance

issue with folder/file node types? -
similar to browser bookmarks, etc -
could allow a "different" view -
similar to views in a database

these act (display wise) more like unordered trees -
with that in mind, folders are like type-1 sectioning nodes -
type-2 sectioning nodes don't/can't exist

the node order of the tree must be independent of the node types -
in contrary to that, the view of a fs is ordered folders-first -
but, folders are just files themselves (folder = list of files and folders)

understand sections to be folders and nodes to be files? -
meh, files are leaf nodes - they have no subordinate entities
