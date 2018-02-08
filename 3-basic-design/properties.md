
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
  - the closest open presequent section
  - optional due to sectioningNode.parentSection
  Section parentSection

  - the sectioning node that declared this section
  - alternatively: declaredBy
  SectioningNode sectioningNode

  - the first content node of this section
  - always a top-level node
  Node firstContentNode
Section end
```
