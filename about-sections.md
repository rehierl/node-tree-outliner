
# Sections

**TODO** -
explain - subsections => tree of sections

<!-- ======================================================================= -->
## Definition

A **section** is a sequence of subsequent nodes.

This definition merely states that a section is not just some sequence of
randomly selected nodes: The order of nodes associated with a section always
corresponds with a document's node sequence.

A section that has no subsections is a sequence of strictly subsequent nodes.
Consequently, any section is a subsequence of its document's node sequence.

**TODO** - explain (node sequence <=> section)

A section that has subsections is a sequence of strictly subsequent nodes, if
it is considered to also contain all nodes within all of its subsections.

If the nodes of a section's subsections are *not* considered to be included,
then a section is merely a sequence of subsequent nodes. In addition to that,
these sequences contain subsequences of strictly subsequent nodes. The
subsections of a section fill any gaps in between any strictly subsequent
subsequences (maybe even before the first or behind the last subsequence).

<!-- ======================================================================= -->
## Outline

The outline of a document represents the structure of its document as
a tree of sections.

A non-empty tree always has a single root section which can be seen to define
the tree of sections that starts with it. An outline is therefore defined by
the root section of its section tree.

Any descendant section of the outline's root section represents an **inner
outline**. The root section's direct subsections represent the **first inner
outlines** of an outline.

* "n-th inner outlines" (plural) is a level-wise perspective
* "n-th inner outline" (singular) is not defined

Each ancestor section of the outline's root section represents an **outer
outline**. The root section's parent section represents the **first outer
outline**, etc.

An outline also represents a tree of outlines.

<!-- ======================================================================= -->
## Table of contents (TOC)

A document's table of contents (TOC) represents the document's outline as
a tree of titles.

Each title within such a tree represents its corresponding section.

A TOC does not have to include all the titles of an outline,
(i.e. inner outlines may be ignored).

A TOC is just a hierarchical listing of a certain section property.
