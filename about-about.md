
**TODO** -

Trying to overlay a structure of sections over a tree of nodes is like adding a
3rd dimension (outline depth) to a two-dimensional object (node level x, sibling
y on level x). Which requires a completely different way of thinking.

Imagine a flat surface, draw the dom tree onto it and elevate each node according
to its outline depth. Each elevated layer contains all nodes that have the same
outline depth. => landscape of a document

Imagine the node sequence of a document in a straight line, each node has an
absolute index within that sequence (1st dimension). Elevate each node according
to its outline depth (2nd dimension). => graph of a document

**TODO** - 

In general, any section ends inside of its parent container element.

**TODO** -

If a node is associated with a section, then all of its child nodes are also
(indirectly) associated with that section.

**TODO** -

Nodes must be associated with a section while they are being entered.
Explain why!

**TODO** -
Almost a Parker Square - dishonesty

**TODO** -
The stack of open sections -
in the section tree -
a path to the current section

<!-- ======================================================================= -->
## Active/Passive nodes

Entering and/or exiting **an inactive (or passive) node** has no effect on the
current state of the outline (i.e. the outline remains unchanged). However, a
passive node may have active descendant nodes.

Entering and/or exiting **an active node** will always changes the current state
of an outline in some way, even if all of its descendant nodes are passive nodes.

**A seemingly active node** is a node that needs to change the outline's state
because of a definition that is not directly associated with itself.

The body element is a seemingly active node because ultimately, any section has
to end with the body element. Also, any document always has at least one section
that ends with the document's body element (because all nodes within a document
always belong to some section).

**TODO** -
ends with parent container - a characteristic of a section, or an element?
the body element is inactive, if it is a characteristic of a section!

<!-- ======================================================================= -->
## Active/Passive content

A sequence of subsequent passive nodes, represents passive content. Processing
the nodes of such a sequence will not change the document's outline in any way.

A group of nodes that contains at least one active node, is said to represent
active content. Processing all nodes of active content will eventually change
the document's outline.

<!-- ======================================================================= -->
## Processing nodes/content

Processing a node, that has no child nodes, means to execute all operations
associated with entering and exiting that node.

Processing a node that has descendant nodes means to process the node itself
and any of its descendant nodes.

Processing content means to process any of its directly subsequent nodes.
The outline of a document is created by processing the document's content.

**TODO** -
partially processed parent nodes

<!-- ======================================================================= -->
## Document - TODO

A document's node sequence is a sequence of subsequent sections.

Any section has a node that precedes it (i.e. the section's sectioning element).

A section is a subsection to the parent section of its sectioning element. Put
differently, the outer section of a sectioning element tells the section that
is introduced to which section it is a subsection.

The section of a sectioning root belongs to a document. As such, it contributes
to the outline (tree of sections) of its document. The choice to not include
such an inner outline in a document's TOC is a choice by preference, (i.e. not
strictly required).

<!-- ======================================================================= -->
## Element X contains section Y

A container element `X` contains section `Y` as an inner section, if `X` is the
section`s parent container. **TODO** - based on container - excludes subsections

<!-- ======================================================================= -->
## Section X (is located inside | belongs to | is associated with) container Y

A section is said to be located inside of its parent container.

In addition to that, a section can also be said to be belong to, or to be
associated with its parent container element.

Note that a section's belongs-to-node (outwards) and contains-node (inwards)
associations have different direction!
