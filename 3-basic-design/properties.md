
## global scope

```
Global begin
  - all currently open sections
  - the bottom section is the root section
  - the top-most section is the current section
  Stack<Section> openSections

  - a reference to the current section
  - used to associate all the nodes
  - equivalent to openSections.get()
  Section currentSection
Global end
```

## node object

```
Node begin
  - the closest open presequent section
  - needed for all nodes
  Section parentSection
Node end
```

## sectioning nodes

```
SectioningNode extends Node begin
  - the section declared by this node
  Section declaredSection
SectioningNode end
```

## section object

```
Section begin
  - the sectioning node that declared this section
  - alternatively: declaredBy
  SectioningNode sectioningNode

  - the closest open presequent section
  - optional due to sectioningNode.parentSection
  Section parentSection

  - the first content node of this section
  - always a top-level node
  Node firstContentNode
Section end
```
