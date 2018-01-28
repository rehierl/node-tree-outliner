
<!-- ======================================================================= -->
# Design (6) - associating sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Fundamental considerations.

* As stated before, all nodes must be associated while they are being entered.

Introduction to sectioning nodes:

* If all sectioning nodes would have to be associated with their own
  section, then no section would ever be truly empty. That is, because
  any section would then always begin with its sectioning node.
* Associating sectioning nodes with their own section adds a sectioning
  node to its own context, although no node is presequent to itself.
* A section could then not be said to be subsequent to its sectioning
  node. That is, because a sectioning node is insequent (i.e. neither
  pre- nor subsequent) to itself.

Definition of section states/events:

* Associating sectioning nodes with their own section can be seen to be in
  conflict with the open event of a section. That is, because nodes would
  have to be associated before a section can even count as being open.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Less confusion with regards to discussions.

If sectioning nodes would have to be associated with their own sections,
then there would always be the difficulty of having to distinguish between
(1) the first node that is associated with a section, and (2) the section's
first actual content node.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Allows to describe the general layout of a section.

If a sectioning node would have to be associated with its own section, then the
sectioning node and all of its descendants would also automatically belong to
the declared section and therefore also to its node sequence. Consequently. it
would not be possible to describe the general properties of a section's node
sequence (see: reduced sequence) independently of its sectioning node.

That is, because the index of the first actual content node within the section's
node sequence would then not be the same for all section types. That is, because
a section's node sequence would then always begin with the section's sectioning
node, which might then followed by one or more intermediate nodes, which are
then followed by the section's actual content nodes.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Consistency with regards to parent containers.

If a sectioning node would have to be associated with its own section, then the
parent container of a type-1 section, which is identical to a type-1 sectioning
node, would automatically belong to the type-1 section. In contrary to that,
the parent container of a type-2 section, which never is identical to a type-2
sectioning node, would still belong to a section that is presequent to its
inner type-2 section.

In other words: Some parent containers would belong to those
sections whose default scope they have to end, but others would not.

Note that the parent container of a type-2 section
must not be associated with such a section.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Non-Empty parent sections.

If all sectioning nodes would have to be associated with their own section, then
a parent section, which only contains a single subsection, but no actual content
nodes of its own, would appear to have no meaningful content. That is, the
corresponding section would appear to be empty. And, because of that, one would
always also have to explicitly check for the existence of possible subsections.

Note that the sectioning node of a subsection would then only be associated
with the subsection it declares. That is, because each node can and will be
associated with one section only. Despite that, a sectioning node still counts
as being implicitly associated with all of its ancestor sections.

With that regards, the advantage of not associating a sectioning node with its
own section therefore is that no parent section will ever appear to be empty.
A parent section will then always have at least one content node and, because
of that, can never be misunderstood to be empty.

That is, there is no need to check the existence of possible subsections, if
the only question that needs to be answered is, whether the parent section
is empty or not. One only needs to test, if a node exists that is strictly
associated with the corresponding section.

* has subsections => has strictly associates nodes => not empty
* not empty => does not necessarily have subsections
* has no strictly associated node => empty

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
A consistent `Node.parentSection` reference.

```
Section Node.parentSection
```

In general, a `parent` property has a clear orientation: from a subordinate
entity towards an entity that is superordinate to it (hence the word "parent").
In short: The general orientation of a `parent` property is "upwards".

In this context, the direction which is consistent with this general
orientation is from a subsequent node towards a node that is presequent
to it. To be more accurate: towards a node that is within its context.

Note that no presequent node is considered to be subordinate to any node
which is subsequent to it. A superordinate node (i.e. a parent node) always
is presequent to those that are subordinate to it (i.e. its descendants).

Associating a sectioning node with its own section will obviously be in
conflict with this general orientation. That is, because it would connect a
superordinate entity (i.e. the sectioning node) with one that is subordinate
to it (i.e. the declared section). Because of that, and with regards to a
sectioning node, the property's direction would be turned upside-down as it
would point from a presequent node towards nodes that are subsequent to it
(i.e. its content nodes). The property's orientation would therefore point
"downwards". Consequently, additional logic would always be required in
order to take the property's different orientations into account (e.g. when
entering and exiting the sections, i.e. when traversing through sections).

Note that the direction of the parent property, with regards to all other
nodes, is guaranteed to be consistent with the afore mentioned orientation.
That is, because they will always be associated with the section of a
presequent sectioning node.

Not associating all sectioning nodes with their own section guarantees that
the orientation of this property is always consistent with regards to all
nodes in the corresponding tree. That is, the `parentSection` property will
always point "upwards".

Note that this parent property, with regards to the descendants of a type-2
sectioning node, obviously needs to be consistent with its ancestor (i.e.
the sectioning node), regardless if sectioning nodes are associated with
their sections or not. That is, because of descendant nodes being implicitly
associated with the sections of their ancestors.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
A sectioning node binds the contents of a section to the node tree.

```
Node Section.sectioningNode
```

The sectioning node of a section can be understood to act as a frame that
defines where exactly, with regards to its surrounding nodes, a section is
located. As such, a sectioning node can be understood to be the node that
defines the "physical" location of a section.

Note that the content nodes of a section have, because of their relationship
with the surrounding nodes of their parent section, similar statements. As
a result, the statements of its content nodes must correspond with the
statement of the sectioning node. This consistency is however guaranteed as
a section is strongly connected and because the default scope of a section
must end with its parent container.

Not associating a sectioning node with its own section therefore guarantees
that all content nodes of a section can be extracted from the tree without
loosing an anchor-like node. A sectioning node can therefore be used to
reintegrate a section at its exact location.

Transformations would not be as straight forward, if sectioning nodes would
have to be associated with their own section. That is, because these nodes
would then count as content nodes. Consequently, after having extracted all
content nodes, the information of where exactly the section was located
would no longer be available.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
A sectioning node binds a section to its parent section.

```
(1) Section Section.parentSection
(2) Node Section.sectioningNode
(3) (section.parentSection === section.sectioningNode.parentSection)
```

If all sectioning nodes would have to be associated with their own section,
then a sectioning node counts as the first content node of the corresponding
section. And, because of that, the above expression would be false for all
sections. That is, because the second part would represent a self-reference,
which obviously could never correspond with a `Section.parentSection` property.

With that in mind, not associating any sectioning node with its own section has
the advantage, that the above expression would always be true. And, because of
that, a `Section.parentSection` property is not required (i.e. optional).

See also: A consistent `Node.parentSection` reference.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Consistent node references.

```
(1) Node Section.sectioningNode
(2) Node Section.firstContentNode
```

In general, an implementation will have to hold at least two node references
with each section object: (1) a reference to the sectioning node, and (2) a
reference to the section's first content node.

If all sectioning nodes would have to be associated with their own section,
then a sectioning node counts as the first content node of the corresponding
section. And, because of that, the `firstContentNode` property would have to
be used to reference the section's first actual content node, instead of its
very first node. That is, in order to bypass having to distinguish between the
different types of sectioning nodes. As such, these properties can then be seen
to be inconsistent with such a design decision.

In contrary to that, and when not associating any sectioning node with its own
section, the `firstContentNode` property always corresponds with the section's
very first node.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The sectioning node of a node's parent section
never is identical to the corresponding node itself.

```
(node.parentSection.sectioningNode !== node)
```

That is obviously true for any node which is not a sectioning node. However,
this expression is also true if the node is a sectioning node. That is, because
no such node is associated with the section it declares.

Note that, if sectioning nodes would have to be associated with their own
section, then the first part of the above expression will be a self-reference,
if the node in question is a sectioning node.

See also: A consistent `Node.parentSection` reference.
