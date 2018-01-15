
<!-- ======================================================================= -->
# Design (6) - conclusions

<!-- ======================================================================= -->
## implementation specific

**CLARIFiCATION**
Because of that, an implementation does not have to always keep references to
all open sections at hand. That is, because an algorithm only needs to know
what the parent section of the next subsequent node is. 

**CLARIFICATION**

are being entered and (2) the section's default scope ends with the first
exit event of a presequent (i.e. with regards to the first node) and
unassociated node.

Note that the latter aspect already is
a hint towards how it has to be implemented.

<!-- ======================================================================= -->
## sectioning nodes (1)

**CLARIFICATION**
A sectioning node does not belong to its own section.



**TODO** -
make sure that a parent section always has at least one content node -
i.e. no parent section can be mistakenly be understood to be empty -
a section's first node always is associated with the declared section -
never with one of its subsections

<!-- ======================================================================= -->
## sectioning nodes (2)

**CLARIFICATION**
A sectioning node does not belong to its own section.

**TODO** -
don't associate sectioning nodes with the sections they declare -
`Section Node.parentSection` property would be inconsistent -
requires hierarchy of sections

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The parent section of a node's parent section is identical
to the parent section of the corresponding sectioning node.

```
section = node.parentSection
sectioningNode = section.sectioningNode
(section.parentSection === sectioningNode.parentSection)
```

**CLARIFICATION**
A node sequence of length `N` can declare no more than `N` sections.
That is, because each sectioning node always declares a single section only.

**DEFINITION**
The rank of a section is the number of its ancestor sections.

Note that the universal section is always included. That is, the root section
has rank 1 and the universal section has rank 0. Note also that this is similar
to a node's node level within a tree of nodes. That is, the root node has node
level 1.

**TODO** -
issue - list of sections - elevate a t2 sectioning node to the same level a t1
sectioning node has - also - the nodes of a t1 section are all descendants of
the t1 sectioning node

`[section, A, section, B, /section, C, /section]`
