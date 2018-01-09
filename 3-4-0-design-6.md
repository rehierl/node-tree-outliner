
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
node is entered.

Note that a section's sectioning node and the section's content nodes must be
strongly connected. It must not be allowed to have a subsequent sectioning node
belong to a presequent section, but not the content nodes of the subsequent
section. This could otherwise result in conflicting statements with regards to
the subsequent section's location.

**CLARIFICATION**
Two sections have no nodes in common, if the presequent section is closed
before the sectioning node of the subsequent section is entered.

Note that these circumstances are of no interest at this point. The relevant
aspect here is to define the relationship between two sections, if those two
sections have one or more nodes in common.

**CLARIFICATION**
A section, which is subsequent to an open section, is said to belong to the
presequent section. In addition to that, the presequent section is said to
contain the subsequent section.

Note that both sections are not required to have any content nodes in common.
That is, because the subsequent sectioning node is a content node of the
presequent, but not a content node of its own section. Also, the subsequent
section is not required to have any content nodes of its own. That is, the
subsequent section may be empty.

<!-- ======================================================================= -->
## inner section

**CLARIFICATION**
A section that belongs to another section is said to be "an inner section of"
the presequent section. In addition to that, the presequent section is said
to be "the parent section of" the inner section.

At this point, the "an inner section of" reference only refers to a section
which belongs to another section. That is, a reference without any additional
meaning. Likewise, the "the parent section of" reference only refers to a
section which is presequent to one of its inner sections.

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
of the parent section's parent container.

(2) An inner section always begins inside of its parent section:
That is, because the first content node of an inner section always is
located in between the inner section's sectioning node and the end of
the inner section's parent container.

Put differently: No inner section can contain even one content node that does
not also belong to the inner section's parent section.

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
allowed to associate each node with one section only.

**CLARIFICATION**
A parent section, which only contains a single inner section, will always
contain at least one content node that does not belong to the inner section
(i.e. the subsection's sectioning node). Because of that, a parent section
will never be empty - even if all of its inner sections don't have any
content nodes.

<!-- ======================================================================= -->
## subsection

**DEFINITION**
An inner section is said to be a sub-section of its parent section.

Note that this definition is based upon the definition of a subset of values.
That is, because a section can still be defined as a set of nodes.

* `(V subset-of W) := ((v in W) for any (v in V))`
* `(s subsection-of p) := (s subset-of p)`

Note that, by this definition, the terms "inner section" and "subsection" are
synonymous and independent of any section hierarchy. In addition to that, the
term "parent section" may refer to multiple different sections. That is, a
subsection does not necessarily have a single unique parent section.

**CLARIFICATION**
The intersection of a subsection with its parent section is always identical
to the subsection itself. That is, because all content nodes of a subsection
also belong to its parent section.

* `(A & B), (A and B) := { x : (x in A) and (x in B) }`
* `(s & p) == s`, for any subset `s` and a parent set `p`

**CLARIFICATION**
A subsection is a subsequence of its parent section.

That is, because any section is a subsequence of the tree's node sequence. In
addition to that, all content nodes of a subsection also belong to its parent
section.

**CLARIFICATION**
Any parent section may contain multiple subsections that are independent from
each other. That is, the subsections of a parent section don't necessarily have
any nodes in common.

**CLARIFICATION**
The section of a subsequent sectioning node always is a subsection of all
presequent and still open sections.

That is, because any node must belong to at least one section. In addition
to that, a sectioning node does not belong to the section it declares.

Put differently: Any section always is a subsection to some parent section,
even if the only available parent section is the universal section.

Note that this is only a clarification of what a sectioning node does:
A sectioning node declares a new subsection (i.e. not just some section).

Note that this, by itself, does not clarify that the structure of sections
must be a tree of sections. An outline can technically still be a list of
one or more sections. What exactly the structure of sections is, still needs
to be determined.

**TODO** -
issue - list of sections - elevate a t2 sectioning node to the same level a t1
sectioning node has - also - the nodes of a t1 section are all descendants of
the t1 sectioning node

<!-- ======================================================================= -->
## section hierarchy

**CLARIFICATION**
Any section can be a subsection of multiple parent sections. That is,
because a section can be subsequent to one or more open sections.

<!-- ======================================================================= -->
## derived statements

**TODO** -
define "parent section of a node"
