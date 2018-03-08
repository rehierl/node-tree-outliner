
<!-- ======================================================================= -->
# List of things to do

The ultimate goal is to leave no question unanswered.

A painfully slow and nerve wrecking process -
It looks like, I'm just too darn stubborn to give up -

always having to look/backwards in order to
know where and how to continue -
like climbing a mountain by moving backwards

<!-- ======================================================================= -->

**TODO**
find a term for type-2 sections that
have an inactive node as parent container -
inner sections: also applies if the parent container
is a type-1 sectioning node -
a description similar to "implied sections"

**TODO**
No two sections within a single tree have identical
complete or even reduced sequences. These are unique to a section. -
No two sections have identical first nodes.

**TODO**
better terms for type-1/2 sectioning nodes? -
sectioning container node (ok) -
sectioning offset/open node (?) -
sectioning end/close node, or end-marker node -

**TODO**
explain superordinate/subordinate section -
already done ?

**TODO**
we have an outline height/depth - define an outline width? -
the maximum number of sections on a certain outline level? -

**TODO**
implicit relationship -> descendants -
implicit associations -> one section only -
combine both levels of implicitness?

**TODO**
an algorithm can in principle start at any node -
the root node must be treated as a type-1 sectioning node -
any node can be understood to have an outline -
issue header element in combination with reusing heading elements -
i.e. a 1st header element can not always be recognized to be with
regards to a presequent (possibly outside of corresponding subtree)
type-1 sectioning node -
not the case when reusing the title element

**TODO**
HTML's sectioning content nodes are defined as -
subsection-of the nearest ... -
if deep into the structure, then close multiple sections -
if shallow, then close just a few, if any -
i.e. context-dependent - inconsistent?

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
recheck

**TODO**
sectioning a tree (i.e. creating an outline for a tree)
is like grouping nodes on a logical level -
geographical (node tree) vs. political (sections) -
elevate the nodes of a flat, two dimensional surface into the next dimension

<!-- ======================================================================= -->
## transformations

(type-1 <=> type-2)

interchangeable/synonymous under the default definitions? -
if so, then the extended definitions must not deviate

not quite -
t1 sections are in general closed -
t2 sections are in general open -

**TODO**
describe multistep transformations -
already done ?

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
