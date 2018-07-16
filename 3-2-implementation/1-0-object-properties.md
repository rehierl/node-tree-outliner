
<!-- ======================================================================= -->
# Objects and variables

The following content is intended to provide
an overview of global variables and object properties.

Note that certain variables or object properties depend on the environment of
an implementation. That is, given a specific environment, certain variables or
properties can be omitted.

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
  - in principle required by/for any node,
    e.g. "when exiting a parent container"
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
  - the closest open presequent section
  - optional - due to sectioningNode.parentSection
  Section parentSection

  - the sectioning node that declared this section
  - not a content node - i.e. unassociated with that section
  - alternatively: declaredBy
  SectioningNode sectioningNode

  - the first content node of this section
  - also the section's first top-level node
  Node firstContentNode

  - the node subsequent to 'sectioningNode' that
    instructed to close this section object
  - null, if the section ends with its parent container
  - if set, the referenced node is the next sibling to
    the section's last top-level node
  - not a content node - i.e. unassociated with that section
  Node endMarkerNode

  - optional - in addition to .endMarkerNode
  - the parent container's last child,
    or the end-marker nodes previous sibling
  - a content node - i.e. associated with that section
  - not necessarily the section's last content node
  Node lastTopLevelNode
Section end
```
