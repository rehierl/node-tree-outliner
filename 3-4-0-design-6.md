
<!-- ======================================================================= -->
# Design (4) - subsection

**CLARIFICATION**
A section is said to be presequent (or predeclared) with regards to another
section, if its sectioning node is presequent to the other section's sectioning
node. Likewise, the other section is said to be subsequent to a predeclared
section.

Note that these statements do not imply any relationship between the two
sections involved. The above statements merely state which of these sections is
declared first: A presequent section is declared before a subsequent section.

**CLARIFICATION**
The definition of a sectioning node does by itself not include any effect
on any presequent section. Sectioning nodes are only defined to declare new
sections, which does not include the characteristic to close any predeclared
section. Because of that, and so far, the only option to close a section is
by exiting the section's parent container.

Note that this does not imply that an additional sectioning node
property (e.g. rank) can not result in such a characteristic.

The next goal is to define the relationship between two sections
independently and unambiguously of any additional characteristic.

**CLARIFICATION**
A subsequent section is said to belong to a presequent section, if
the presequent section still counts as being open when the subsequent
sectioning node is entered.

**CLARIFICATION**
A section that belongs to another section is said to be "an inner section of"
the presequent section. In addition to that, the presequent section is said to
be "the parent section of" the inner section.

Note that the reference "an inner section of", only refers to a section that
belongs to another section. That is, a reference without any additional meaning.
Likewise, the reference "the parent section of" only refers to a section that
is presequent to a corresponding inner section; i.e. a reference without any
additional meaning. The actual meaning of these two references will be
clarified; see below.

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
