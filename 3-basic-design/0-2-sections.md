
<!-- ======================================================================= -->
# Design - sections

In principle, an algorithm must traverse the node tree in order to visit and
associate each node with at least one section. Because of that, a section can
initially be understood as a (logical) group of nodes.

Therefore, sections can be understood the define the logical relationship
between nodes (logical perspective). Consequently, the node tree can be
understood to define structural relationship between all nodes (structural
perspective).

<!-- ======================================================================= -->
## set of sections (S), SxN

**DEFINITION**
A section is a set of nodes.

The common aspect of the initially mentioned requirements is that any node must
belong to at least one section. In addition to that, no node can belong to the
same section more than once. Hence, sections can be defined as sets of nodes:

* `s := {n1,...,nk}`, `s in S`, `ni in N`
* `S` represents the set of sections, `N` the set of nodes
* `(s subset-of N)` is true for any `s in S`
* `(is-empty s)` is true, if `(#s == 0)`
* `#s := k`, `k in [0,#N]`

If node `n` is determined to be associated with section `s`, then node `n` must
be added to section `s` as one of its elements (Note that this is just a formal
requirement). By itself, this `add` operation defines a many-to-many (N:M)
relation which will be referred to as the "SxN relation".

* `(s contains ni)` is true, if `(ni in s)`
* `contains` is said to be the semantics of the `SxN` relation.
* `(ni element-of s)` is true, if `(ni in s)`
* synonymous - `element-of`, `belongs-to`, `located-within`, etc.
* `(s related-to ni)` is true, if `(ni in s)`
* `(ni related-to s)` is true, if `(ni in s)`

Note that the `contains` relation is said to be "directional" because the order
of elements in the corresponding expressions does matter. In contrary to that,
the `related-to` relation is said to be "un-directional".

Note that the direction of the `contains` relation is downwards: A superordinate
entity contains an entity which is subordinate to it. And, because of that, the
direction of the inverted `element-of` relation is upwards.

**DEFINITION**
A section is a sequence of nodes.

When the algorithm traverses the node tree, it adds each node to one or more
sections, one after another, in a specific order. Because of that, a non-empty
section has a first and a last node. Consequently, sections can also be defined
as sequences of nodes:

* `s := [n1,...,nk]`, `s in S`, `ni in N`
* `n1` is the section's first node, `nk` is the section's last node
* `(ni != nj)` for `i,j in [1,k]` and `(i != j)`

**CLARIFICATION**
Both of these definitions (i.e. "set of nodes", "sequence of nodes") technically
allow to associate any node with multiple sections. Rules are therefore required
in order to uniquely determine a node's location with regards to the sections
of its node tree (i.e. its logical location).

Note that, because of this formal approach (i.e. associate each node with one
or more sections), the relationship between sections can be ignored for the
time being. Because of that, the relationship between sections must later be
inferred from the associations the sections have with the nodes of the tree.

**DEFINITION**
The scope of a section is the range of nodes that are associated with it.

The scope of a section begins with the section's first node and ends with the
section's last node. Consequently, any non-empty section always has a non-empty
scope. The scope of an empty section is said to be empty. However, an empty
section can also be understood to have no scope at all.

<!-- ======================================================================= -->
## sectioning nodes (SN), NxS

When beginning to traverse a node tree, the set of known sections is initially
empty. Certain nodes are therefore required in order to declare (aka. introduce)
new sections. These nodes will be referred to as the tree's "sectioning nodes".

**DEFINITION**
Any sectioning node always declares a single new section.

* No section can exist without the sectioning node that declares it.
* Any section can be identified by its sectioning node.

Consequently, there is a one-to-one (1:1) relation on the set of sectioning
nodes `SN` and the set of known sections `S`. This relation will be referred
to as the tree's "NxS relation".

* `(sn declares s)` is true, if node `sn` declares section `s`
* `(s declared-by sn)` is true, if `(sn declares s)` is true
* for any `sn in SN subset-of N` and for any `s in S`

An algorithm has knowledge of a section as soon as its sectioning node is being
entered. That is, because a sectioning node always and unconditionally declares
a new section. Because of that, any new section must be added to the set of
known sections as soon as its sectioning node is being entered.

In general, and from that point on, any subsequent node must be associated with
that new and any other known section. Consequently, any node potentially belongs
to multiple sections. That is, because any node can be subsequent to any number
of sectioning nodes.

Note that a sectioning node can be understood to be superordinate to its
subordinate section. That is, the `declares` relation is directed downwards
and its antonym `declared-by` relation is directed upwards.

Note that there will be different types of sectioning nodes. For the time
being, each type of sectioning node can be understood to group together all
those sectioning nodes that have identical characteristics.

**PROPERTIES**
The `NxS` relation can be understood to define the following two
implementation specific object properties:

* `Section SectioningNode.declaredSection`
* `SectioningNode Section.sectioningNode`

**DEFINITION**
A sectioning node does not belong to the section it declares.

Even though a sectioning node is insequent and thus not subsequent to itself,
it is technically still possible to associate a sectioning node with the
section it declares. That is, because an algorithm knows about a section as
soon as it enters the section's sectioning node. However, this does not imply
that it would be reasonable to associate a sectioning node with its own section.

Note that associating a sectioning node with its own section can be seen to
add a node to its own context. That is, a sectioning node would consequently
have an effect on itself as this information would be used to set the
corresponding property of the sectioning node.

Obviously, and as far as possible, an algorithm needs to be able to treat all
sectioning nodes alike. (Note that this will be referred to as "consistent
association across all types of sectioning nodes".) That is, because associating
one type of sectioning nodes with their own section, but not the sectioning
nodes of another type, would make it necessary to add additional logic with
regards to the different types of sectioning nodes.

If all sectioning nodes would have to be associated with their own section,
then no section could ever be empty. That is, because any section would then
always begin with its own sectioning node. And because of that, additional
logic would be required in order to determine if a section contains any
meaningful content or not.

Note that more explanations will follow, which explain from additional
perspectives why sectioning nodes must not be associated with their own
sections and why that rule can not have any exceptions.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
A node sequence of length `N` can declare no more than `N` sections.
That is, because each sectioning node always declares a single section only.

**CLARIFICATION**
A section is said to be subsequent to its sectioning node.

Note that this perspective is based upon a section's first content node,
which always is subsequent to the section's sectioning node.

**CLARIFICATION**
A section is said to be presequent to a node, if the section
is declared by a sectioning node that is presequent to it.

Note that, because of that, a section is understood to be located in between
its sectioning node and its first content node. However, the focus of this
statement is on nodes that are unassociated with the corresponding section.

**CLARIFICATION**
A section is said to be presequent to another section, if its
sectioning node is presequent to the other section's sectioning node.

Note that, except for a tree's first and last nodes, any node is presequent
to the tree's last and subsequent to the tree's first node.

**CLARIFICATION**
A sectioning node can only be associated with a presequent section.

That is, because a sectioning node does not belong to its own section.

**CLARIFICATION**
The structure of all sections is referred to as a tree's "outline".

Note that this basic term does not allow to determine which relationship
the sections have with each other. What structure exactly a tree's outline
has, still needs to be determined.

**CLARIFICATION**
The process of creating an outline for a given tree of nodes may be
referred to as "sectioning the tree", or in general "to section a tree".

Note that such a process can be understood to group the structurally related
nodes (e.g. a geographical relationship) on a logical level (e.g. by political
relationship).

**CLARIFICATION**
With regards to sectioning a tree, the sectioning nodes are said to be the
tree's "active" nodes. Any other node is therefore said to be an "inactive",
or "passive" node. Because of that, a tree's set of nodes can be split into:
(1) the set of active and (2) the set of passive nodes.

Here, the notion of the terms "active" and "passive" refers to a node's
characteristic to have an effect on the outline of its tree. If a node
has such an effect, the node is active, otherwise it is passive.

Note that currently no other types of nodes (besides the sectioning nodes) are
active. If that ever changes (e.g. due to the definition of an end marker node,
or some node property), then the set of active nodes will also contain those
corresponding nodes.

**CLARIFICATION**
In order to simplify discussion, all the nodes of a section, excluding the
section's sectioning node, are said to be the section's "content nodes". These
nodes combined are said to define the "contents of a section". Finally, the
term "section" is in general used to refer to its content nodes.

**Memory hook**
The `NxN` relation can be understood to define a spacial relationship (e.g.
cities on a continent). In contrary to that, the `SxN` relation can be
understood to define a logical relationship (e.g. by political affiliation).

Note that, this perspective is not overly accurate because a political
affiliation may span over multiple segments (e.g. continents and/or islands)
that are structurally separated from each other.

<!-- ======================================================================= -->
## the root node - universal section

**CLARIFICATION**
Any node always belongs to at least one section.

Because a section can not exist without a presequent sectioning node, the root
node, with which an algorithm has to begin, can not be associated with any
predeclared section. That is, because there is no sectioning node presequent
to it that could declare such a presequent section.

However, the root node can be seen to be embedded into a theoretical
universal section `u`. As such, this universal section must be understood
to be declared by a virtual sectioning node that always is presequent to
any node. This universal section must also be understood to never end.
Because of that, the universal section can be understood to be omnipresent.
That is, any node always is related to it (aka. global scope).

Consequently, and because of this formal concept, any node within a tree
always belongs to at least one section. Put differently, there is no node
that does not belong to any section at all.

**CLARIFICATION**
The root node is a sectioning node
and its section is referred to as the "root section".

Without any further clarification, and assumed that a tree's root node does
itself not (strictly or loosely) contain any other sectioning node, all the
nodes in the root's subtree would then only belong to the universal section.
Because of that, the logical location of those nodes would be undefined as
they would all appear lost inside of the global scope.

Consequently, the root node of a tree must always be treated as a sectioning
node. That is especially true, if the algorithm's initial node is the tree's
absolute root node (e.g. the HTML `<body>` element).

**CLARIFICATION**
Any node sequence, in the context of an outline algorithm, always contains
at least one sectioning node. Put differently, any node sequence always has
a first and a last sectioning node. In addition to that, the first node of
a node sequence is always (treated as) a sectioning node.

That is, because the node sequence's first node (i.e. the root node) must
be treated as a sectioning node.
