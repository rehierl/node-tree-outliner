
<!-- ======================================================================= -->
# Objects and variables

The following content is intended to provide
an overview of global variables and object properties.

<!-- ======================================================================= -->
## Global scope

```
Global begin
  - the current node being entered/exited
  Node currentNode

  - the node level of currentNode
  - maintained by the tree traversal algorithm
  int currentNodeLevel

  - all currently open sections
  - the bottom section is the root section
  - the top-most section is the current section
  - not needed -> currentSection.parentSection{+}
  Stack<Section> openSections

  - a reference to the current section
  - used to associate all the nodes
  - equivalent to openSections.get()
  Section currentSection
Global end
```

<!-- ======================================================================= -->
## Node object

```
Node begin
  - the closest open presequent section
  - needed for all nodes
  Section parentSection
Node end
```

<!-- ======================================================================= -->
## SectioningNode object

```
SectioningNode extends Node begin
  - the section declared by this node
  Section declaredSection
SectioningNode end
```

<!-- ======================================================================= -->
## Section object

```
Section begin
  - the sectioning node that declared this section
  - alternatively: declaredBy
  SectioningNode sectioningNode

  - the closest open presequent section
  - optional due to sectioningNode.parentSection
  Section parentSection

  - the first content node of this section
  - also the section's first top-level node
  Node firstContentNode
Section end
```
