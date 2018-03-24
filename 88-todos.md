
<!-- ======================================================================= -->
# List of things to do

The ultimate goal is to leave no question unanswered -
develop a design that can be used to explain all possible circumstances -

A painfully slow and nerve wrecking process -
It looks like, I'm just too darn stubborn to give up -

always having to look/backwards in order to
know where and how to continue -
like climbing a mountain by moving backwards

<!-- ======================================================================= -->
## minor/isolated/mixed

a section tree is just another node tree -
fundamental conclusions drawn based on the section tree,
may also apply to any other node tree -

**TODO**
is that loop sufficient? -
with regards to implicit associations -
-> in 3-8-1-implementation

**TODO**
coin the term "a design's structural integrity"? -
i.e. a design must be in itself consistent -

**TODO**
an algorithm can in principle start at any node -
the root node must be treated as a type-1 sectioning node -
could that type-switching even be implemented? -
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
question is, if a node tree defines a set-subset relationship -

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
overlay or embedded perspective?
does the logical hierarchy act as a flat overlay on top of the node tree -
is the logical hierarchy embedded into the node tree? -
put differently, is the logical structure an integral part of the node tree? -
the overlay perspective is similar to looking through a window -

**TODO**
"executing" an algorithm on a node sequence (event sequence)
feels a lot like a turing machine

**TODO**
mobile - crib mobile -
just a visual image

**compilers** -
headings <=> variable/parameter declarations -
sections <=> scopes/blocks -

**file systems** -
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
