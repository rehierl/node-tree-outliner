
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
sections. The above statements merely state which of these sections is
declared first: A presequent section is declared before a subsequent section.

**CLARIFICATION**
The definition of a sectioning node does by itself not include any effect
on any presequent section. Sectioning nodes are only defined to declare new
sections, which obviously does not include the characteristic to close any
predeclared section. Because of that, and so far, the only option to close
a section is by exiting the section's parent container.

Note that this does not imply that a (to be defined) sectioning node property
can not result in such a characteristic. However, these additional properties
must be consistent with the following statements.

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
before the sectioning node of the subsequent section is entered. These kind
of sections are said to be unrelated with, or independent from each other.

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

Note that, in order for two sections to be related with each other, the
sectioning node of the subsequent section *must belong* to the presequent
section.

Consequently, related sections are not required to share any content nodes. That
is, because the subsequent sectioning node is a content node of the presequent,
but not a content node of its own section. Also, the subsequent section is not
required to have any content nodes of its own. That is, the subsequent section
may still be empty.

Note that, under this perspective, sibling sections are seen to be unrelated
with each other. This is somewhat consistent with the relation of a node tree,
as there is no edge (i.e. an explicit relationship) that connects two nodes
with each other. That is, under a tree's relation, siblings are unrelated with
each other. However, siblings still have the same parent node (i.e. an implicit
relationship).

**TODO** -
clarify sibling sections

<!-- ======================================================================= -->
## inner section

**CLARIFICATION**
A section that belongs to another section is said to be "an inner section of"
the presequent section. In addition to that, the presequent section is said
to be "a parent section of" the inner section. Consequently, an inner section
is said to be related with its parent sections.

Note that a section can be an inner section with regards to multiple different
parent sections, just as it can be subsequent to multiple different and still
open presequent sections.

At this point, the "an inner section of" reference only refers to a section
which belongs to another section. That is, a reference without any additional
meaning. Likewise, the "a parent section of" reference only refers to a section
which is presequent to one of its inner sections.

Note that, at the moment, it might be confusing that a section may have multiple
parent sections. So for now, "the parent section of" will be used instead to
refer to the corresponding presequent section.

**Memory hook**
Just an example:

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
The parent container of an inner section either is the parent container of
its parent section, or a descendant of the parent section's parent container.

Put differently, the parent container of an inner section never is an ancestor
of the parent section's parent container.

**TODO** -
explain in detail?

**CLARIFICATION**
The default scope of an inner section always begins and always
ends inside of, or with the default scope of its parent section.

(1) An inner section always ends with, or inside of its parent section:
That is, because the inner section's parent container never is an ancestor
of the parent section's parent container. Because of that, an inner section
can not end outside of its parent section.

(2) An inner section always begins inside of its parent section:
That is, because the first content node of an inner section always is
located in between the inner section's sectioning node and the end of
the inner section's parent container.

Put differently: No inner section can contain even one content node that does
not also belong to the corresponding parent section.

Put differently: No parent section can end inside of one of its inner sections.
That is, a parent section either remains to be open when an inner section is
closed, or both sections end with the same event.

**CLARIFICATION**
All content nodes of an inner section are also content nodes of the inner
section's parent section.

That is, because both sections count as being open for as long as the inner
section is open. Because of that, all content nodes of an inner section must
also be associated with the inner section's parent section.

**TODO** -
However, this is only a formal requirement. That is, because the definitions
treat all sections as separate entities. For practical reasons, and depending
on the exact nature of the resulting structure of sections, it could still be
allowed, due to implied associations, to associate each node with one section
only.

**CLARIFICATION**
A parent section can only be a parent section, if it contains at least one
inner section. As such, a parent section always contains at least one or more
content nodes (i.e. the sectioning nodes of its inner sections). Because of
that, a parent section can never be empty - even if all of its inner sections
don't have any content nodes themselves (i.e. are empty).

<!-- ======================================================================= -->
## subsection

**DEFINITION**
An inner section is said to be a sub-section of its parent section.

Note that this definition is based upon the definition of a subset of values.
That is, because a section can still be seen as a set of nodes.

* `(V subset-of W) := ((v in W) for any (v in V))`
* `(s subsection-of p) := (s subset-of p)`

Note that, by this definition, the terms "inner section" and "subsection" are
synonymous and independent of any section hierarchy. In addition to that, the
term "parent section" may still refer to one of multiple different sections.
That is, a subsection is not yet defined to have one unique parent section.

**CLARIFICATION**
The intersection of a subsection with its parent section is always identical to
the subsection itself. That is, because all content nodes of a subsection also
belong to its parent section.

* `(A & B), (A and B) := { x : (x in A) and (x in B) }`
* `(s & p) == s`, for any subsection `s` and a parent section `p`

**CLARIFICATION**
A subsection is a subsequence of its parent section.

That is, because a section can still be seen as a subsequence of the tree's node
sequence. In addition to that, all content nodes of a subsection also belong to
its parent section.

**CLARIFICATION**
Any parent section may contain multiple subsections that are independent from
each other. That is, the subsections of a parent section are not required to
share any content nodes.

For now, these kind of independent and intermediate subsections will be ignored.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The section of a subsequent sectioning node is a subsection to all presequent
and still open sections.

That is, because a subsequent section does, by default, not close any presequent
section. Consequently, all those sections count as being open for as long as the
subsection is open.

Note that this merely changes the perspective from one pair of sections towards
a subsection with regards to multiple presequent parent sections.

**CLARIFICATION**
There always is at least one open section.

Note that this is only a clarification of what a sectioning node does:
A sectioning node declares a new subsection (i.e. not just some section).

**CLARIFICATION**
Any section always is a subsection to one or more presequent sections.
That is, even if the only available section is the universal section.

Note that this, by itself, does not clarify that the structure of sections
is a tree of sections. That structure can technically still be a list of one
or more sections. What exactly the structure of sections is, still needs to
be determined.

Yes, 

**TODO** -
issue - list of sections - elevate a t2 sectioning node to the same level a t1
sectioning node has - also - the nodes of a t1 section are all descendants of
the t1 sectioning node

<!-- ======================================================================= -->
## section hierarchy

**CLARIFICATION**
Any section can be a subsection of multiple parent sections. That is,
because a section can be subsequent to one or more open sections.

Note that this is independent of those cases in which there are one or more
other sections in between two involved sections. That is, an independent section
can be subsequent to a parent section and presequent to another subsection.

<!-- ======================================================================= -->
## derived statements

**TODO** -
define "parent section of a node"
