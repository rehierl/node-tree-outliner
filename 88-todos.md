
<!-- ======================================================================= -->
# List of things to do

The ultimate goal is to leave no question unanswered.

A painfully slow and nerve wrecking process -
It looks like, I'm just too darn stubborn to give up -

always having to look/backwards in order to
know where and how to continue -
like climbing a mountain by moving backwards

<!-- ======================================================================= -->

(a misplaced note)
Note that no definition, not even a modified definition, can close the
theoretical, omnipresent universal section. However, non-default definitions
may still be allowed to close the root section (which does not mean that that
would be reasonable).

**TODO**
a heading that has a rank may/can act as an end-marker node -
that is, a rank adds an additional role to a heading element -
could that be used to proof that no t1 section can be closed?

**TODO**
top-level nodes -
with regards to the support of transformations -
-> expand in 3-8-1-implementation

**TODO**
use/compare node levels of sectioning nodes -
depends on: allow/disallow closing type-1 sections -
-> expand in 3-8-1-implementation

**TODO**
is that loop sufficient? -
i.e. with regards to implicit associations -
-> in 3-8-1-implementation

**TODO**
add the term "structural integrity"?

**TODO**
proof that a path in `SN{+}` exists for each path in `S{+}N` -
and by that, proof that those paths allow to make the same statements -
this would confirm the conclusions drawn from the initially defined
`SN{+}` paths. that is, because the corresponding statements can then
also be derived from the `S{+}N` paths -
this would suggest/indicate that the design is in itself consistent -
this would also serve as a formal basis for 2D/3D height maps -
what is there to proof? -> each node is associate with a section -
the root node is associated with the universal section -
-> continue 3-5-3-levels-of-implicitness

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

<!-- ======================================================================= -->
## type-1 sectioning nodes

(close modifiers vs. type-1 sections)

`Section SectioningNode.declaredSection` - singular, not plural -
in conflict with "one or more (i.e. a list of) sections" -

an outline object type (singular) can be used to represent such a list -
but that requires an additional type of object

Note that this does not mean that a sectioning node is not allowed to hold
a reference to the section it declares, which still is a single section only.

<!-- ======================================================================= -->
## perspectives

**TODO**
overlay or embedded perspective?
does the logical hierarchy act as a flat overlay on top of,
or is it embedded into the node tree? -
i.e. is the logical structure an integral part of the node tree? -
similar to looking through a window

**TODO**
structural vs. logical perspective -
node tree vs. section tree -
see "single-s"

**TODO**
sectioning a tree (i.e. creating an outline for a tree)
is like grouping nodes on a logical level -
geographical (node tree) vs. political (sections) -

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

plot twist: see the "extensions" chapter

closing a subsection does not necesarily mean that ancestor sections are closed
as well - in contrary to that, closing an ancestor section requires that all
subections are closed as well - proof that those nodes must be associated with
the parent section of the most signigicant section being closed? -
wouldn't add up with close modifiers

<!-- ======================================================================= -->
## general ideas

**TODO**
mobile - crib mobile -
just a visual image

**TODO**
"executing" an algorithm on a node sequence (event sequence)
feels a lot like a turing machine

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
