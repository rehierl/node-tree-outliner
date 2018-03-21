
<!-- ======================================================================= -->
# Design - the SxS relation

**CLARIFICATION**
At any given point in time, during the traversal of the node tree,
there always are one or more open sections.

That is, because each node in a node tree must be associated with at least one
section. For that to happen, one or more sections must always be open when the
next subsequent node is entered.

Note that, when the root node is entered, the universal section is the only open
section. When the root's first child is entered, the universal section and the
root section (always a type-1 section) are open.

**CLARIFICATION**
The section of a subsequent sectioning node
is a subsection to all open presequent sections.

That is, because all presequent sections remain to be open for as long as a
subsection is open. Which is, because the default definitions do not include
the characteristic to close a presequent section. Consequently, a subsequent
section always is a subsection to all open presequent sections.

Note that this is only intended to switch ones perspective from a pair of
sections towards a subsequent inner section (aka. subsection) with regards
to all open presequent sections.

**CLARIFICATION**
Any sectioning node always declares a new subsection.

That is, a sectioning node does not declare some abstract and isolated entity.
The section that a sectioning node declares always is a subsection to one or
more open presequent sections.

Note that this, by itself, does not allow to conclude what the structure of
sections is. The overall structure can technically still be a list of one or
more section trees. That is, if the universal section is ignored.

**CLARIFICATION**
Any parent section may contain multiple independent subsections. That is, the
subsections of a parent section do not necessarily share any content nodes.

That is, because it is possible that the parent container of a presequent
subsection is exited before a subsequent subsection is entered (e.g. a type-1
sectioning node which is a previous sibling to some other sectioning node).

Note that all of these independent and intermediate subsections will be
ignored by the following considerations. That is, because the focus still
is on multiple sections that all are related with each other.

<!-- ======================================================================= -->
## tree of sections

```
... n0 n1 n2 n3 n4 n5 n6 n7 n8 n9 ...
       ========================== s0
          ======================= s1
             ========    ======== s2, s7
```

Select a subsection (e.g. `s2`) and all of its parent sections (e.g. `s0, s1`).

Obviously, these three sections are related with each other. This group of
related sections represents a subset (e.g. `s := { s2, s0, s1 }`) of the set
of known sections `S`.

In addition to that, the sections in such a set of related sections `s` are
ordered. That is, because the set of their sectioning nodes is ordered according
to the node sequence of the tree, which itself is based upon the tree's order
of nodes. (Recall that any section is presequent or subsequent to any other
section.) Consequently, and if that node order is taken into account, the
above set of related sections `s` defines an ordered list of sections (i.e.
`s := [ s0, s1, s2 ]`).

As mentioned before, all sections are subsequences of the tree's node sequence.
Consequently, any section is a subsequence to all of its parent sections. That
is, `s2` is a subsequence of `s1` and `s0`. In addition to that, `s1` is a
subsequence of `s0`.

The relationships between the sections in the above ordered list of related
sections can be used to define a binary relation `R`:

* `(a,b) := (a -> b) := (a subsection-of b)`
* `R := (S,G)`, and `G := { (s2,s1), (s2,s0), (s1,s0) }`

Note that this relation is transitive. Also note, that no rooted tree of nodes
is defined by a transitive relation. If a tree's relation would be transitive,
then there would be nodes that had more than one parent node.

* transitive := if `aRb` and `bRc`, then also `aRc`
* example: `(s2,s1)` and `(s1,s0)` and also `(s2,s0)`

Like the inverted graph of a rooted tree, a relation as defined above does not
(necessarily) define a rooted tree of nodes. That is, because node `s0` has two
different parent nodes (i.e. `s1` and `s2`).

However, if an implicit transitivity is taken into account, the complete
relation of the above example can be defined as follows:

* `R := (S,G)`, and `G := { (s2,s1), (s1,s0), (s7,s1) }`
* `sem(R) := "subsection-of"`

As before, this (reduced) relation does not define a rooted tree.
That is, because node `s1` has two parent nodes (i.e. `s2` and `s7`).

Note that the semantics of a relation reflects the relation's orientation (i.e.
superordinate-to-subordinate or vice versa). That is, the orientations of the
above relation `R` and the relation of a node tree `T` are not consistent with
each other. That is, `sem(R)` is not consistent with the semantics of a node
tree's relation (i.e. `sem(T) := "parent-of"`). However, `sem(R)` matches the
antonym semantics of a tree `sem(T') := "child-of"`.

* `R' := (S,G')`, and `G' := { (s0,s1), (s1,s2), (s1,s7) }`
* `sem(R') := "parent-sequence-of"` or `"parent-section-of"`

Note that nodes `s2` and `s7` now have the same parent node `s1`.

Note that `R'` does define a tree of nodes/sections. Because of that, sections
`s2` and `s7` can now be referred to as "sibling sections". Moreover, all terms
(ancestor, descendant, etc.) that are defined for a tree of nodes also apply
to a tree of sections.

Note that sibling sections are said to be unrelated with each other, which is
consistent with the relation of a node tree. That is, because there is no edge
(i.e. an explicit relationship) that connects two siblings with each other.
Under the relation of a tree, and although they share the same parent node (i.e.
an implicit relationship), siblings are said to be unrelated with each other.

Note that this statement can not be turned around. That is, unrelated sections
are not necessarily siblings to each other. Which is, because they may have
different parent sections.

* sibling section => unrelated section
* but not vice versa (i.e. not <=>)

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
By default, any sectioning node defines a rooted tree of sections.

That is, because, based on the `subsection-of` relationship, a binary
relation can be defined which itself defines a rooted tree of sections.

**CLARIFICATION**
By default, any sectioning node defines a rooted ordered tree of sections.

That is, because the node order of the node tree defines an order on the set
of all sectioning nodes. Consequently, a node sequence defines the order on
the set of all declared sections.

Note that sibling sections are ordered because a presequent sibling section
will be entered/created/opened before any of its subsequent sibling sections.
In addition to that, any parent section will be entered before any of its
descendant sections. That is, the node order of the node tree carries over
onto the section hierarchy.

**CLARIFICATION**
Similar to parent and descendant nodes, a parent section is understood to be
superordinate to its subordinate subsection. Because of that, a parent section
can be understood to have a higher priority/significance than all of its
subsections.

* (pattern: superordinate -> subordinate entity)
* parent node -> child node
* sectioning node -> declared section
* (parent) section -> subsection
* (parent) section -> content nodes

Note that, due to the section tree being just another specialized tree of nodes,
any parent section is superordinate to its subordinate descendant sections.

**CLARIFICATION**
A section, which is a child section of some other section, can be referred to
as one of the other section's strict (or direct, immediate) subsections. In
contrary to that, a section which is a descendant section, but not a child
section, can be referred to as a loose (or ?implicit, distant?) subsection.

These or similar qualifiers (i.e. strict/direct vs. loose/implicit/distant)
may be used in cases where the relationship between two sections needs to be
clarified. Consequently, similar qualifiers may be used to clarify the
relationship between a parent node and its descendant nodes.

**CLARIFICATION**
The relation of the rooted ordered tree of nodes, in combination with the
definition of sectioning nodes, defines the relationship between sections and
nodes, and the relationship between the sections themselves. Consequently, the
corresponding relations are a matter of consequence and therefore do not have
to be defined explicitly.

```
NxN + SN => NxS, SxN, SxS
```

* `(n1,n2) in NxN` - node `n1` is the parent of `n2`
* `n in SN subset-of N` - node `n` is a sectioning node
* `(n,s) in NxS` - node `n in SN` declares section `s`
* `(s,n) in SxN` - section `s` contains node `n`
* `(s1,s2) in SxS` - section `s1` contains section `s2`

**CLARIFICATION**
The node order of the section tree is defined by the node order of the node
tree. In addition to that, the section tree will be created in the order in
which its sections will be entered during the traversal of the section tree.

That is, because due to the node order of the node tree, all parent sections
will be entered/created/opened before any subsection is entered. In addition
to that, the sectioning nodes of sibling sections are entered according to the
node order of the node tree (i.e. in the sequence in which they appear in the
node sequence, which is based upon the node order of the node tree).

Note that not any tree data structure is suited to represent the tree of
sections. That is, because an AVL tree, for example, will repeatedly trigger
balancing operations, if entries are added in an orderly fashion (e.g. in
ascending order). Consequently, a list-based data structure would be more
appropriate.

<!-- ======================================================================= -->
## a section's parent section

Obviously, there now are two (seemingly) different definitions for the term
"parent section of a section": (1) a section is a parent section to all of its
inner sections, and (2) a section is a parent section of an inner section, if
it is the inner section's parent section in the corresponding tree of sections.

Note that both definitions are not independent from each other. That is,
because all parent sections of a subsection (1) are elements of the rooted path
of sections which begins in the root section and ends in the subsection's parent
section (2).

**CLARIFICATION**
The least significant ancestor section of a section will be referred to as
*the (unique) parent section* of the corresponding subsection.

Note that this parent section is the nearest (i.e. closest according to the
node sequence) open presequent section. Put differently, a section's unique
parent section is the least significant open presequent section which was
declared last, before the corresponding subsection was entered.

Note that this settles the issue of sections having multiple different parent
sections. That is, because any section always has, if the universal section is
included, exactly one unique parent section and may have one or more ancestor
sections.

**CLARIFICATION**
Similar as before, but with regards to sections instead of ordinary nodes,
a subsection can be understood to be strictly related to its unique parent
section and loosely related to all other ancestor sections.

**CLARIFICATION**
A reference to a section's unique parent section can be used to represent
all the parent/ancestor sections of a given subsection. If this practical
representation would not be possible, then each subsection would have to
hold references to all of its ancestor sections, which would otherwise
be required by the formal definitions.

**CLARIFICATION**
A section's unique parent section defines the following,
implementation specific property:

```
Section Section.parentSection
```

**CLARIFICATION**
A section's parent section can be understood to define the location of that
section with regards to the section hierarchy (i.e. its logical location).
