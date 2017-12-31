
<!-- ======================================================================= -->
# Design (4) - SxS

**CLARIFICATION**
A section is said to be presequent (or predeclared) with regards to another
section, if its sectioning node is presequent to the other section's sectioning
node. Likewise, the other section is said to be subsequent to a predeclared
section.

**CLARIFICATION**
The definition of a sectioning node does by itself not include any effect
on any presequent section. Sectioning nodes are only defined to declare new
sections, which does not include the characteristic to end any predeclared
section. Because of that, and so far, the only option to close a section is
by exiting the section's parent container.

**CLARIFICATION**
A subsequent section belongs to a presequent section, if the presequent section
still counts as being open when the subsequent sectioning node is being exited.

**CLARIFICATION**
A subsequent section begins and ends inside of a presequent section, if (1) the
parent container of the subsequent section is identical to the parent container
of the presequent section, or if (2) the parent container of the subsequent
section is a descendant of the presequent section's parent container.

**CLARIFICATION**
The default scope of a section that belongs to another section always begins
and always ends with (or inside of) the corresponding presequent section.

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

Note that the parent container of such a subsequent section is either the
parent container of the presequent section, or one of its descendant nodes.
Put differently, the parent container of such a subsequent section never is
an ancestor of the presequent section's parent container.
