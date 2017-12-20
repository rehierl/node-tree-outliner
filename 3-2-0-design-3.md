
<!-- ======================================================================= -->
# Design (3) - Sectioning nodes

Because a section is a sequence of strictly subsequent nodes, definitions only
need to tell an algorithm, with which node a section begins and with which node
it ends. In addition to that, an algorithm must have the means to implement the
corresponding operations efficiently, or even at all.

Because an algorithm knows about a section as soon as it enters the section's
sectioning node, it has the ability to execute operations that prepare itself
for the association of the first node (e.g. mark a section as being "open").
That is, either when entering or when exiting the sectioning node.

The use of the sectioning node's enter or exit event is, by itself, not a
requirement for the definition of a certain type of sectioning nodes. That is,
in theory, any subsequent event could be used. However, an algorithm must know
which event exactly it has to use. Because of that, the relationship of the
sectioning node and the section's first node must be clearly defined.

Note that, the definition of a sectioning node can, in principle, only define
one effective open event, during which the declared section has to be marked as
being "open". Multiple such events do not necessarily represent a design flaw
because an open command executed on an already open section won't change the
section's state. However, it must not be possible to close a section before the
execution of a second subsequent open command, as this would represent a design
error. It must not be allowed to re-open an already closed section.

<!-- ======================================================================= -->
## type-1, first child

Because a sectioning node does not belong to its own section, the very first
node that could possibly be associated with a section is the first child of a
sectioning node.

All an algorithm has to do in such a case is to mark the declared section as
being open when it is about to exit the sectioning node's enter event.

**DEFINITION**
A section will be referred to as a "type-1 section", if its scope begins with
the first child of its sectioning node. Consequently, a sectioning node that
declares a type-1 section will be referred to as a "type-1 sectioning node".

**CLARIFICATION**
A type-1 section is empty, if its sectioning node has no child nodes.

Note that, in an unordered tree of nodes, any child would have to belong to
a type-1 section. That is, because there is no guarantee that a certain child
will be a parent's first child. All child nodes are considered to be equal.

**CLARIFICATION**
The root node is a type-1 sectioning node.

That is, because the root's first child must belong to the declared section. In
addition to that, there are no outer nodes that are subsequent to it. Because of
that, no other type of sectioning node can match the root node.

<!-- ======================================================================= -->
## type-2, next sibling

Likewise, an algorithm can easily implement a rule that defines the next
sibling of a sectioning node as the section's first node.

All an algorithm has to do in such a case is to mark the declared section
as being open when it is about to exit the sectioning node's exit event.

**DEFINITION**
A section will be referred to as a "type-2 section", if its scope begins with
the next sibling of its sectioning node. Consequently, a sectioning node that
declares a type-2 section will be referred to as a "type-2 sectioning node".

**CLARIFICATION**
Authors need to be aware that, due to the strict definition (i.e. "next
sibling"), the placement of a type-2 sectioning node is significant to
the section of a sectioning node.

**CLARIFICATION**
A type-2 section is empty, if its sectioning node has no next sibling. Put
differently, a type-2 section is non-empty, if the sectioning node has a next
sibling. The latter is true, whether this next sibling represents meaningful
content or not (e.g. whitespace node).

Note that this definition requires an ordered tree of nodes. That is, because
in an unordered tree, no node has one specific next sibling. All siblings are
considered to be equal.

Attempting to use this strict definition in an unordered tree will not allow
deterministic results. That is, because siblings are not guaranteed to be
served in any particular order. Subsequent runs will produce different results
(e.g. different number of nodes for a specific section). Because of that, all
siblings would have to belong to a type-2 section. Consequently, and in an
unordered tree, type-2 sectioning nodes would not be much different to type-1
sectioning nodes.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Type-1 and type-2 sectioning nodes force no pattern upon a tree's structure.

That is, the declared section is empty, if the sectioning node has, depending
on its definition, no first child or no next sibling. Because of that, both
definitions do not force that the tree must have a specific structure.

**CLARIFICATION**
The sectioning node's event is strictly presequent
to the first node's enter event.

Unless further types of sections are defined, the first node of a section is
strictly subsequent to the corresponding event of the sectioning node. That is,
no other event will be executed after the sectioning node's event was exited
and before the first node is entered.

**CLARIFICATION**
The sectioning node's enter event is not necessarily strictly presequent
to the first node's enter event.

The next sibling of a parent can only be loosely subsequent to it. That is,
because a node can only be a parent node, if it has at least one child node.
No sibling can therefore be strictly subsequent to a parent node.

Because of that, the first node of a section is strictly subsequent to
a sectioning node, if it is also the sectioning node's first child.

In contrary to that, the first node of a section is only loosely subsequent
to a sectioning node, if it is the sectioning node's next sibling and if the
sectioning node is a parent node.

Put differently, type-2 sectioning nodes allow any number of events in between
the sectioning node's enter event and the first node's enter event.

<!-- ======================================================================= -->
## Why no loose type-2 definition?

Would it be reasonable to loosely define a type of section as "begins with the
'next subsequent' node" instead of the above strict definition (i.e. "begins
with the next sibling").

() Reader libraries tend to create implicit whitespace nodes. Because of that,
if an implicit whitespace node would follow such a sectioning node, then the
next subsequent node would not be the next sibling of an ancestor. Consequently,
and in order to truly support a loose definition, those whitespace nodes would
have to be taken into account.

() A strict type-2 sectioning node, if it has no next sibling, can still have
nodes that are subsequent to its exit event (i.e. the next sibling of one of
its ancestors). After all, once a section is marked as being open inside of
the corresponding exit event, the section remains open until it is closed.
Because of that, a loose definition combines in itself, multiple strict
definitions (i.e. "next sibling", "the parent's next sibling", etc). This
essentially means, that the exact semantics of such a sectioning node depends
on missing subsequent nodes.

() Additional logic would always be required in order to traverse from the
sectioning node to the first node, or vice versa. That is, the potentially
greater distance between those two nodes would always have to be taken into
account.

() Because the previous sibling of the first node could be an ancestor of the
sectioning node, there would have to be a clear reason as to why that ancestor
is not supposed to be the actual sectioning node.

() It does matter, where the sectioning node and the section's first node is
located. Both can be seen to define a section's "location". Consequently, the
corresponding statements can be in conflict with each other (e.g. if both nodes
have different parent nodes).

() Such a definition would disallow consistent transformations. In general,
type-2 patterns can be transformed into type-1 patterns by grouping all the
nodes of a type-2 section as descendants of a type-1 sectioning node.
(forwards)
Where would such a type-1 sectioning node would have to be placed, if it
were supposed to replace the pattern of a loose definition? At the location
of the sectioning node, or at the first node of its section?
(backwards)
If, in addition to that, the inserted type-1 sectioning node would have to be
replaced with the initial pattern, the resulting structure would be different
to the initial structure. That is, the result of subsequent transformations is
not guaranteed to be semantically equivalent to the original structure. After
all, the information of the distance between the sectioning node and the first
node would no longer be available.

**CLARIFICATION**
A loose type-2 definition is insufficient to guarantee consistent dynamic
support. Because of that, a strict type-2 definition is a necessity.

<!-- ======================================================================= -->
## Other possible first nodes

Attempting to define any other type of node, as a section's first node, will
add additional requirements to a definition and to an implementation. Apart
from the additional effort needed to detect when to actually begin associating
subsequent nodes with a section, an implementation would also have to take into
account that the structure of a tree could violate these requirements.

In order to justify these additional requirements, a definition would need
to have a clear reason as to why certain nodes (i.e. those in between the
sectioning node and the section's first node) would have to be excluded.
That is, the semantics of these unrelated nodes must be defined separately
and with regards to the declared section. Because of that, such an attempt
is, although technically possible, ill advised.

### second sibling

As mentioned above, type-2 sectioning nodes define the next sibling of the
sectioning node to be the first node of the declared section. As such, there
must be a definition of what the semantics of the sectioning node's descendants
are with regards to the declared section.

`<type-2> A </type-2> B C`

Here, node `B` will be the 1st and `C` the 2nd node of the declared section.
Because of that, node `A` can be understood to represent data that can be
used to initialize the section that is declared by the sectioning node:

```
// while exiting "type-2"
section = new Section("A")
knownSections.add(section)
section.open()
```

Note that node `A` does not necessarily have to be a single node. As such, node
`A` can represent a whole subtree of nodes, or even a sequence of such subtrees,
which must all be inactive with regards to the design. That is, no node within
subtree `A` must be allowed to have any effect on predeclared sections, or
declare new sections themselves.

If node `C` would have to become the section's actual 1st node, then node `B`
would need to have semantics defined with regards to the declared section. That
is, `B`'s semantics would have to be similar to those of node `A`. Because of
that, the definition of a 2nd subtree that has similar semantics to node `A`,
does not justify the additional requirements that would have to be met because
of having to skip subtree `B`.

Consequently, defining any other subsequent sibling as the section's first node
is unreasonable, because any node in the sequence of skipped nodes could easily
be added as descendants of the sectioning node.

### second child

Type-1 sectioning nodes define the first child of the sectioning node to be the
first node of the declared section. Because of that, these type of nodes can not
themselves support any data that can be used to set any section properties.

`<type-1> A B </type-1> C`

However, the first child of the sectioning node could be used to specify data
that could be used to set such properties before any node will be associated
with the corresponding section.

```
// while entering "type-1"
section = new Section()
knownSections.add(section)

// while exiting "A"
section.configure("A")
section.open()
```

In such a case, the question would have to be answered as to why node `A` must
not be associated with the declared section. After all, even if the above data
container `A` would be associated with that section, it could still be excluded
from a subsequent process (e.g. excluded from being displayed).

`<container> <type-2> A </type-2> B </container> C`

In addition to that, there needs to be sufficient reason to choose this pattern
over the pattern of a type-2 sectioning node. That is, because subtree `A` could
then be understood to be the actual sectioning node. Consequently, there always
is a certain amount of symmetry that needs to be taken into account when
defining additional types of sectioning nodes.

Out of all the other options, and because a type-1 sectioning node does not
support any configuration data, this option could be seen to be reasonable
enough to justify the above mentioned additional constraints.

Note the HTML `<header>` element.

### next sibling of an ancestor

Although not every node is guaranteed to have an ancestor node, an algorithm
technically has the means to begin with associating nodes, if one of the
sectioning node's ancestors was exited. However, this would add additional
difficulty to a clear definition of such a sectioning node.

`<container> ... <A:type-x/> ... <B:type-x/> ... </container> C`

That is, because there would have to be a clear answer as to which section node
`C` would have to belong, if a child contains multiple sectioning nodes of this
type. In addition to that, the corresponding ancestor could then be understood
to be the actual sectioning node.

### further options

Although there are even further ways to define the first node of a section (e.g.
variable relationship, descendants of siblings or children, etc.), it seems that
the more intricate the relationship between a sectioning node and the section's
first node is, the more questions would have to be answered in order to clearly
define an additional section type.
