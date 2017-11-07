
<!-- ======================================================================= -->
## Section (2) - TODO

* `SxS` relation

<!-- ======================================================================= -->
## Sectioning node (2) - TODO

* Does a sectioning element belong to the section it introduces?
* The section of a sectioning element begins inside, or just behind of it.
* A section is subsequent to its sectioning element.

<!-- ======================================================================= -->
## Current section (2), Stack of open sections - TODO

Traversing the relevant tree in order to produce an outline needs to (implicitly
or explicitly) create and update stacks of open sections.

Stack of open sections - the current section is the section at the top of this
stack - not some random section, a specific order -
path in the tree of sections (starts at the root, ends at the current section)

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
