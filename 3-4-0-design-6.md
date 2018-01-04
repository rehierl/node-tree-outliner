
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

Note that this does not imply that an additional sectioning node property
(e.g. rank) can not result in such a characteristic. However, these additional
properties can only be defined if they do not produce any conflict with the
following statements.

**CLARIFICATION**
A subsequent section is said to belong to a presequent section, if the
presequent section still counts as being open when the subsequent sectioning
node is entered.

Note that this indicates that a section's sectioning node and its content
nodes must be strongly connected. It must not be allowed to have a subsequent
sectioning node belong to a presequent section, but not the the content
nodes of the subsequent section. This would otherwise result in conflicting
statements.

**CLARIFICATION**
Two sections have no nodes in common, if the presequent section is closed
before the sectioning node of the subsequent section is entered.

Note that these circumstances are of no interest at this point. The relevant
aspect here is to define the relationship between two sections, if those two
sections have one or more nodes in common.

**CLARIFICATION**
A section that belongs to another section is said to be "an inner section of"
the presequent section. In addition to that, the presequent section is said
to be "the parent section of" the inner section.

Note that the "an inner section of" reference, for now only refers to a section
that belongs to another section. That is, a reference without any additional
meaning. Likewise, the "the parent section of" reference only refers to a
section that is presequent to one of its inner sections.

The actual semantics of these references will be defined below.

**CLARIFICATION**
The parent container of an inner section either is the parent container of its
parent section, or a descendant of the parent section's parent container. Put
differently, the parent container of an inner section is by definition never
an ancestor of the parent section's parent container.

```
              n1
A:        ==========
          n2      n3
B:  ===========
C:  n4 ========
       n5 n6 n7
```

(Nodes `n1` and `n2` represent type-1 sectioning nodes
and `n4` a type-2 sectioning node.)

**CLARIFICATION**
The default scope of an inner section always begins and always ends inside
of, or with the default scope of its parent section.

(1) An inner section always ends with, or inside of its parent section:
That is, because the inner section's parent container never is an ancestor
of the parent section's parent container.

(2) An inner section always begins inside of its parent section:
That is, because the first content node of an inner section always is
located in between the inner section's sectioning node and the end of
the inner section's parent container.

**CLARIFICATION**
The content nodes of an inner section also belong to the parent section. As
such, they must be associated with the inner section and the parent section.

That is, because both sections count as being open for as long as the inner
section is open. Because of that, all the content nodes of an inner section
must also be associated with the inner section's parent section.

Note that this is a purely formal requirement because the definitions treat
all sections as separate entities. Practically, and depending on the exact
structure of sections, it could still be possible to strictly associate any
node with one section only.

**DEFINITION**
An inner section is said to be a sub-section of its parent section.

That is, because any content node of a subsection also belongs to
the corresponding parent section.

Note that this definition is similar to the formal definition of
a "subset": i.e. `(V subset-of W) := ((v in W) for any (v in V))`

<!-- ======================================================================= -->
## derived statements
