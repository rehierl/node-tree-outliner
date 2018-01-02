
<!-- ======================================================================= -->
# Design (4) - subsection

**CLARIFICATION**
A section is said to be presequent (or predeclared) with regards to another
section, if its sectioning node is presequent to the other section's sectioning
node. Likewise, the other section is said to be subsequent to a predeclared
section. In addition to that, and because a sectioning node unconditionally
declares exactly one new section, a section always is presequent or subsequent
to another section.

Note that these statements do not imply any relationship between the two
sections involved. The above statements merely state which of these sections
is declared first: A presequent section is declared before a subsequent section.

**CLARIFICATION**
The definition of a sectioning node does by itself not include any effect
on any presequent section. Sectioning nodes are only defined to declare new
sections, which does not include the characteristic to close any predeclared
section. Because of that, and so far, the only option to close a section is
by exiting the section's parent container.

Note that this does not imply that an additional sectioning node property
(e.g. rank) can not result in such a characteristic. However, these additional
properties can only be defined if they are not in conflict with the below
statements.

**CLARIFICATION**
A subsequent section is said to belong to a presequent section, if the
presequent section still counts as being open when the subsequent section's
sectioning node is entered.

Note that two sections have no nodes in common, if the presequent section
is closed before the sectioning node of the subsequent section is entered.
However, these circumstances are of no interest at this point.

The relevant aspect here is to define the relationship between
two different sections, if they have one or more nodes in common.

**CLARIFICATION**
A section that belongs to another section is said to be "an inner section of"
the presequent section. In addition to that, the presequent section is said
to be "the parent section of" the inner section.

Note that the "an inner section of" reference, only refers to a section that
belongs to another section. That is, a reference without any additional meaning.
Likewise, the "the parent section of" reference only refers to a section that
is presequent to one of its inner sections; i.e. a reference without any other
meaning. The actual meaning of these two named references is going to be
clarified below.

The next goal is to unambiguously define the relationship between two sections,
independently of any additional characteristic. That is, if one section is an
inner section to another section.

**CLARIFICATION**
The parent container of an inner section either is the parent container of its
parent section, or one of the parent section's descendants. Put differently,
the parent container of an inner section is by definition never an ancestor of
the parent section's parent container.

```
              n1
A:        ==========
          n2      n3
B:  ===========
    n4 n5 n6 n7
C:     ========
```

(Nodes `n1` and `n2` represent type-1 sectioning nodes.
Node `n4` represents an empty type-2 sectioning node)

**CLARIFICATION**
The default scope of an inner section always begins and always ends with,
or inside of the default scope of its parent section.

**TODO**
If a section is an inner section, then the inner section's first node, and any
other node subsequent to it, must also be associated with the parent section.
