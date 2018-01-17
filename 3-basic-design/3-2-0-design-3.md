
<!-- ======================================================================= -->
# Design (3) - sectioning nodes

Because a section is a sequence of strictly subsequent nodes, definitions
only need to tell an algorithm when a section begins and when it ends. In
addition to that, an algorithm must have the means to implement the
corresponding operations efficiently, or even at all.

Because an algorithm knows about a section as soon as it enters the section's
sectioning node, it has the ability to execute operations that prepare itself
for the association of the first content node (e.g. change a section's state
to "open" when entering or exiting the section's sectioning node).

The use of the sectioning node's enter or exit event is, by itself, not
a requirement for the definition of a certain type of sectioning node.
Technically, the sectioning node's enter event and any event subsequent
to it could be used to open the declared section.

However, an algorithm must know which event exactly it has to use. Because
of that, the relationship of the sectioning node and the section's first
content node must be clearly and unambiguously defined.

Note that the definition of a sectioning node can in principle only define
one effective open event. Multiple open events do not necessarily represent
a design error because an open operation, executed on an already open section,
is ineffective. That is, because it won't further change the section's state.

However, it must not be possible to close a section before the execution of a
second subsequent open event. This would represent a design error as this would
obviously represent an attempt to re-open a section that is already closed.

<!-- ======================================================================= -->
## type-1, first child

Because a sectioning node does not belong to its own section, the very first
node that could possibly be associated with a section is the first child of
a sectioning node.

**DEFINITION**
A section will be referred to as a "type-1 section", if its scope begins with
the first child of its sectioning node. Consequently, a sectioning node that
declares a type-1 section will be referred to as a "type-1 sectioning node".

**CLARIFICATION**
An algorithm must open a type-1 section when it is about to exit the
sectioning node's enter event. Put differently, the sectioning node's
enter event represents the section's open event.

**CLARIFICATION**
A type-1 section is empty, if its sectioning node has no child nodes.

Note that, in an unordered tree of nodes, a parent node has no first child.
All child nodes are considered to be equal.

**CLARIFICATION**
The root node is a type-1 sectioning node.

As mentioned before, the root node must declare its own section. In addition
to that, even the first child of the root must belong to the root section.
That is, because every node in a tree must belong to at least one section
which is declared within the current tree. Consequently, the root node
matches the definition of a type-1 sectioning node.

<!-- ======================================================================= -->
## type-2, next sibling

Likewise, an algorithm can easily implement a rule that defines the next
sibling of a sectioning node as the section's first node.

**DEFINITION**
A section will be referred to as a "type-2 section", if its scope begins with
the next sibling of its sectioning node. Consequently, a sectioning node that
declares a type-2 section will be referred to as a "type-2 sectioning node".

**CLARIFICATION**
An algorithm must open a type-2 section when it is about to exit the sectioning
node's exit event. Put differently, the sectioning node's exit event represents
the section's open event.

Note that, because the descendants of a type-2 sectioning node are entered
before the section's open event is executed, the sectioning node's descendants
do not contribute to the content of the declared type-2 section. In other words,
these nodes are not understood to represent content nodes of the declared
section, but content nodes of those sections with which the sectioning node
is associated.

**CLARIFICATION**
Authors need to be aware that, due to this strict definition (i.e. "next
sibling"), the placement of a type-2 sectioning node is significant to a
type-2 section.

**CLARIFICATION**
A type-2 section is empty, if its sectioning node has no next sibling.

Note that a type-2  section is non-empty, if the sectioning node has a next
sibling, regardless of what type of node the next sibling is (i.e. whether
the next sibling represents meaningful content or not, e.g. a whitespace node).

Note that this definition requires an ordered tree of nodes. That is, because
in an unordered tree, no node has one specific next sibling. All siblings are
considered to be equal - even the presequent ones.

Attempting to use this strict definition in an unordered tree will not allow
deterministic results. That is, because siblings are not guaranteed to be
served in any particular order. Subsequent runs will produce different results
(e.g. different number of nodes for a specific section). Because of that, all
siblings would have to belong to a type-2 section. Consequently, and with
regards to an unordered tree, type-2 sectioning nodes would be similar to
type-1 sectioning nodes.

**DEFINITION**
A type-2 sectioning node must not contain any active nodes as one of its
descendant nodes. The data defined by the descendants of a type-2 sectioning
node must only be used to initialize the declared section (i.e. set certain
properties of the declared section).

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Type-1 and type-2 sectioning nodes add no additional requirement to the
structure of a node tree. That is, because the section's open event is
the corresponding event of the section's sectioning node. As such, the
"open" operation does not require any additional node, or any specific
node structure.

Note that using the enter event of the first content node to open a
declared section would add the requirement that a section would always
need at least one node. That is, such a section could never be empty.

**CLARIFICATION**
The first node's enter event is said to be strictly subsequent
to the corresponding event of the sectioning node.

Unless further types of sectioning nodes are defined, the first node of a
section is strictly subsequent to the corresponding event of the sectioning
node. That is, no other event will be executed after the sectioning node's
event was exited and before the first node is entered.

**CLARIFICATION**
The first node's enter event is not necessarily strictly subsequent
to the sectioning node's enter event.

The next sibling of a parent can only be loosely subsequent to it. That is,
because a node can only be a parent node, if it has at least one child node.
No sibling can therefore be strictly subsequent to a parent node.

Because of that, the first node of a section is strictly subsequent to
a sectioning node, if it is also the sectioning node's first child.

In contrary to that, the first node of a section is only loosely subsequent
to its sectioning node, if it is the sectioning node's next sibling and if the
sectioning node is a parent node.

Put differently, type-2 sectioning nodes allow any number of events in between
the sectioning node's enter event and the first node's enter event.

<!-- ======================================================================= -->
## why no loose type-2 definition?

Would it be reasonable to loosely define a type of section as "begins with the
'next subsequent' node" instead of the above strict definition (i.e. "begins
with the next sibling").

() Reader libraries tend to create implicit whitespace nodes. Because of
that, if an implicit whitespace node would immediately follow a loosely
defined sectioning node, then the intended next subsequent node would not
be the next sibling of an ancestor. That is, because that whitespace node
would be the next sibling. Consequently, and in order to truly support a
loose definition, those whitespace nodes would have to be taken into account.

() A strict type-2 sectioning node, if it has no next sibling, can still
have nodes that are subsequent to its exit event (i.e. the next sibling of
one of its ancestors). After all, once a section is marked as being open
by the sectioning node's exit event, the section remains to be open until
it is closed. Because of that, a loose definition combines in itself, multiple
strict definitions (i.e. "next sibling", "the parent's next sibling", etc).
A loose definition would therefore mean that the semantics of a sectioning
node would depend on nodes that are subsequent to it. Put differently,
subsequent nodes would be allowed to have an effect on presequent nodes.

() Additional logic would always be required in order to traverse from the
sectioning node to the first node, or vice versa. That is, the potentially
greater "distance" between those two nodes would always have to be taken
into account.

() Because the previous sibling of the first node could potentially be an
ancestor of the sectioning node, there would have to be a clear reason as
to why that ancestor is not supposed to be the actual sectioning node.

Consequently, a certain amount of "symmetry" needs to be taken into account
when defining sectioning nodes. After all, it does not make much sense to
define an additional type of sectioning nodes, if it would only be slightly
different to an existing one.

() It does matter, where the sectioning node and the section's first node is
located. Both can be seen to define the "location" of a section, and, as such
the relationship with other sections. Consequently, the corresponding statements
can be understood to be in conflict with each other, if both nodes turn out to
have different parent nodes.

Note that this can also be understood to indicate that all sections must be
strongly connected. That is, a section must not be allowed to contain any gaps
at all, not even in between a section's sectioning node and its first node.

() Such a definition would disallow consistent transformations. In general,
type-2 patterns can be transformed into type-1 patterns by grouping all the
nodes of a type-2 section as descendants of a type-1 sectioning node.
(forwards) Where would such a type-1 sectioning node have to be placed, if it
were supposed to replace the pattern of a loose definition? At the location of
the sectioning node, or at the location of the first node?
(backwards) If, in addition to that, the injected type-1 sectioning node would
have to be replaced by the initial pattern, the resulting structure would then
be different to the initial structure. That is, the result of subsequent
transformations is not guaranteed to be semantically equivalent to the initial
structure. After all, the information of the distance between the sectioning
node and the first node would no longer be available.

**CLARIFICATION**
A loose type-2 definition is insufficient to guarantee consistent dynamic
support. Because of that, a strict type-2 definition is required.

<!-- ======================================================================= -->
## other possible first nodes

Attempting to define any other type of node, as a section's first node, will
add additional requirements. Apart from the additional effort needed to detect
when to actually begin associating subsequent nodes with a section, an
implementation would also have to take into account that, due to an user/input
error, the structure of a tree could be in conflict with these requirements.

In order to justify these additional requirements, a definition would need
to have a clear reason as to why certain nodes (i.e. those in between the
sectioning node and the section's first node) would have to be excluded.
That is, the semantics of these unrelated nodes must be defined separately
and with regards to the declared section. Because of that, such an attempt
is, although technically possible, ill advised.

### second sibling

As mentioned above, type-2 sectioning nodes define the next sibling of the
sectioning node to be the first node of the declared section. As such, there
must be a definition that clarifies what the semantics of the sectioning node's
descendants are with regards to the declared section.

`<type-2> A </type-2> B C`

Here, node `B` will be the 1st and `C` the 2nd node of the declared section.
Because of that, node `A` can be understood to represent data that can be
used to initialize the declared section:

```
// while exiting "type-2"
section = new Section("A")
knownSections.add(section)
section.open()
```

Note that node `A` does not necessarily have to be a single node. Node `A` can
represent a whole subtree of nodes, or even a sequence of such subtrees, which
must all be inactive with regards to the design. That is, no node within subtree
`A` must be allowed to have any effect on predeclared sections, or declare new
sections of their own.

If node `C` would have to become the section's actual 1st content node, then
node `B` would need to have semantics defined with regards to the declared
section. That is, `B`'s semantics would have to be similar to those of node
`A`. Because of that, the definition of an additional subtree that has similar
semantics to node `A`, does not justify the additional requirements that would
have to be met because of having to skip subtree `B`.

Consequently, defining any other subsequent sibling as the section's first node
is unreasonable, because any node in the sequence of skipped nodes could easily
be added as descendants of the sectioning node.

### second child

Type-1 sectioning nodes define the first child of the sectioning node to be the
first node of the declared section. Because of that, these type of nodes can
themselves not support any data that can be used to set any section properties.

`<type-1> A B </type-1> C`

However, the first child of the sectioning node could be used to specify data
that could be used to set section properties before any node will be associated.

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
then be understood to be the actual sectioning node.

Out of all the other options, and because a type-1 sectioning node does itself
not support any configuration data, this option could be seen to be reasonable
enough to justify the above mentioned additional constraints.

Note the HTML `<header>` element.

### next sibling of an ancestor

Although not every node is guaranteed to have an ancestor node (i.e. the root
node), an algorithm technically has the means to mark a section as being open,
as soon as one of the sectioning node's ancestors is about to be exited.
However, this would add additional difficulty to a clear definition of such a
sectioning node.

`<container> ... <A:type-x/> ... <B:type-x/> ... </container> C`

That is, because there would have to be a clear answer as to which section node
`C` would have to belong, if a child contains multiple sectioning nodes of this
type. In addition to that, the corresponding ancestor could also be understood
to represent the actual sectioning node.

### other options

Although there are even further ways to define the first node of a section (e.g.
variable relationship, descendants of children or siblings, etc.), it seems that
the more intricate the relationship between a sectioning node and the section's
first node is, the more questions would have to be clearly answered in order to
unambiguously define any additional section type.
