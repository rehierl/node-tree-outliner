
<!-- ======================================================================= -->
# Design (6) - associating sectioning nodes

<!-- ======================================================================= -->
## sectioning nodes ()

**CLARIFICATION**
A sectioning node does not belong to its own section:
Provides a "physical" connection to the subsection's parent section.

i.e. the defining node of a section's location -
strongly connected

describe the purpose of a sectioning node inside of presequent sections -
not associated with its declared section

<!-- ======================================================================= -->
## sectioning nodes ()

**CLARIFICATION**
A sectioning node does not belong to its own section:
Multi-step transformations.

**TODO** -
a practical issue -
transformations

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Fundamental considerations.

* All nodes must be associated while they are being entered.

See the introduction to sectioning nodes:

* Associating sectioning nodes with their own section adds the
  sectioning to its own context, even though a sectioning node
  is not presequent to itself.
* From a strict perspective, a section would not be subsequent to
  its sectioning node. That is, because the sectioning node would
  then be the section's very first node.
* No section would ever be truly empty. That is, because any section
  would then always have at least one node (i.e. the sectioning node)
  that is strictly associated with it.

See the definition of the section states/events:

* Associating sectioning nodes with their own section can be seen to be
  in conflict with a section's open event. That is, because nodes would
  have to be associated before a section can even count as being open.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Less confusion with regards to a discussion.

If sectioning nodes would have to be associated with their own sections,
then there would always be the difficulty of having to distinguish between
(1) the first node that is associated with a section, which then is the
section's sectioning node, and (2) the section's first actual content node.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Technically allows to prematurely close a type-1 section.

If a type-1 sectioning node would have to be associated with its own section,
then all of its descendants would also automatically belong to the declared
section. Consequently, and because of implicit associations, it would not be
possible for a type-1 section to end inside of a type-1 sectioning node.

Not associating sectioning nodes with their own section, therefore technically
allows a type-1 section to end inside of its sectioning node. However, this
does not mean that it would be reasonable to let a type-1 section end before
its sectioning node is being exited. Not associating sectioning nodes with
their own section merely does not disallow such an option.

Apart from that, allowing a type-1 section to end inside of its sectioning
node would require to allow having nodes that are not supposed to belong to
the declared section. Consequently, the type-1 definition of an ordered tree
would have to be inconsistent with the type-1 definition of an unordered tree.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Description of the general properties of a section.

If a sectioning node would have to be associated with its own section, then the
sectioning node and all of its descendants would also automatically belong to
the declared section. It would therefore not be possible to describe the general
properties of a section's node sequence (see: reduced sequence) independently
of the corresponding sectioning node.

That is, because the index of the first actual content node within the section's
node sequence would then not be the same for all section types. That is, because
a section's node sequence would then always begin with the section's sectioning
node, which is then can be followed by one or more intermediate nodes, which are
then followed by the section's actual content nodes.

Note that this is also an implementation specific aspect. That is, because
when a type-2 sectioning node would have to be associated with its own section,
an implementation would have to store a reference to the section's first actual
content node in order to bypass having to distinguish between the different
types of sections.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Consistency with regards to the parent container of a section.

That is, the parent container of a type-1 section, which is identical to a
type-1 sectioning node, would then also belong to the type-1 section. In
contrary to that, the parent container of a type-2 section, which is not
identical to a type-2 sectioning node, would still belong to a section that
is presequent to the declared type-2 section.

Note that the parent container of a type-2 section must not belong to a
type-2 section, as it would implicitly associate any node that is presequent
to the sectioning node of a declared type-2 section.

In other words: Some parent containers would belong to a declared section,
but others would not.

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
Non-Empty parent sections.

If all sectioning nodes would have to be associated with their own section,
then a section's sectioning node (and possibly also its descendant nodes)
would have to be skipped in order to reach the first actual content node.

Note that, in such a case, it would obviously help to have two references:
(1) a reference to the sectioning node, and (2) a reference to the first
content node. However, this does not change the fact that the sectioning
node still counts as the section's first node. Consequently, the reference
to the first content node represents an attempt to bypass the section's
first node. That is, it represents on its own some inconsistency with such
a design decision.

```
(1) Node Section.sectioningNode
(2) Node Section.firstContentNode
```

A parent section, that only contains a single subsection, but no actual content
nodes of its own, would then appear to have no meaningful content. That is, the
corresponding section would appear to be empty. And, because of that, one would
always also have to explicitly check for the existence of possible subsections.

Note that the sectioning node of a subsection would then only be associated
with the subsection it declares. That is, because each node can and will
be associated with one section only. Despite that, a sectioning node still
counts as being implicitly associated with all of its ancestor sections.

Note that the focus of this consideration is that additional tests would be
necessary in order to reliably tell whether a section has meaningful content
or not. A reference to the section's first actual content node won't change
that.

With that regards, the advantage of not associating a sectioning node with its
own section therefore is that no parent section will ever appear to be empty.
A parent section will always have at least one content node and, because of
that, can never be misunderstood to be empty.

Note that, in this case, the reference of the sectioning node provides a
"physical" connection with the section's parent section. In addition to that,
the reference to the section's first content node then corresponds with the
section's first node.

That is, there is no need to check the existence of possible subsections, if
the only question that needs to be answered is, whether the parent section
is empty or not. One only needs to check, if a node exists that is strictly
associated with the corresponding section.

* has subsections => has strictly associates nodes => not empty
* not empty => does not necessarily have subsections
* has no strictly associated nodes => empty

<!-- ======================================================================= -->
## sectioning nodes

**CLARIFICATION**
A sectioning node does not belong to its own section:
A consistent `Section Node.parentSection` property.

In general, a `parent` property has a clear orientation: from a subordinate
entity towards an entity that is superordinate to it (hence the word "parent").
In short: The general orientation of a `parent` property is "upwards".

In this context, the direction which is consistent with this general
orientation is from a subsequent node towards one that is presequent
to it. To be more accurate: towards a node that is within its context.

Note that, no presequent node is considered to be subordinate to any node
that is subsequent to it. A superordinate node (i.e. a parent node) always
is presequent to those that are subordinate to it (i.e. its descendants).

Associating a sectioning node with its own section will obviously be in
conflict with this general orientation. That is, because it would connect a
superordinate entity (i.e. the sectioning node) with one that is subordinate
to it (i.e. the declared section). Because of that, and with regards to a
sectioning node, the property's direction would be turned upside-down as it
would point from a presequent node towards nodes that are subsequent to it
(i.e. its content nodes). That is, the property's orientation is in such a
case not upwards. Consequently, additional logic would always be required in
order to take the property's different orientations into account (e.g. when
entering and traversing the sections).

Note that the parent property, with regards to the descendants of a type-2
sectioning node, obviously needs to be consistent with its ancestor (i.e.
the sectioning node), regardless if sectioning nodes are associate with
their sections or not. That is, because of descendant nodes being implicitly
associated with the sections of their ancestors.

Note that the direction of the above property, with regards to all other
nodes, is guaranteed to be consistent with the afore mentioned orientation.
That is, because they must be associated with the section of a presequent
sectioning node.

Not associating all sectioning nodes with their own section guarantees that
the orientation of this property is always consistent with regards to all
nodes in the corresponding tree. That is, the `parentSection` property will
always point upwards.

Note that the focus here is to have a consistent definition of the above
mentioned property and consequently allow to use it in a consistent manner.
Any inconsistency is prone to be misunderstood and thus, prone to trigger
implementation errors.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The sectioning node of a node's parent section
never is identical to the corresponding node itself.

```
(node.parentSection.sectioningNode !== node)
```

That is obviously true for any node which is not a sectioning node. However,
this expression is also true if the node in question is a sectioning node.
That is, because no such node is associated with the section it declares.

**CLARIFICATION**
The parent section of a node's parent section is identical
to the parent section of the corresponding sectioning node.

```
section = node.parentSection
(section.parentSection === section.sectioningNode.parentSection)
```

The focus of this expression is that the corresponding associations must be
consistent with each other. That is, the sectioning node's parent section
must correspond with the parent section of the section it declares.
