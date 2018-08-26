
<!-- ======================================================================= -->
# Associating sectioning nodes

In principle, any node, including all sectioning nodes, must be associated with
all open presequent sections (formal approach). That is, even if each node is
strictly associated with one section only (practical approach). Because of that,
no sectioning node can be associated with a random/arbitrary section.

* No sectioning node can be associated with a section that is subsequent to
  it. That is because these sections do not count as being open by the time
  the sectioning node is being entered. Despite that, such an association
  would also be in conflict with the context of the sectioning node.
* No sectioning node can be associated with a presequent section that is
  already closed when the sectioning node is being entered. That is because
  it would be in conflict with the closed state of a section as it would add
  that sectioning node to the closed section.

Consequently, a sectioning node can only be associated with the section it
declares (a technical possibility) and/or with all remaining open presequent
sections. Because of that, there are only two options available:

1. Associate a sectioning node with its own section, or
2. with the parent section of the section it declares.

Note that the statement "A sectioning node does not belong to its own section",
(not option 1), is equivalent to "A sectioning node belongs to the parent
section of the section it declares" (option 2).

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Fundamental considerations.

* As stated before, all nodes must be associated while they are being entered.

From the introduction of sectioning nodes:

* If all sectioning nodes would have to be associated with their own
  section, then no section would ever be truly empty. That is because
  any section would then always begin with its own sectioning node.
* Associating sectioning nodes with their own section adds a sectioning
  node to its own context, although no node is presequent to itself.
* A section could then not be understood to be subsequent to its
  sectioning node. That is because a sectioning node, like any other
  node, is insequent (i.e. neither pre- nor subsequent) to itself.

From the definition of section states/events:

* Associating sectioning nodes with their own section can be seen to be in
  conflict with the open event of a section. That is because nodes would
  have to be associated before a section can truly count as being open.
  However, a section is guaranteed to exist by the time its sectioning node
  is being entered.

From the definition of inner sections:

* Not associating sectioning nodes with their own sections guarantees that
  the section hierarchy is acyclic. That is because a section never is a
  subsection to itself. Which is because a parent section always has more
  content nodes than any of its inner sections.

From the definition of end-marker nodes (/see/ extensions /):

* End-marker nodes will not be associated with the sections they close.
  Because of that, case-dependent associations would have to be justified, if
  sectioning nodes would have to be associated with the sections they declare.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Less confusion with regards to discussions.

If sectioning nodes would have to be associated with their own sections,
then there would always be the difficulty of having to distinguish between
(1) the first node that is associated with a section, and (2) the section's
first actual content node.

Not associating any sectioning node with its own section allows to avoid this
confusion, as no sectioning node would then belong to the section it declares.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Allows to describe the general layout of a section.

If a sectioning node would have to be associated with its own section, then the
sectioning node and all of its descendants would also automatically belong to
the declared section and therefore also to its node sequence. Consequently. it
would not be possible to describe the general properties of a section's node
sequence (/see/ reduced sequence /) independently of its sectioning node.

That is because the index of the first actual content node within the section's
node sequence would then not be the same for all section types. Which is,
because a section's node sequence would then always begin with the section's
sectioning node, which could then be followed by one or more intermediate
data nodes (/see/ type-2 sectioning nodes /), which are then followed by the
section's actual content nodes.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Consistency with regards to all parent containers.

If a sectioning node would have to be associated with its own section, then the
parent container of a type-1 section, which is identical to a type-1 sectioning
node, would automatically belong to the type-1 section. In contrary to that,
the parent container of a type-2 section, which never is identical to a type-2
sectioning node, would still belong to a section that is presequent to its
inner type-2 section.

In other words: Some parent containers would then belong to those
sections whose default scope they have to end, but others would not.

Recall that the parent container of a type-2 section must not be
associated with such a section.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Non-Empty parent sections.

If all sectioning nodes would have to be associated with their own section,
then a parent section, which only contains a single subsection, but no actual
content nodes of its own, would appear to have no meaningful content. Due to
having no strict association of its own, it would appear to be empty. And,
because of that, one would always have to explicitly also test whether the
section in question has any subsections or not.

Note that the sectioning node of a subsection would then only be associated
with the subsection it declares. That is because each node can and will be
associated with one section only. Although a sectioning node would still
count as being implicitly associated with all of its ancestor sections.

With that in mind, the advantage of not associating a sectioning node with its
own section therefore is, that no parent section will ever appear to be empty.
A parent section will always have one or more content nodes (i.e. the sectioning
nodes of its subsections) and, because of that, can never be misunderstood to be
empty.

That is, there is no need to check the existence of possible subsections, if
the only question that needs to be answered is, whether the section in question
is empty or not. One only needs to test, if a node exists that is strictly
associated with the corresponding section.

* has subsections => has strictly associates nodes => not empty
* not empty => does not necessarily have subsections
* has no strictly associated node => empty

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
A consistent `Node.parentSection` property.

In general, a `parent` property has a clear orientation: from a subordinate
entity towards an entity that is superordinate to it (hence the word "parent").
In short: The general orientation of a `parent` property is "upwards".

In this context, the general direction which is consistent with this
orientation is from a subsequent node towards a node that is presequent
to it. To be more accurate: towards a node that is within the corresponding
node's context.

Note that no presequent node is considered to be subordinate to any node
which is subsequent to it. A superordinate node (i.e. a parent node) always
is presequent to those that are subordinate to it (i.e. its descendants).

Associating a sectioning node with its own section will obviously be in
conflict with this general orientation. That is because it would connect a
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
That is because they will always be associated with the section of a
presequent sectioning node.

Not associating any sectioning node with its own section guarantees that
the orientation of this property is always consistent with regards to all
nodes in the corresponding tree. That is, the `parentSection` property will
always point "upwards".

Note that this parent property, with regards to the descendants of a type-2
sectioning node, obviously needs to be consistent with its ancestor (i.e.
the sectioning node), regardless if sectioning nodes are associated with
their own sections or not. That is because of descendant nodes being
implicitly associated with the sections of their ancestors.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Binds the contents of a section to the node tree.

```
SectioningNode Section.sectioningNode
```

The sectioning node of a section can be understood to act as a frame that
defines where exactly, with regards to its surrounding nodes, a section is
located. As such, a sectioning node can be understood to be the node that
defines the "structural/physical" location of a section.

Note that the content nodes of a section have, because of their relationships
with the surrounding nodes of their parent section, similar statements. As
a result, the statements of its content nodes must correspond with the
statement of the sectioning node. This consistency is however guaranteed as
a section is strongly connected and because the default scope of a section
ends with its parent container.

Not associating a sectioning node with its own section therefore guarantees
that all content nodes of a section can be extracted from the tree without
loosing an anchor-like node. A sectioning node can therefore be used to
reintegrate a section at its exact location.

Transformations would not be as straight forward, if sectioning nodes would
have to be associated with their own section. That is because the sectioning
nodes would then also count as content nodes. Consequently, after having
extracted all content nodes, the information of where exactly the section was
located would no longer be available.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Binds a section to its parent section.

```
(1) Section Section.parentSection
(2) Node Section.sectioningNode
(3) (section.parentSection === section.sectioningNode.parentSection)
```

If all sectioning nodes would have to be associated with their own section, then
any sectioning node counts as the first content node of the section it declares.
And, because of that, the above expression would be false for all sections. That
is, because the second part would represent a self-reference, which obviously
could never correspond with the `Section.parentSection` property.

With that in mind, not associating any sectioning node with its own section
has the advantage, that the above expression would always be true. And, because
of that, the `Section.parentSection` property is in principle not required (i.e.
optional). As such, that property is a mere matter of convenience.

Note that this appears to be consistent with not having to explicitly define
the corresponding relations (i.e. `SxN` and `SxS`).

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Consistent node references.

```
(1) Node Section.sectioningNode
(2) Node Section.firstContentNode
```

In general, an implementation will have to store at least two node references
with each section object: (1) a reference to the sectioning node, and (2) a
reference to the section's first content node.

If all sectioning nodes would have to be associated with their own section,
then a sectioning node counts as the first content node of the corresponding
section. And, because of that, the `firstContentNode` property would have to
be used to reference the section's first actual content node, instead of its
very first node. That is, in order to bypass having to distinguish between
the different types of sectioning nodes. Consequently, the referenced node
may itself be strictly associated with a subsection. As such, these properties
can be seen to be in conflict with such a design decision.

In contrary to that, and when not associating any sectioning node with its
own section, the `firstContentNode` property will always correspond with the
section's very first node.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
The `firstContentNode` property.

Note that this consideration assumes that no sectioning node belongs to
its own section. The following clarifications would otherwise not be true.

**CLARIFICATION**
Any non-empty section always has one or more strictly associated nodes.
That is, the `parentSection` property of these strictly associated nodes
holds a reference to the corresponding non-empty section.

That is because if a non-empty section has no subsections, then it contains
at least one inactive node that is strictly associated with it. If a non-empty
section contains subsections, then such a parent section will (also) contain
the strictly associated sectioning nodes of its immediate subsections.

**CLARIFICATION**
The very first node of a section always is strictly associated with it. Put
differently, a section has no implicitly associated node that is presequent
to its first strictly associated node.

In order to begin with an implicitly associated node, the very first node would
have to be strictly associated with a subsection. But, as no sectioning node
belongs to its own section, a section's very first node can never be strictly
associated with one of the parent section's subsections.

Consequently, and even if each node is associated with one section only, the
`firstContentNode` property will always hold a reference to a section's first
content node. In addition to that, this node always is identical to the
section's first top-level node (i.e. critical to transformations).

* (/see/ "reduced sequences" /)

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Any sectioning node must be associated with the parent section
of the section it declares. There is no room for any exception!
