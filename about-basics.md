
# Fundamental aspects

```
Example:
========
<body>
  A
  <h1>B</h1>
  C
</body>
```

Node `A` belongs to the section introduced by the body element (i.e.
**the body section**). The body section is said to contain node `A`.

Node `C` belongs to section `B` because the last section introduced before
node `C` is section `B`. There is also no indication that section `B` ends
before node `C`. If that were the case, node `C` would have to belong to
the body section.

**TODO** -
Does a heading element and its inner nodes (e.g. `h1` and `B`) belong to the
section that the heading element introduces, or to the section to which it is
subsequent (i.e. to some previous section)?

<!-- ======================================================================= -->
## Section (1)

A section is a sequence of nodes.

This definition implies that the nodes of a section have a specific order:

* synonymous - introduce, initialize, declare
* synonymous - associate with, establish a relationship with
* synonymous - is associated with, is related to

At some point, an element introduces a new section. From that point on, nodes
will be associated with this section, one after another, until that is
no longer allowed.

* A two-way, one-to-many (1:N) relationship.
* A section is empty, if no nodes were associated with it.
* A node is always added to the end of a section or more accurately,
  to the end of its sequence, when it has to be associated with it.
* The n-th node of a section's sequence is the section's n-th node.
* A non-empty section always has a first and a last node.
* A section is defined by its node sequence.

Definitions

* `Section Node.parentSection`
* `Node[] Section.innerNodes`

### open and closed sections

A section is open, if it is still allowed to associate entities
(nodes, a title, subsections, etc.) with it.

* synonymous - open, has started
* synonymous - closed, has ended, has stopped

A section is closed, if no more associations are allowed.

### associated resources

* synonymous - allocate, lock, create
* synonymous - released, unlocked, freed, destroy

Similar to binary streams, certain resources (e.g. memory) must be associated
with a section. These need to be allocated when a section is opened and
released when it is closed.

* Once a section is closed, it can not be re-opened.

Once introduced, a new section object is automatically opened for associations.
As this step will allocate resources, there needs to be a point for each section
at which the resources of a section can be released.

Ultimately, that point is reached for any section when the starting element
(e.g. the body element) has been processed. But, at that point, certain sections
might no longer be accessible. In such a case, resources allocated for sections
that are no longer accessible will remain locked (e.g. memory leaks).

<!-- ======================================================================= -->
## Sectioning element (1)

Any sectioning element always introduces a new section.

* A sectioning element introduces a single section
  (not 0, not 2, ..., not N, but exactly and always 1).
* synonymous - introduce, initialize, declare

This definition implies that no section can exist without first being
introduced by some sectioning element.

* A two-way, one-to-one (1:1) relationship.
* A section can be identified by its sectioning element.

Definitions

* `SectioningElement Section.declaredBy`
* `Section SectioningElement.declaredSection`

As a result, this definition also defines an order between
a sectioning element and its section:

* A sectioning element precedes its section.
* A section is subsequent to its sectioning element.
* This is an abstract order that represents that a section
  can not exist without its sectioning element.
* This does not state that the sectioning element
  can not be associated with its section.

In addition to that, this definition implies that some process will have to
switch away from a pre-existing section to the next new section as soon as the
next sectioning element is reached (i.e. there has to be some order on a
document's set of the sections).

* synonymous - declared before, pre-exists, precedes
* synonymous - next new, declared after, is subsequent to

If there is a preceding section, then there must also be a sectioning element
that precedes it (because this section must also be declared at some point).

* The sectioning element of a preceding section precedes the sectioning element
  of a subsequent section.
* The order required on the set of sections is equivalent to the order of their
  sectioning elements.

In between any two sectioning elements, there may be any number of
non-sectioning element nodes (i.e. nodes that do not introduce a new section).

Consequently, this definition also implies that all the nodes of a document
must be processed according to some order (i.e. there are preceding, and there
are subsequent nodes).

=> see also - a document's node sequence

### Additional notes

This definition does not state that a preceding section must end once the next
sectioning element is reached. Such a section may simply be suspended when the
new section begins and it may be resumed once that new section ends.

* synonymous - suspend, pause
* synonymous - resume, continue

The definition of a sectioning element must define (1) which effect it has on
pre-existing sections, and (2) what kind of relationship the new section has
with these.

### Does it, or does it not ...?

**TODO** -
The section of a sectioning element begins inside, or just behind of it.

=> see also - a sequence of nodes subsequent to a node

<!-- ======================================================================= -->
## Current section

Once a section is declared, it automatically becomes the current section. It
remains to be the current section for as long as (1) it did not end, and (2)
no new section was introduced by some other subsequent sectioning element.

* synonymous - current, active, current active

Any subsequent node must always be associated with the current active section,
i.e. determining to which section a node belongs, must always take multiple
aspects into account:

1. Was a new section introduced? =>
   The next subsequent node belongs to the new section, if that is the case.
2. Did the current section end? =>
   The next subsequent node belongs to this section, if that is *not* the case.
3. If the current section, or even multiple previous open sections have ended,
   which of these is the next current section?

At any given time, multiple sections may be open, but only one of these can be
the current active section. All the other sections are inactive, i.e. they may
be associated with further entities at some later point in time.

* synonymous - inactive, suspended
* Sections that are inactive are still open for associations.

**TODO** -
Stack of open sections - the current section is the section at the top of this
stack - not some random section, a specific order

### Node X belongs to section Y

* synonymous - belongs to, is located inside, is associated with, is related to

A node belongs to a section, if the node is associated with it.

This definition is based upon the direct relationship between a node and its
section (i.e. no subsections in between).

### Section X contains node Y

* synonymous - contains, is associated with, is related to

A section contains a node, if the node belongs to it.

<!-- ======================================================================= -->
## Relationship between sections and nodes

Nodes are directly associated with sections, which will also associate the
section with the associated node.

* More than one node can be associated with a single section.
* However, any node can only be directly associated with a single section.
* A two-way, one-to-many (1:N) relationship.

### nodes -> sections (NxS)

Any node within a document always belongs to some section,
regardless if that section has a title or not.

* NxS is left-total.

The belongs-to association puts each node into a direct relationship with a
single section: A node either belongs to one section, or it belongs to a
different one (i.e. a node can not directly belong to two different sections
at the same time).

* NxS is functional

Multiple nodes may still belong to the same section.

### sections -> nodes (SxN)

A section contains a node, if that node belongs to it.

* SxN is right-total.

Because multiple nodes may belong to the same section, a section either
contains no node at all, a single node, or more than one nodes.

* SxN is not functional

A section that itself does not contain any nodes, is not necessarily empty
(e.g. a section may consist of subsections only).

<!-- ======================================================================= -->
## Relations

We are already trapped deep inside discrete mathematics (graph theory)!

* [en.wikipedia.org, graph theory](https://en.wikipedia.org/wiki/Graph_theory)
* [en.wikipedia.org, binary relation](https://en.wikipedia.org/wiki/Binary_relation)
* [en.wikipedia.org, tree structure](https://en.wikipedia.org/wiki/Tree_structure)
* [en.wikipedia.org, tree (data structure)](https://en.wikipedia.org/wiki/Tree_%28data_structure%29)

The DOM tree is a tree data structure defined in terms of nodes and edges.

### Node.parentNode, Node.childNodes

The edges of a DOM node tree are defined in terms of pairs of nodes that are
elements of the Cartesian product `PxC`.

* `P` represents the set of parent nodes - `C` the set of child nodes -
  `P` and `C` are both equal to `N` - `N` is the set of all nodes.
* The characteristic function `R(p,c)` returns `1 (true)`, if node `p` is the
  parent node of child node `c`; otherwise, `0 (false)` is returned.
* All pairs of nodes for which `R` holds (i.e. is true) define the parent-child
  relationship between all nodes.
* `R` can be used to define boolean functions used to test certain conditions
  and functions that can be used to retrieve all the nodes that are associated
  with a given node.

Definitions

* `bool Node.isParentOf(Node c)`
* `bool Node.isChildOf(Node p)`
* `Node Node.parentNode()`
* `Node[] Node.childNodes()`

### Node.parentSection, Section.innerNodes

The belongs-to/contains-node relationship between nodes and sections can be
defined in terms of pairs that elements of the Cartesian product `NxS`.

* `S` represents the set of all sections

Definitions

* `bool Node.belongsTo(Section s)`
* `bool Section.containsNode(Node n)`
* `Section Node.parentSection()`
* `Node[] Section.innerNodes()`

**TODO** -
Section.firstInnerNode(), Section.lastInnerNode(), ... -
requires an order of some sort

### Section.parentSection, Section.subsections

The parent-of/contains-section relationship between sections can be defined in
terms of pairs that are elements of the Cartesian product `SxS`.

* `P` represents the set of sections that have one or more subsections (`PxS`)
* `C` represents the set of sections that have a parent section (`SxC`) -
  the root section does not have a parent section

Definitions

* `bool Section.isParentOf(Section c)`
* `bool Section.isSubsectionTo(Section p)`
* `Section Section.parentSection()`
* `Section[] Section.subsections()`

**TODO** -
firstSubSection(), lastSubSection(), ... -
requires an order of some sort

<!-- ======================================================================= -->
## A memory hook

```
<- root <-          path-of-nodes          -> leaf ->
<- parent-of                              child-of ->

... x N x N x ... x N x N x ...    (down) belongs-to
      x                 x
... x S x S x ... x S x S x ...    (up) contains-node

<- parent-section                      sub-section ->
```

<!-- ======================================================================= -->
## Inner nodes, outer nodes

All inner nodes are descendant to a given node.

* synonymous - descendant nodes, inner nodes

The outer nodes of a node are the nodes that remain of a node tree once (1) the
node itself is and (2) all its inner nodes are removed.

* `outer-nodes := (all-nodes - element - inner-nodes)`
* => *not* synonymous - ancestors, outer nodes
* `#(x) := number-of-set(X)`
* `#(ancestors) <= #(outer-nodes)`

**TODO** -
N-th outer node?

<!-- ======================================================================= -->
## Heading element (1)

A heading element is a sectioning element.

A heading element is parent to all of its child nodes. The inner nodes of a
heading element define the title for the heading's section.

**TODO** -
effect/relationship on/with other sections -
A heading's section begins just after the heading element -
excludes: belongs itself to it section

<!-- ======================================================================= -->
## Parent container X of section Y

Except for the body element,
any node of a document has a parent element.

* Any parent element is a container element.
* Based on the NxN binary relation of a tree data structure.

The parent element of element `X` is the parent container of section `Y`,
if element `X` introduces section `Y` as an outer section.

* The parent container of a section introduced by a heading element is
  the heading's parent element.

If element `X` introduces section `Y` as an inner section, then element `X` is
itself the parent container of section `Y`.

* The parent container of the section introduced by the body element is
  the body element.

This definition is based upon an element's characteristic to
introduce a new section:

* A sectioning element and the section's parent container element are not
  necessarily identical (i.e. these can be different elements).
* A section always begins inside of its parent container.
* This definition is independent of where exactly a section ends.

<!-- ======================================================================= -->
## Relationship between sections

### subsequent

### inner -> outer

### outer -> inner

### formal definitions

Relations that need to be defined using scientific methods:
SxS (parent-of/child-of), `S` is the set of sections

**TODO** -
formalize this
