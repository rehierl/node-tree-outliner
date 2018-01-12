
<!-- ======================================================================= -->
# Design (4) - subsection

**CLARIFICATION**
A section is said to be presequent (or predeclared) with regards to another
section, if its sectioning node is presequent to the other section's sectioning
node. Likewise, the other section is said to be subsequent to the predeclared
section. In addition to that, and because a sectioning node unconditionally
declares exactly one new section, a section always is presequent or subsequent
to any other section.

Note that these statements do not imply any relationship between any two
sections. The above statements only state which of these sections is declared
first: A presequent section is declared before a subsequent section.

**CLARIFICATION**
The definition of a sectioning node does by itself not include any effect
on any presequent section. Sectioning nodes are only defined to declare new
sections, which obviously does not include the characteristic to close any
predeclared section. Because of that, and so far, the only option to close
a section is by exiting the section's parent container.

Note that this does not imply that a (to be defined) sectioning node property
can not result in such a characteristic. However, these additional properties
must be consistent with the below statements.

**CLARIFICATION**
Two sections have one or more nodes in common, if nodes exist that are
associated with both sections. This can obviously only be the case, if the
presequent section still counts as being open when the subsequent sectioning
node is entered. If two sections have one or more nodes in common, then both
sections are said to share the corresponding nodes.

Note that a section's sectioning node and the section's content nodes must be
strongly connected. It must not be allowed to have a subsequent sectioning node
belong to a presequent section, but not the content nodes of the subsequent
section. This could otherwise result in conflicting statements with regards to
the subsequent section's location.

**CLARIFICATION**
Two sections have no nodes in common, if the presequent section is closed
before the sectioning node of the subsequent section is entered. Two such
sections are said to be unrelated with, or independent from each other.

Note that, in order for two sections to be unrelated with each other, the
sectioning node of the subsequent section *must not belong* to the presequent
section. Consequently, both sections can not share any content nodes.

Note that these circumstances are of no interest at this point. The relevant
aspect here is to define the relationship between two sections, if those two
sections are related with each other.

**CLARIFICATION**
A section, which is subsequent to a section that is still open, is said to
belong to the presequent section. In addition to that, the presequent section
is said to contain the subsequent section. These kind of sections are said to
be related with each other.

Note that, in order for two sections to be related, the sectioning node of the
subsequent section *must belong* to the presequent section.

Consequently, related sections are not required to share any content nodes. That
is, because the subsequent sectioning node is a content node of the presequent,
but not a content node of its own section. Also, the subsequent section is not
required to have any content nodes of its own. That is, the subsequent section
may even be empty.

Note that, under this perspective, sibling sections are seen to be unrelated
with each other. This is somewhat consistent with the relation of a node tree,
as there is no edge (i.e. an explicit relationship) that connects two nodes
with each other. That is, under the relation of a tree of nodes, siblings are
unrelated. However, siblings still have the same parent node (i.e. an implicit
relationship).

<!-- ======================================================================= -->
## inner section

**CLARIFICATION**
A section that belongs to another section is said to be "an inner section of"
the presequent section. In addition to that, the presequent section is said to
be "a parent section of" the inner section. Consequently, an inner section is
said to be related with all of its parent sections.

Note that a section can be an inner section with regards to multiple different
parent sections. That is, because it can be subsequent to multiple different
and still open presequent sections.

Note that allowing multiple parent sections is just a formal approach. The
semantics will be clarified when the relationship between sections is clarified.
For now, the expression "the parent section of" is only used to reference the
corresponding presequent section.

At this point, the "an inner section of" reference only refers to a section
which belongs to another section. That is, a reference without any additional
meaning. Likewise, the "a/the parent section of" references only refer to a
section which is presequent to one of its inner sections.

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

Nodes `n1` and `n2` represent type-1 sectioning nodes.
Nodes `n4` and `n5` represent type-2 sectioning nodes.

**CLARIFICATION**
The parent container of an inner section
never is an ancestor of the parent section's parent container.

That is, because the parent container of an inner section either is the
parent container of its parent section, or a descendant of said container.

**TODO** -
explain in detail?

**CLARIFICATION**
The default scope of an inner section begins and ends inside of,
or with the default scope of its parent section.

* An inner section always ends with, or inside of its parent section:
  That is, because the inner section's parent container never is an
  ancestor of the parent section's parent container. Because of that,
  an inner section can not end outside of its parent section.
* An inner section always begins inside of its parent section:
  That is, because the first content node of an inner section always
  is located in between the inner section's sectioning node and the
  end of the inner section's parent container.

Put differently:

* No inner section contains content nodes that do not also belong to its parent
  section. That is, an inner section does not reach past its parent section.
* No parent section can end inside of one of its inner sections. That is, a
  parent section either remains to be open when an inner section is closed,
  or both sections end with the same event.

Note that an inner section can not begin with its parent section. That is,
because a sectioning node does not belong to its section. Consequently, there
always is at least the inner section's sectioning node in between both events.

**CLARIFICATION**
All content nodes of an inner section
are also content nodes of its parent section.

That is, because both sections count as being open for as long as the inner
section is open. Because of that, all content nodes of an inner section must
also be associated with the inner section's parent section.

Note that this is just a formal requirement. That is, because the definitions
treat all sections as separate entities. For practical reasons, and depending
on the exact nature of the resulting structure of sections, it could still be
allowed, due to implied associations, to associate each node with one section
only.

**CLARIFICATION**
A parent section always has at least one content node.

That is, because a parent section can only be a parent section, if it contains
at least one inner section. As such, a parent section always contains at least
one or more content nodes (i.e. the sectioning nodes of its inner sections).
Because of that, a parent section can never be empty - even if all of its
inner sections don't have any content nodes themselves (i.e. are empty).

<!-- ======================================================================= -->
## subsection

**DEFINITION**
An inner section is a sub-section, or a sub-set, of its parent section. That is,
because a section is still also a set of nodes.

* `(V subset-of W) := ((v in W) for any (v in V))`
* `(s subsection-of p) := (s subset-of p)`

Note that, by this definition, the terms "inner section" and "subsection" are
synonymous and independent of any section hierarchy. In addition to that, the
term "parent section" may still refer to one of multiple different sections.

**CLARIFICATION**
The intersection of a subsection with its parent section is always identical to
the subsection itself. That is, because all content nodes of a subsection also
belong to its parent section. The point here is to concentrate on the content
nodes of a section.

* `(A & B), (A and B) := { x : (x in A) and (x in B) }`
* `(s & p) == s`, for any subsection `s` and a parent section `p`

**CLARIFICATION**
An inner section (or subsection) is a subsequence of its parent sections.

That is, because any section still is a subsequence of the tree's node sequence.
In addition to that, all content nodes of a subsection also belong to its parent
section.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The section of a subsequent sectioning node
is a subsection to all open presequent sections.

That is, because all these presequent sections remain to be open for as long
as the subsection is open. And, because of that, a subsequent section always
is a subsection to all open presequent sections.

Note that this is merely intended to change the perspective from a pair of
sections towards a subsequent inner section (aka. subsection) with regards
to all of its presequent and still open parent sections.

**CLARIFICATION**
Any parent section may contain multiple independent subsections. That is, the
subsections of a parent section do not necessarily share any content nodes.

That is, because it is possible that the parent container of a presequent
subsection is exited before a subsequent subsection is entered (e.g. a type-1
sectioning node that is presequent to a type-1, or a type-2 sectioning node).

Note that all of these independent and intermediate subsections will be ignored.
That is, because the focus now is on multiple related open sections.

**CLARIFICATION**
At any given point in time, during the traversal of the node tree, there always
are one or more open sections.

That is, because each node in a node tree must be associated with at least one
section. For that to happen, one or more sections must always be open when a
nodes is entered - even if the only open section left is the universal section.

Note that, when the root node is entered, the universal section is open. When
the root's first child is entered, the universal section and the root section,
a type-1 section, is open. In addition to that, it must not be allowed to close
all of the remaining open sections. The latter is guaranteed by the concept of
default scopes, but not by possible sectioning node properties.

**CLARIFICATION**
A sectioning node always declares a new subsection. That is, a sectioning node
does not declare some abstract and isolated entity.

Note that this, by itself, does not allow to conclude that the structure of
sections is a single tree of sections. That structure can technically still be
a list of one or more sections. That is, if the universal section is ignored.
What exactly a tree's structure of sections is, still needs to be determined.

<!-- ======================================================================= -->
## tree of sections

```
... n0 n1 n2 n3 n4 n5 n6 n7 n8 n9 ...
       ========================== s0
          ======================= s1
             ========    ======== s2, s7
```

Select a subsection (e.g. `s2`) and all of its parent sections (e.g. `s0, s1`).
Obviously, all these sections are related with each other. This group of related
sections represents a subset (e.g. `s := { s2, s0, s1 }`) of the set of known
sections.

In addition to that, the sections in the above set of related sections `s` are
ordered. That is, because the set of sectioning nodes is ordered according to
the node order of the tree. Consequently, and if that node order is taken into
account, the above set of related sections `s` is also an ordered list of
sections (i.e. `s := [ s0, s1, s2 ]`).

As mentioned above, all sections are subsequences of the tree's node sequence.
And, because of that, any section is a subsequence with regards to all of its
parent sequences. That is, `s2` is a subsequence of `s1` and `s2` is also a
subsequence of `s0`. In addition to that, `s1` is a subsequence of `s0`.

The relationships between the section in the above ordered list of related
sections can be formalized into:

* `(a -> b) := (a subsection-of b) := (a subsequence-of b)`
* `G := { (s2 -> s1), (s2 -> s0), (s1 -> s0) }`
* `G := { (s2,s1), (s2,s0), (s1,s0) }`

Note that this graph is transitive:

* transitive := if `aRb` and `bRc`, then also `aRc`
* from the example: `(s2,s1)` and `(s1,s0)` and also `(s2,s0)`

Note that, like the inverted graph of a rooted tree, the above graph does not
(necessarily) define a rooted tree. That is, because node `s0` has two parent
nodes (i.e. `s1` and `s2`).

If an implicit transitivity is taken into account, the complete graph for the
above example can be defined as follows:

* `G := { (s2,s1), (s1,s0), (s7,s1) }`

Note that this reduced graph does not define a rooted tree. That is, because
node `s1` has two parent nodes (i.e. `s2` and `s7`). Also note that sections
`s2` and `s7` are independent from each other.

In addition to that, the semantics `sem(R) := "subsection-of"` of this relation
`R := (S,G)` is not consistent with the semantics of the relation of a node tree
(i.e. `sem(T) := "parent-of"`). However, `sem(R)` matches the antonym (i.e.
inverted) semantics of a tree `sem(T') := "child-of"`.

* `R' := (S,G')`
* `G' := { (s0,s1), (s1,s2), (s1,s7) }`
* `sem(R') := "parent-sequence-of" or "parent-section-of"`

Note that nodes `s2` and `s7` now have the same unique parent node `s1`. These
sections can therefore be seen to be child sections of their common parent
section `s1`. Because of that, both sections are said to be "sibling sections".
Hence, all terms (ascendant, descendant, etc.) defined for a tree of nodes also
apply to a tree of sections.

**CLARIFICATION**
By default, any sectioning node defines a rooted tree of sections. In addition
to that, and because of the node tree's order of nodes, these trees of sections
are rooted and ordered trees of sections.

Note that this settles the issue of having multiple parent sections: A section
always has exactly one unique parent section and may have multiple ancestor
sections.

**CLARIFICATION**
The definition of sectioning nodes defines the relationship between nodes and
sections, and the relationship between all sections.

```
NxN + SN => NxS + SxS
```

* `NxN` represents the relation of nodes
* `SN` represents the definitions of sectioning nodes
* `NxS` represents the relationship between nodes and sections
* `SxS` represents the relationship between all sections

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
That is, because each section always has exactly one direct/immediate parent
section. It simply is not possible for a section to have multiple parent
sections.

**CLARIFICATION**
A node sequence of length `N` can declare no more than `N` sections. That is,
because each sectioning node always declares a single section only.

**TODO** -
associate each node with one section only

**TODO** -
issue - list of sections - elevate a t2 sectioning node to the same level a t1
sectioning node has - also - the nodes of a t1 section are all descendants of
the t1 sectioning node
