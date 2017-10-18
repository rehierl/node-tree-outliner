
# Notes

**TODO** -
Nodes must be associated with a section while they are being entered.
Explain why!

<!-- ======================================================================= -->
## Active/Passive nodes

Entering and/or exiting **an inactive (or passive) node** has no effect on the
current state of the outline (i.e. the outline remains unchanged). However, a
passive node may contain active descendant nodes.

Entering and/or exiting **an active node** will always changes the current state
of an outline in some way, even if that node only has passive descendant nodes.

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
## Section

A **section** is a sequence of subsequent nodes.

This definition merely states that a section is not just some sequence of
randomly selected nodes: The order of nodes associated with a section always
corresponds with a document's node sequence (because nodes must be associated
with a section while they are being entered).

A section that has no subsections is a sequence of strictly subsequent nodes.
Consequently, such a section is a subsequence of its document's node sequence.

A section that has subsections is a sequence of strictly subsequent nodes, if
it is considered to also contain all nodes within all of its subsections.

If the nodes of a section's subsections are *not* considered to be included,
then a section is merely a sequence of subsequent nodes. But, in addition to
that, these sequences of nodes can be split up into sequences of strictly
subsequent nodes. With that perspective, the subsections of a section can be
seen to fill the gaps in between the strictly subsequent subsequences.

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
## Open/Closed Sections

A section is considered open, if it is still allowed to associate entities
(nodes, a heading and subsections) with it. A section is closed (has ended),
if that is no longer allowed.

Similar to binary streams, certain resources (e.g. memory) will be associated
with a section. These must be allocated (locked) when a section is opened and
released (freed, unlocked) when it is closed.

Once created, a new section object is automatically opened for associations.
As this step will allocate resources, there needs to be a point for each section
at which a section's resources can be released.

Ultimately, that point is reached for any section when tree traversal ends. But,
at that point, certain sections might no longer be accessible. In such a case,
resources allocated for sections that are no longer accessible will remain
locked (e.g. memory leaks).

<!-- ======================================================================= -->
## The current/active section - TODO

* At any given time, multiple sections may be open.
* Only one open section is considered to be the current/active section.

<!-- ======================================================================= -->
## Implied headings

During tree traversal, the following states can be observed:

0. A section object is created and automatically opened for associations
   (i.e. `(section.heading == null)` is true).
1. A section is still open, but no heading was associated with it
   (i.e. `(section.heading == null)` is still true).
2. The first heading element within an open section was entered and associated
   with that section (i.e. `(section.heading != null)` is true - step F.1.1).
3. A section has ended and *a heading* element was associated with it
   (i.e. `(section.heading != null)` remains to be true).
4. A section has ended and *no heading* element was associated with it
   (i.e. `(section.heading == null)` remains to be true).

From these states, the following statements can be derived:

1. The expression `(section.heading == null)` is true for sections that
   have *no heading* and that are either *open or closed*.
2. The expression `(section.heading != null)` is true for sections that
   have *a heading* and that are either *open or closed*.

Note that both expressions are ambiguous with regards to a section's
is-open-or-closed state.

Obviously, it would be preferable to have a dedicated is-open-or-closed state
property for each section. But, such a property would only have a use for as
long as tree traversal has not finished. Once tree traversal is done, all
sections are closed and such a property would hold the exact same value for any
section (i.e. such a state property would be wasting memory).

The current algorithm will therefore associate a non-null pseudo heading
(aka. implied heading) with a section that has ended and that has no heading.
This allows to make the following statements:

1. The expression `(section.heading == null)` is true for sections that
   have *no heading* and that are *still open*.
2. The expression `(section.heading != null)` is true for sections that
   have *a heading* (implied or not) and that are either *open or closed*.

Therefore, if expression (1) (i.e. `section.hasNoHeading()`) evaluates to true,
a heading can still be associated with the corresponding section because that
section is still open. -- This is at least the intention behind implied headings.

Obviously, it would be an error to associate an implied heading with an open
section that has no heading (because a heading element could still follow). As
a result, the expression `section.setImpliedHeading()` implicitly states, that
the corresponding section has no heading *and* that it has ended.

Overwriting an implied heading would also be an error, because this would
represent an attempt to continue a section that has already ended. Once a
section ends, any resources associated with it can be released. After that,
those resources can no longer be accessed because any such attempt would
inevitably trigger an access violation error.

**TODO** -
Each heading element has a rank.
Is it necessary to associate a rank (highest or lowest) with an implied heading?
Does the algorithm implicitly associate a rank with an implied heading?
