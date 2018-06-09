
<!-- ======================================================================= -->
# Design - subsection

**CLARIFICATION**
A section is said to be presequent (or predeclared) with regards to another
section, if its sectioning node is presequent to the other section's sectioning
node. Likewise, the other section is said to be subsequent to the presequent
section.

Note that these statements do not imply any structural relationship between
two sections. The above statements merely state which of these sections is
declared/entered first. That is, a presequent section is declared before a
subsequent section.

**CLARIFICATION**
A section always is presequent or subsequent to another section
and insequent to itself.

That is, because any sectioning node unconditionally declares exactly one new
section. And because there is a 1:1 relationship between the set of sections
and the set of sectioning nodes, the order introduced above is total. That is,
for any two sections it can be determined which of those is presequent to the
other one.

**CLARIFICATION**
The default definitions of sectioning nodes (so far) do not include any effect
on any presequent section. That is, because sectioning nodes are only defined
to declare/open new sections. This obviously does not include the characteristic
to close any presequent section. The only event that can result in the closure
of a section therefore is the exit event of its parent container.

Note that this does not imply that a (to be defined) sectioning node property
can not result in such a characteristic. However, these additional properties
must not break consistency with the default definitions described below.

Note that the formal definitions treat any section as a separate entity. As
such, no section is defined to have an effect on another section. This is
not supposed to imply, that a section can not have an implicit relationship
with another section.

**CLARIFICATION**
Two sections have one or more nodes in common, if nodes exist that are
associated with both sections. This can obviously only be the case, if the
presequent section still counts as being open when the subsequent sectioning
node is entered. If two sections have one or more nodes in common, then both
sections are said to share the corresponding content nodes.

Note that a section's sectioning node and the section's content nodes must be
strongly connected. That is, it must not be possible to end up with a subsequent
sectioning node belonging to a presequent section, but not the content nodes of
the subsequent section. This would otherwise result in conflicting statements
with regards to the logical location of the subsequent section.

**CLARIFICATION**
Two sections have no nodes in common, if the presequent section is closed
before the sectioning node of the subsequent section is entered. Two such
sections are said to be unrelated with, or independent from one another.

Note that all sections declared inside of the same node tree can be understood
to always be, one way or another, related with each other. After all, they all
are declared inside of the same node tree. However, the focus here is, that
there is no strong (i.e. explicit) relationship between two such sections.

Note that, in order for two sections to be unrelated with each other, the
sectioning node of the subsequent section *must not belong* to the presequent
section. Consequently, both sections can not share any content nodes.

Note that these circumstances are of no interest at this point. The focus here
is to define the relationship between two sections, if these are related with
each other.

**CLARIFICATION**
A section, which is subsequent to an open presequent section, is said to belong
to that presequent section. In addition to that, the presequent section is said
to contain the subsequent section. Both sections are therefore said to be
related with each other.

Note that, in order for two sections to be related with each other, the
sectioning node of the subsequent section *must belong* to the presequent
section.

Note that related sections are not required to share any content nodes. That
is, because the subsequent sectioning node is a content node of the presequent,
but not a content node of its own section. Also, the subsequent section is not
required to have any content nodes of its own - that section may be empty.

<!-- ======================================================================= -->
## inner section

**CLARIFICATION**
A section that belongs to another section is said to be "an inner section of"
the presequent section. In addition to that, the presequent section is said
to be "a parent section of" the inner section.

Note that a section may be an inner section to multiple parent sections. That
is, because like any other node, a section can be subsequent to multiple open
presequent sections. Consequently, an inner section is said to be related to
all these open presequent sections.

Note that allowing multiple parent sections is merely a formal approach. The
semantics will be clarified when the relationship between sections is clarified.
For now, the expression "the parent section of" is only used in a given context
to refer to a presequent section with regards to another subsequent section.

At this point, the "an inner section of" reference only refers to a section
which belongs to one or more other sections. That is, a linguistic reference
without any additional meaning. Likewise, the "a/the parent section of"
references only refer to a section which has one or more inner sections.

**A visual example**

```
            n1
A:      ==========
        n2      n3
B:  ==========
C:  n4 -------
D:     n5 ----
```

* nodes `n1` and `n2` represent type-1 sectioning nodes.
* nodes `n4` and `n5` represent type-2 sectioning nodes.

**CLARIFICATION**
The parent container of an inner section either is identical to the
parent container of its parent section, or a descendant of that container.

Put differently, the parent container of an inner section
*never is* an ancestor of its parent section's parent container.

That is, because ...

* the parent section is still open when the inner section's sectioning node
  is entered. In addition to that, the inner section's sectioning node is
  not defined to close the parent section. Consequently, the inner section's
  sectioning node is located inside of the parent section's default scope.
* Case 1 (the parent section is a type-1 section): The inner section's
  sectioning node always is a descendant of the parent section's sectioning
  node. Because of that, the parent container of the inner section either
  is identical to the parent section's parent container (inner type-2), or
  a descendant of said container (inner type-1 or type-2).
* Case 2 (the parent section is a type-2 section): The inner section's
  sectioning node either is a sibling of the parent section's sectioning
  node, or a descendant of such a sibling. Because of that, the parent
  container of the inner section either is identical to the parent section's
  parent container (inner type-2), or a descendant of said container (inner
  type-1 or type-2).

Note that two sections may have identical parent containers, if (and only if)
the subsequent section is a type-2 section. In all other cases, the inner
section's parent container is always a descendant of the parent section's
parent container.

**CLARIFICATION**
The default scope of an inner section begins and ends inside of, or with the
default scope of its parent section. Because of that, a parent section remains
to be open for as long as one of its inner sections is still open.

* An inner section always ends with, or inside of its parent section:
  That is, because the inner section's parent container never is an
  ancestor of the parent section's parent container. And, because of
  that, an inner section can not end outside of its parent section.
  That is, an inner section never ends with a node that does not also
  belong to the inner section's parent section.
* An inner section always begins inside of its parent section:
  That is, because the first content node of an inner section always
  is located in between the inner section's sectioning node and the
  exit event of the inner section's parent container.

Put differently:

* An section can not contain any node that does not also belong to its parent
  section. That is, an inner section can not reach out of its parent section.
* A parent section can not end inside of one of its inner sections. That is,
  a parent section either remains to be open when an inner section is closed,
  or both sections end at the same time (i.e. with the same event).

**CLARIFICATION**
All content nodes of an inner section are
also content nodes of its parent section.

That is, because both sections are open for as long as the inner section
is open. Consequently, all content nodes of an inner section must also
be associated with the inner section's parent section.

Note that this is just a formal requirement. That is, because the definitions
treat all sections as separate entities. For practical reasons, based on
implicit associations and depending on the exact nature of the resulting
structure of sections, it could still be allowed to associate each node with
one section only.

**CLARIFICATION**
The first content node of a parent section never is a content node of one of
its inner sections. Put differently, all non-empty sections have different
(i.e. unique) first content nodes.

That is, because a parent section must be opened first. After that, the
sectioning node of its first inner section can be entered and associated.
Which is, because no sectioning node belongs to its own section. Finally,
the inner section is opened next.

**CLARIFICATION**
A parent section always has more content nodes than any of its inner sections.

That is, because for each inner section, the parent section contains at least
the inner section's sectioning node. Which is, because no sectioning node
belongs to its own section.

* content node of an inner section => content node of a parent section
* but not vice versa (i.e. not <=>)

This means that, if a node is a content node of an inner section, then that
node is also a content node of the inner section's parent section. (Note that
an inner section always has a parent section. It would otherwise be no inner
section). However, this does *not* mean that, if a node is a content node of a
parent section, then that node is also a content node of one of the parent
section's inner sections. (Note that this applies even if that parent section
had one or more inner sections).

**CLARIFICATION**
A section can not be a parent section, or an inner section to itself.
The structure of sections therefore is acyclic.

Because all non-empty sections have different first content nodes, an inner
section can not begin with its parent section. And, because of that, a section
can not be an inner section to itself. Consequently, the structure of sections
has no loops and/or cycles (i.e. acyclic).

Note that one could still open Pandora's box, if one would associate a parent
container with an inner section while exiting that parent container (hint: due
to implicit associations).

<!-- ======================================================================= -->
## subsection

**DEFINITION**
An inner section is a sub-section, or a sub-set, of its parent section.

* `(V subset-of W) := ((v in W) for any (v in V))`
* `(s subsection-of p) := (s subset-of p)`

That is, because a section still counts as a set of nodes. In addition to
that, all content nodes of an inner section are also content nodes of its
parent section.

Note that, the terms "inner section" and "subsection" are therefore synonymous.
Both terms however are still considered to be independent of any hierarchy.
That is, because both are defined with regards to two related sections. In
addition to that, the term "parent section" may still refer to one of multiple
different open presequent sections.

**CLARIFICATION**
An inner section (or subsection) is a subsequence to all of its parent sections.

That is, because any section still counts as a subsequence of the tree's node
sequence. In addition to that, all content nodes of a subsection also belong
to its parent section.

**CLARIFICATION**
The intersection of a subsection with its parent section always is identical
to the subsection itself. That is, because all content nodes of a subsection
also belong to its parent section (hint: focus on the content nodes).

* `(A & B), (A and B) := { x : (x in A) and (x in B) }`
* `(s & p) == s`, for any subsection `s` and its parent section `p`

<!-- ======================================================================= -->
## derived statements

Note that the afore mentioned considerations all are
with regards to the default scopes of the involved sections.

**CLARIFICATION**
No node can ever be allowed to close a parent section from within one of the
parent section's inner sections. That is, without closing all of the parent
section's inner sections at the same time.

Closing a parent section inside of one of its inner sections would consequently
define all those nodes, that are subsequent to the parent section's close event
and presequent to the inner section's close event, to not belong to the parent
section (although they would still belong to the corresponding "subsection").
And, because of that, the definition of the term "subsection" no longer applies
as that "subsection" would then contain nodes which the "parent section" would
not contain. As a result, such an inner section is not a subsection to that
parent section, it would be something else instead. That is, their relationship
would change considerably.

Note that a subset is not a subset, if it contains even one element that does
not also belong to its parent set. Put differently, a subset is not a subset,
if there is no guarantee that all elements of the subset are also elements of
its parent set. That is, it must be guaranteed that such conditions never occur.

**CLARIFICATION**
A section never is a subsection to itself.

Note that the formal definition of the term "subsection" allows to state that
a section is also a subsection to itself. In contrary to that, a section can
technically not be a subsection to itself. That is, because a sectioning node
does not belong to its own section. And, because of that, a parent section
can never be a subsection to itself.

Note that a section is for the same reason technically a "strict subset" of its
parent section. That is, because a parent section always has more content nodes
than any of its subsections.

**CLARIFICATION**
A sectioning node (type-1 or type-2), which is a subsequent (or next) sibling
of a type-1 sectioning node, can never declare a subsection to that presequent
type-1 section.

That is, because the presequent section will be closed (due to its parent
container) before the subsequent sectioning node can even be entered.
Consequently, both sections can not share any content nodes. And, because
of that, the definition of the terms "inner section" and "subsection" do
not apply.

Note that the subsequent section can also not be redefined (e.g. via a close
modifier) to be an inner section of the already closed presequent section. Any
such definition would (seemingly) produce a conflict, as both sections are by
structural relationship independent from each other (seemingly, as all such
modifiers are always understood to be with regards to open presequent sections,
never with regards to closed presequent sections).
