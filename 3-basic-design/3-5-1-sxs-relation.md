
<!-- ======================================================================= -->
# Design - the SxS relation

**CLARIFICATION**
At any given point in time, during the traversal of the node tree,
there always are one or more open sections.

That is, because each node in a node tree must be associated with at least one
section. For that to happen, one or more sections must always be open when a
node is entered - even if the only open section left is the universal section.

Note that, when the root node is entered, the universal section is the only
open section. When the root's first child is entered, the universal section
and the root section, a type-1 section, are open. In addition to that, it
must not be allowed to close all of the remaining open sections.

Note that no definition, not even a modified definition, can close the
theoretical, omnipresent universal section. Because of that, non-default
definitions may at most be allowed to close the root section.

**CLARIFICATION**
The section of a subsequent sectioning node
is a subsection to all open presequent sections.

That is, because all presequent sections remain to be open for as long as
a subsection is open. And, because of that, a subsequent section always is
a subsection to all open presequent sections.

Note that this is only intended to change the perspective from a pair of
sections towards a subsequent inner section (aka. subsection) with regards
to all open presequent sections.

**CLARIFICATION**
Any sectioning node always declares a new subsection.

That is, a sectioning node does not declare some abstract and isolated entity.
The section that a sectioning node declares always is a subsection to one or
more open presequent sections.

Note that this, by itself, does not allow to conclude that the structure of
sections is a single tree of sections. The overall structure can technically
still be a list of one or more section trees. That is, if the universal section
is ignored.

**CLARIFICATION**
Any parent section may contain multiple independent subsections. That is, the
subsections of a parent section do not necessarily share any content nodes.

That is, because it is possible that the parent container of a presequent
subsection is exited before a subsequent subsection is entered (e.g. a type-1
sectioning node that is a previous sibling to some other sectioning node).

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
related sections represents a subset (e.g. `s := { s2, s0, s1 }`) of the
set of known sections.

In addition to that, the sections in such a set of related sections `s` are
ordered. That is, because the set of their sectioning nodes is ordered
according to the node sequence of the tree, which is based upon the tree's
order of nodes. Consequently, and if that node order is taken into account,
the above set of related sections `s` also defines an ordered list of sections
(i.e. `s := [ s0, s1, s2 ]`).

As mentioned above, all sections are subsequences of the tree's node sequence.
And, because of that, any section is a subsequence with regards to all of its
parent sections. That is, `s2` is a subsequence of `s1` and `s0`. In addition
to that, `s1` is a subsequence of `s0`.

The relationships between the section in the above ordered list of related
sections can be formalized into:

* `(a,b) := (a -> b) := (a subsection-of b)`
* `(a subsection-of b) := (a subsequence-of b) := (a subset-of b)`
* `R := (S,G)`, and `G := { (s2,s1), (s2,s0), (s1,s0) }`

Note that this graph is transitive. Also note, that no rooted tree of nodes
is defined by a transitive relation. If such a relation would be transitive,
then there would be nodes that would have more than one parent node. The
corresponding relation would consequently not define a rooted tree.

* transitive := if `aRb` and `bRc`, then also `aRc`
* example: `(s2,s1)` and `(s1,s0)` and also `(s2,s0)`

Like the inverted graph of a rooted tree, the above graph does itself
not (necessarily) define a rooted tree. That is, because node `s0` has
two different parent nodes (i.e. `s1` and `s2`).

If an implicit transitivity is taken into account, the complete graph of
the above example can be defined as follows:

* `G := { (s2,s1), (s1,s0), (s7,s1) }`

As before, this reduced graph does not define a rooted tree. That is,
because node `s1` has two parent nodes (i.e. `s2` and `s7`). In addition
to that, sections `s2` and `s7` are independent from each other.

Note that the semantics `sem(R) := "subsection-of"` of this relation
`R := (S,G)` is not semantically consistent with the semantics of the relation
of a node tree (i.e. `sem(T) := "parent-of"`). However, `sem(R)` matches the
antonym (i.e. inverted) semantics of a tree `sem(T') := "child-of"`.

* `R' := (S,G')`
* `G' := { (s0,s1), (s1,s2), (s1,s7) }`
* `sem(R') := "parent-sequence-of"` or `"parent-section-of"`

Note that sections `s2` and `s7` both have the same unique parent node `s1`.
Both sections can therefore be seen to be subsections to their common parent
section `s1`.

Note that the semantics of a relation reflects the relation's orientation (i.e.
superordinate-to-subordinate or vice versa). That is, the orientations of the
above two relations (i.e. `R` and `T`) are not consistent with each other.

Note that `R'` does define a tree of nodes/sections. Because of that, sections
`s2` and `s7` can be understood to be "sibling sections". Moreover, all terms
(ancestor, descendant, etc.) that are defined for a tree of nodes also apply
to such a tree of sections.

Note that sibling sections are said to be unrelated with each other, which is
consistent with the relation of a node tree. That is, because there is no edge
(i.e. an explicit relationship) that connects two siblings with each other.
Under the relation of a tree, and although they share the same parent node (i.e.
an implicit relationship), siblings are said to be unrelated with each other.

Note that this statement can not be turned around. That is, unrelated sections
are not necessarily siblings to each other. Which is, because they may have
different parent sections.

* (sibling => unrelated), but not (unrelated => sibling)

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
By default, any sectioning node defines a rooted tree of sections. In addition
to that, and due to the node tree's order of nodes, these trees of sections are
rooted ordered trees of sections.

That is, because the node order of the node tree defines an order on the set
of sectioning nodes and therefore an order on the set of all declared sections.
In short: The node order of the node tree carries over onto the set of sections.

Note that this settles the issue of having multiple parent sections. That is,
because any section always has, according to the above relation of sections,
exactly one unique parent section and may have multiple other ancestor sections.

**CLARIFICATION**
The relation of the rooted ordered tree of nodes, in combination with the
definition of sectioning nodes, defines the relationship between sections and
nodes, and the relationship between the sections themselves. Consequently, the
corresponding relations are a matter of consequence and therefore do not have
to be defined explicitly.

```
... x N x ... x N x ...
      x         x
      S x ... x S

... that is ...

NxN + SN => NxS, SxN, SxS
```

* `(n1,n2) in NxN` - node `n1` is the parent of `n2`
* `n in SN subset-of N` - node `n` is a sectioning node
* `(n,s) in NxS` - node `n in SN` declares section `s`
* `(s,n) in SxN` - section `s` contains node `n`
* `(s1,s2) in SxS` - section `s1` contains section `s2`

**CLARIFICATION**
The parent section of a subsection is the closest open presequent section (i.e.
"closest" with regards to the distance between both sectioning nodes in the
tree's node sequence). Put differently, a section's parent section is the open
presequent section which was declared last, before the corresponding subsequent
sectioning node was entered.

```
Section Section.parentSection
```

**CLARIFICATION**
A parent section is understood to be superordinate to its subordinate
subsection. Because of that, a parent section is said to have a higher
priority/significance than its subsections.

(pattern: superordinate -> subordinate entity)

* parent node -> child node
* sectioning node -> declared section -> content nodes
* parent section -> subsection

**CLARIFICATION**
A section, which is a child section of some other section, can be referred to
as one of the other section's strict (or direct, immediate) subsections. In
contrary to that, a section which is a descendant section, but not a child
section, can be referred to as a loose (or ?implicit, distant?) subsection.

That is, these or similar qualifiers (i.e. strict/direct vs. loose/implicit)
may be used in cases where the relationship between two sections needs to be
clarified.
