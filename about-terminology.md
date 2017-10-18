
# Terminology

This document is used to clarify important terms that are used throughout this
repository.

## Outline

The outline of a document represents the structure of its document as
a tree of sections.

Except for an empty tree, any tree always has a single root section. An outline
is therefore defined by the root section of its section tree.

Consequently, any section within such a section tree represents an inner outline.
The root section's subsections are said to represent the outline's first inner
outlines, etc.

Any ancestor section of an outline's root section is said to represent one of
the outline's outer outlines. The root section's parent section is said to
represent the outline's first outer outline, etc.

**TODO** -
define the tree of outlines

## Table of contents (TOC)

A document's table of contents (TOC) represents the document's outline as
a tree of headings.

Each heading within such a tree represents its corresponding section.

Note - A TOC does not have to include the headings of an outline, (i.e. inner
outlines may be ignored).

## Processing nodes/content

Processing a node, that has no child nodes, means to execute all operations
associated with entering and exiting that node.

Processing a node that has descendant nodes means to process the node itself
and any of its descendant nodes.

Processing content means to process any of its directly subsequent nodes. The
outline of a document is created by processing the document's content.

## Active/Passive nodes

A node that has no effect on the outline of a document is said to be **passive**
with regards to the process of creating a document's outline. Entering and exiting
a passive node does not change the document's outline in any way. However, a
passive node may contain active descendant nodes.

An **active** node introduces a new section, ends existing ones, or has both
of these characteristics. Entering and/or exiting an active node will therefore
always change the document's outline in some way, even if that node only has
passive descendant nodes.

Note - Like any heading element, the body element is an active node because
ultimately, any section has to end with the body element. Also, any document
always has at least one section that ends with the document's body element
(because all nodes within a document always belong to some section).

**TODO** -
ends with parent container - a characteristic of a section, or an element?

## Active/Passive content

A group of one or more subsequent passive nodes, is said to represent passive
content. Processing the nodes of such a group will not change the document's
outline in any way.

A group of nodes that contains at least one active node, is said to represent
active content. Processing all nodes of active content will eventually change
the document's outline.

## The body section

The section that is introduced by a document's body element is simply referred
to as "the body section".

## Heading X introduces section X

Assume that any heading element can be identified by the heading's inner nodes,
or some other unique characteristic (e.g. the heading's `id`).

The intention behind this definition is to identify a section by the heading
element that introduced it. Note that each heading element always introduces a
single section (i.e. never more than one).

A reference of the form "section `A`" therefore refers to the section introduced
by the corresponding heading element.

## Heading X of section Y

If a section `A` is introduced by heading element `A`, then that heading element
is also said to be the heading of that section.

## Node X (is located inside | belongs to | is associated with) section Y

Node `B` is said to be located inside section `A` because there is nothing that
introduces a new section in between heading `A` and node `B`. There is also
nothing that indicates that section `A` ends before node `B` is reached.

If a node is located inside a section, then it is also said to belong to, or to
be associated with, that section. In such a case, the node and its section are
both said to have a direct relationship.

Note that this definition is based upon the direct relationship between a node
and its section (i.e. no subsections in between).

## Section X (contains | is associated with) node Y

Section `A` contains node `B` because node `B` is located inside section `A`.

If a node is located inside a section, then that section is said to contain, or
to be associated with, that node.

Note the direct relationship between the node and its section.

## Parent container X of section Y

Except for the body element, any node within a document always has a parent
element. A node's parent element is said to be the node's parent container
element because it contains the node as one of its inner child nodes.

A heading element is the parent container of all its inner child nodes. The inner
nodes of a heading element define the heading for the section that the heading
element introduces.

The parent container of a section introduced by a heading element is the parent
element of that heading. In general, the parent element of element `X` is said
to be the parent container of section `Y` if element `X` introduces section `Y`
as a subsequent section (i.e. not inside of it).

The parent container of the section introduced by the body element is the body
element. In general, element `X` is said to be the parent container of section
`Y` if element `X` introduces section `Y` as an inner section.

A container element is said to contain section as an inner section if that
container element is the section`s parent container.

Note that the element which introduced a section and the section's parent
container element are not necessarily identical (i.e. these can be different
elements).

Note that, as this definition is based upon an element's characteristic to
introduce a new section, it is independent of where exactly a section ends. The
only statement that can be made is that a section always begins inside its
parent container.

## Section X (is located inside | belongs to | is associated with) container Y

A section is said to be located inside of its parent container.

In addition to that, a section can also be said to be belong to, or to be
associated with its parent container element.

Note that a section's belongs-to-node (outwards) and contains-node (inwards)
associations have different direction!
