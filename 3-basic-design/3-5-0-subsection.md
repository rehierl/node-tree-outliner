
<!-- ======================================================================= -->
# Design - subsection

**CLARIFICATION**
A section is said to be presequent (or predeclared) with regards to another
section, if its sectioning node is presequent to the other section's sectioning
node. Likewise, the other section is said to be subsequent to the presequent
section. In addition to that, and because a sectioning node unconditionally
declares exactly one new section, a section always is presequent or subsequent
to any other section.

Note that these statements do not imply any relationship between any two
sections. The above statements only state which of these sections is declared
first: A presequent section is declared before a subsequent section.

**CLARIFICATION**
The default definitions of sectioning nodes do by themselves not include any
effect on any presequent section. That is, because sectioning nodes are only
defined to declare new sections. This obviously does not include the
characteristic to close any presequent section. Because of that, and so
far, the only option to close a section is by exiting parent containers.

Note that this does not imply that a (to be defined) sectioning node property
can not result in such a characteristic. However, these additional properties
must be consistent with the default definitions described below.

**CLARIFICATION**
Two sections have one or more nodes in common, if nodes exist that are
associated with both sections. This can obviously only be the case, if the
presequent section still counts as being open when the subsequent sectioning
node is entered. If two sections have one or more nodes in common, then both
sections are said to share the corresponding content nodes.

Note that a section's sectioning node and the section's content nodes must be
strongly connected. That is, it must not be allowed to have a subsequent
sectioning node belong to a presequent section, but not the content nodes of
the subsequent section. This would otherwise result in conflicting statements
with regards to the location of the subsequent section.

**CLARIFICATION**
Two sections have no nodes in common, if the presequent section is closed
before the sectioning node of the subsequent section is entered. Two such
sections are said to be unrelated with, or independent from each other.

Note that all sections declared inside of a node tree can be understood to
always be, one way or another, related with each other. After all, they all are
declared inside of the same node tree. However, the focus here is, that there
is no strong (i.e. explicit) relationship between two independent sections.

Note that, in order for two sections to be unrelated with each other, the
sectioning node of the subsequent section *must not belong* to the presequent
section. Consequently, both sections can not share any content nodes.

Note that these circumstances are of no interest at this point. The relevant
aspect here is to define the relationship between two sections, if these two
sections are related with each other.

**CLARIFICATION**
A section, which is subsequent to an open presequent section, is said to belong
to the presequent section. In addition to that, the presequent section is said
to contain the subsequent section. Both sections are said to be related with
each other.

Note that, in order for two sections to be related with each other, the
sectioning node of the subsequent section *must belong* to the presequent
section.

Consequently, related sections are not required to share any content nodes. That
is, because the subsequent sectioning node is a content node of the presequent,
but not a content node of its own section. Also, the subsequent section is not
required to have any content nodes of its own. That is, the subsequent section
may even be empty.

<!-- ======================================================================= -->
## inner section

**CLARIFICATION**
A section that belongs to another section is said to be "an inner section of"
the presequent section. In addition to that, the presequent section is said to
be "a parent section of" the inner section.

Note that a section may be an inner section with regards to multiple parent
sections. That is, because like any other node, a section can be subsequent to
multiple open presequent sections. Consequently, an inner section is related
to all of its parent sections.

Note that allowing multiple parent sections is just a formal approach. The
semantics will be clarified when the relationship between sections is clarified.
For now, the expression "the parent section of" is only used to refer to the
corresponding presequent section with regards to some specific context.

At this point, the "an inner section of" reference only refers to a section
which belongs to one or more other sections. That is, a reference without any
additional meaning. Likewise, the "a/the parent section of" references only
refer to a section which is related to some inner section.

**Memory hook**
Just a visual example:

```
              n1
A:        ==========
          n2      n3
B:  ===========
C:  n4 ========
D:     n5 =====
```

* nodes `n1` and `n2` represent type-1 sectioning nodes.
* nodes `n4` and `n5` represent type-2 sectioning nodes.

**CLARIFICATION**
The parent container of an inner section never is an ancestor
of the parent section's parent container.

That is, because the parent container of an inner section either is the
parent container of the parent section, or a descendant of said container.

**CLARIFICATION**
The default scope of an inner section begins and ends inside of,
or with the default scope of its parent section.

* An inner section always ends with, or inside of its parent section:
  That is, because the inner section's parent container never is an
  ancestor of the parent section's parent container. And, because of
  that, an inner section can not end outside of its parent section.
* An inner section always begins inside of its parent section:
  That is, because the first content node of an inner section always
  is located in between the inner section's sectioning node and the
  exit event of the inner section's parent container.

Put differently:

* No inner section can contain any nodes that do not also belong to its
  parent section. That is, an inner section can not reach past the end of
  its parent section.
* No parent section can end inside of one of its inner sections. That is, a
  parent section either remains to be open when an inner section is closed,
  or both sections end at the same time (i.e. with the same event).

Note that an inner section can not begin with its parent section. That is,
because a sectioning node can only declare a single new section. Consequently,
the inner section's sectioning node will always be entered, after the parent
section was opened.

**CLARIFICATION**
All content nodes of an inner section
are also content nodes of its parent section.

That is, because both sections are open for as long as the inner section
is open. Because of that, all content nodes of an inner section must also
be associated with the inner section's parent section.

Note that this is just a formal requirement. That is, because the definitions
treat all sections as separate entities. For practical reasons, and depending
on the exact nature of the resulting structure of sections, it could still be
allowed, based on implicit associations, to associate each node with one
section only.

<!-- ======================================================================= -->
## subsection

**DEFINITION**
An inner section is a sub-section, or a sub-set, of its parent section.
That is, because a section still counts as a set of nodes.

* `(V subset-of W) := ((v in W) for any (v in V))`
* `(s subsection-of p) := (s subset-of p)`

(Again, all content nodes of an inner section
are also content nodes of its parent section)

Note that, the terms "inner section" and "subsection" are synonymous and still
considered to be independent of any section hierarchy. In addition to that,
the term "parent section" may still refer to one of multiple different open
presequent sections.

**CLARIFICATION**
An inner section (or subsection) is a subsequence of all of its parent sections.

That is, because any section still counts as a subsequence of the tree's node
sequence. In addition to that, all content nodes of a subsection also belong
to its parent section.

**CLARIFICATION**
The intersection of a subsection with its parent section always is identical to
the subsection itself. That is, because all content nodes of a subsection also
belong to its parent section (hint: focus on the content nodes).

* `(A & B), (A and B) := { x : (x in A) and (x in B) }`
* `(s & p) == s`, for any subsection `s` and its parent section `p`

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
At any given point in time, during the traversal of the node tree,
there always are one or more open sections.

That is, because each node in a node tree must be associated with at least one
section. For that to happen, one or more sections must always be open when any
node is entered - even if the only open section left is the universal section.

Note that, when the root node is entered, the universal section is the only
open section. When the root's first child is entered, the universal section
and the root section, a type-1 section, are open. In addition to that, it
must not be allowed to close all of the remaining open sections.

Note that no definition, not even a modified definition,
can close the omnipresent universal section.

**CLARIFICATION**
The section of a subsequent sectioning node
is a subsection to all open presequent sections.

That is, because all presequent sections remain to be open for as long as
the subsection is open. And, because of that, a subsequent section always
is a subsection to all open presequent sections.

Note that this is only intended to change the perspective from a pair of
sections towards a subsequent inner section (aka. subsection) with regards
to all of its presequent and still open parent sections.

**CLARIFICATION**
Any sectioning node always declares a new subsection.

That is, a sectioning node does not declare some abstract and isolated entity.
The section that a sectioning node declares always is a subsection to one or
more open presequent sections.

Note that this, by itself, does not allow to conclude that the structure of
sections is a single tree of sections. The overall structure can technically
still be a list of one or more root sections. That is, if the universal
section is ignored.

**CLARIFICATION**
Any parent section may contain multiple independent subsections. That is, the
subsections of a parent section do not necessarily share any content nodes.

That is, because it is possible that the parent container of a presequent
subsection is exited before a subsequent subsection is entered (e.g. a type-1
sectioning node that is a previous sibling to a some other sectioning node).

Note that all of these independent and intermediate subsections will be ignored
by the following considerations. That is, because the focus is on multiple
sections that are related with each other.

<!-- ======================================================================= -->
## tree of sections

```
... n0 n1 n2 n3 n4 n5 n6 n7 n8 n9 ...
       ========================== s0
          ======================= s1
             ========    ======== s2, s7
```

Select a subsection (e.g. `s2`) and all of its parent sections (e.g. `s0, s1`).

Obviously, all these sections are related with each other. This group of
related sections represents a subset (e.g. `s := { s2, s0, s1 }`) of the
set of known sections.

In addition to that, the sections in such a set of related sections `s` are
ordered. That is, because the set of their sectioning nodes is ordered
according to the node sequence of the tree, which is based upon the tree's
node order. Consequently, and if that node order is taken into account, the
above set of related sections `s` also defines an ordered list of sections
(i.e. `s := [ s0, s1, s2 ]`).

As mentioned above, all sections are subsequences of the tree's node sequence.
And, because of that, any section is a subsequence with regards to all of its
parent sections. That is, `s2` is a subsequence of `s1` and `s0`. In addition
to that, `s1` is also a subsequence of `s0`.

The relationships between the section in the above ordered list of related
sections can be formalized into:

* `(a,b) := (a -> b) := (a subsection-of b)`
* `(a subsection-of b) := (a subsequence-of b) := (a subset-of b)`
* `R := (S,G)`, and `G := { (s2,s1), (s2,s0), (s1,s0) }`

Note that this graph is transitive. Also note, that no rooted tree of nodes
is defined by a relation that is transitive. If such a relation would be
transitive, then there would be nodes that have more than one parent nodes.
The corresponding relation would consequently not define a rooted tree.

* transitive := if `aRb` and `bRc`, then also `aRc`
* example: `(s2,s1)` and `(s1,s0)` and also `(s2,s0)`

Like the inverted graph of a rooted tree, the above graph does itself
not (necessarily) define a rooted tree. That is, because node `s0` has
two parent nodes (i.e. `s1` and `s2`).

If an implicit transitivity is taken into account, the complete graph of
the above example can be defined as follows:

* `G := { (s2,s1), (s1,s0), (s7,s1) }`

As before, this reduced graph does not define a rooted tree. That is,
because node `s1` has two parent nodes (i.e. `s2` and `s7`). In addition
to that, sections `s2` and `s7` are independent from each other.

Note that the semantics `sem(R) := "subsection-of"` of this relation
`R := (S,G)` is not consistent with the semantics of the relation of a node
tree (i.e. `sem(T) := "parent-of"`). However, `sem(R)` matches the antonym
(i.e. inverted) semantics of a tree `sem(T') := "child-of"`.

* `R' := (S,G')`
* `G' := { (s0,s1), (s1,s2), (s1,s7) }`
* `sem(R') := "parent-sequence-of"` or `"parent-section-of"`

Note that nodes `s2` and `s7` both have the same unique parent node `s1`. Both
sections can therefore be seen to be subsections of their parent section `s1`.

Note that `R'` does define a tree of nodes/sections. Because of that, sections
`s2` and `s7` can be understood to be "sibling sections". Moreover, all terms
(ascendant, descendant, etc.) that are defined for a tree of nodes also apply
to such a tree of sections.

Note that sibling sections are said to be unrelated with each other, which is
consistent with the relation of a node tree. That is, because there is no edge
(i.e. an explicit relationship) that connects two nodes with each other. Under
the relation of a tree, and although they share the same parent node (i.e. an
implicit relationship), siblings are said to be unrelated with each other.

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
definition of sectioning nodes, automatically defines the relationship between
sections and nodes, and the relationship between the sections themselves.
Consequently, the corresponding relations are a matter of consequence and
therefore do not have to be defined explicitly.

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
The parent section of a subsection is the closest open presequent section
(i.e. "closest" with regards to the distance between both sectioning nodes
in the tree's node sequence). Put differently, a section's parent section is
the open presequent section which was declared last, before the corresponding
subsequent sectioning node was entered.

<!-- ======================================================================= -->
## TODO

**TODO** -
a subsection is subordinate to its superordinate parent section -
add as a note-like clarification -

**TODO** -
improve the explanation of *ordered* in "rooted ordered tree of sections"? -
the focus of the above statements is more on a rooted path of sections -
needs to take the overall order into account -

**TODO** -
inner section, even if not a direct child subsection -
is it necessary to distinguish (i.e. strict vs. loose)? -

**TODO** -
independent sections are sibling sections -
nope, not always the case -