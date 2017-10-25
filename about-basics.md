
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

* Any node always belongs to some section.

Node `C` belongs to section `B`.

* There is no indication that section `B` ends before node `C`.
  If that were the case, node `C` would have to belong to a pre-existing
  section (i.e. the body section).
* No other new section is introduced before node `C`.
  If that were the case, node `C` would have to belong to this new section.

**TODO** -
Does a heading element and its inner nodes (e.g. `h1` and `B`) belong to the
section that the heading element introduces, or to a section to which it is
subsequent (i.e. to some previous section)?

<!-- ======================================================================= -->
## Section (1)

A section is a sequence of nodes.

This definition implies that the nodes of a section have some order.

* synonymous - introduce, initialize, declare
* synonymous - associate with, establish a relationship with
* synonymous - is associated with, is related to

At some point, an element introduces a new section. From that point on, nodes
will be associated with this section, one after another, until that is no longer
allowed. Consequently, the order of nodes is based upon the traversal of a node
tree.

* The `SxN` relation is a two-way, one-to-many (1:N) relationship
  (`S` is the set of sections, `N` the set of nodes).
* A section is empty, if no nodes were associated with it.
* A node is added to the end of a section, or more accurately
  to the end of its sequence, when it has to be associated with it.
* The n-th node of a section's sequence is the section's n-th node.
* A non-empty section always has a first and a last node.

A section is declared by its sectioning element and defined by its node sequence.
To truly distinguish sections from one another, the section's sectioning element
must be taken into account (e.g. empty section).

Definitions

* `Section Node.parentSection`
* `Node[] Section.innerNodes`

### open and closed sections

* synonymous - open, has started

A section is open, if it is still allowed to associate entities
(nodes, a title, subsections, etc.) with it.

* synonymous - closed, has ended

A section is closed, if no more associations are allowed.

* From that point on, a section is fully defined/qualified.

### associated resources

* synonymous - allocate, lock, create
* synonymous - release, unlock, free, destroy

Similar to binary streams, certain resources (e.g. memory) must be associated
with a section. These need to be allocated when a section is opened and released
when it is closed.

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

* synonymous - introduce, initialize, declare

A sectioning element introduces a new section.

* Any node can be classified as a sectioning, or as a non-sectioning node:
  A node either introduces a new section, or it does not.
* A sectioning element introduces a single section
  (not 0, not 2, ..., not N, exactly and always 1).

This definition implies that no section can exist without
first being introduced by some sectioning element.

* This `NxS` relation is a two-way, one-to-one (1:1) relationship.
* Any section can be identified by its sectioning element.

Definitions

* `SectioningElement Section.declaredBy`
* `Section SectioningElement.declaredSection`

As a result, this definition also defines an order between
a sectioning element and its section:

* A sectioning element precedes its section.
* A section is subsequent to its sectioning element.
* A section can not exist without its sectioning element.

This definition also implies that some process will have to switch away from
a pre-existing section to the introduced next new section as soon as the next
sectioning element is reached (i.e. there is some order on a document's set of
sections).

* synonymous - declared before, pre-exists, precedes
* synonymous - next new, declared after, is subsequent to

If there is a preceding section, then there must also be a sectioning element
which precedes it (because that section must also be declared at some point).

* The sectioning element of a preceding section
  precedes the sectioning element of a subsequent section.
* The order on the set of sections is
  equivalent to the order of their sectioning elements.

This definition does not state that a preceding section must end once the next
sectioning element is reached. Such a section may simply be suspended when the
new section begins and it may be resumed once that new section ends.

* synonymous - suspend, pause
* synonymous - resume, continue

The definition of a sectioning element must define (1) which effect it has on
pre-existing sections, and (2) what kind of relationship the new section has
with these.

=> see also - a sequence of nodes subsequent to a node

<!-- ======================================================================= -->
## Current section (1)

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

### Node X belongs to section Y

* synonymous - belongs to, is located inside, is associated with, is related to

A node belongs to a section, if the node is associated with it.

This definition is based upon the direct relationship between a node and its
section (i.e. no subsections in between).

**TODO** -
is located inside -> loosely related to

### Section X contains node Y

* synonymous - contains, is associated with, is related to

A section contains a node, if the node belongs to it.

<!-- ======================================================================= -->
## Section (2) - TODO

* `SxS` relation

<!-- ======================================================================= -->
## Sectioning element (2) - TODO

* Does a sectioning element belong to the section it introduces?
* The section of a sectioning element begins inside, or just behind of it.
* A section is subsequent to its sectioning element.

<!-- ======================================================================= -->
## Stack of open sections - TODO

Stack of open sections - the current section is the section at the top of this
stack - not some random section, a specific order -
path in the tree of sections (starts at the root, ends at the current section)

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
