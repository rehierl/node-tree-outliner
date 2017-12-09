
<!-- ======================================================================= -->
# Associations (2)

This section builds upon the fundamental definitions, considerations and
conclusions mentioned previously.

<!-- ======================================================================= -->
## Sections (2)

**CLARIFICATION**
Any descendant of a node, that is associated with a section, also loosely
belongs to the very same section. Also, any node loosely belongs to any
section with which any of its ancestors is associated.

That is, because a semantically consistent path can be defined that
connects a section with any of the associated node's descendants.

Note that, if this statement would not be applicable/true, then there would
consequently be no definition for the term "descendant". That is, because the
definition of this term is also based upon the construction of a semantically
consistent path. In addition to that, the definition of the term "ancestor"
is derived from the definition of the term "descendant".

**CLARIFICATION**
Nodes must be associated with sections while they are being entered.

The order of a tree's traversal is dictated by the node order of a tree. That
is, the traversal of a tree must reflect the tree's semantics. Because exit
events will be executed in reverse order, associating any nodes while they are
being exited would constitute a deviation of the tree traversal's order and, as
such, a deviation of the tree's semantics. Consequently, associating nodes with
sections while they are being exited can not result in sections that accurately
represent the contents of a tree.

Also, the location of a node (with regards to a tree's sections) could otherwise
be affected by nodes that are subsequent to it. Because of that, a node could
then be affected by nodes that are not within its actual context, which would
consequently be in conflict with the definition of a node's context.

**CLARIFICATION**
A section is a sequence of strictly subsequent nodes.

A consequence of the states a section has is, that definitions only need to
tell an algorithm, with which node a section begins and with which node it ends.
Because of that, a section is a subsequence of the corresponding node sequence.
Consequently, a section is a sequence of strictly subsequent nodes.

Put differently, a section has no gaps in between its nodes. That is, any
subsequent node in between a section's first and last node is in relationship
with the corresponding section.

**CLARIFICATION**
The very first node of a section is not necessarily strictly subsequent to its
sectioning node.

The next sibling of a parent node can only be loosely subsequent to it. That is,
because a node can only be a parent node, if it has at least one child node. No
sibling can therefore be strictly subsequent to any parent node.

Because of that, the first node of a section is strictly subsequent to a
section's sectioning node, if it is also the sectioning node's first child node.
In contrary to that, the first node of a section is only loosely subsequent to
the section's sectioning node, if it is the sectioning node's next sibling and
if the sectioning node is a parent node.

<!-- ======================================================================= -->
## Sectioning nodes - first nodes (2)

As stated before, rules are required to tell an algorithm when to begin
associating nodes with a section. In addition to that, an algorithm must
have the means to implement the corresponding operations efficiently.

Because an algorithm knows about a section as soon as it enters the section's
sectioning node, it has the ability to execute operations that prepare itself
for the association of the section's first node (e.g. mark the section as being
open). That is, either when entering or when exiting the sectioning node.
Because of that, the first node of a section must be defined in terms of the
structural relationship that node has with the section's sectioning node.

The very first node that could possibly be associated with a section is the
first child of the sectioning node. That is, because it is unreasonable to
associate a sectioning node with its own section. All an algorithm would have
to do in the case of such a sectioning node is to mark the declared section
as being open when it is about to exit the sectioning node's enter event.

**DEFINITION**
A section will be referred to as a "type-1 section", if its scope begins with
the first child of its sectioning node. Consequently, a sectioning node that
declares a type-1 section will be referred to as a "type-1 sectioning node".
("type-1" because the section's first node is the first subsequent node
possible).

Likewise, an algorithm can easily implement a rule that defines the next sibling
of a sectioning node as the section's first node. All an algorithm would have
to do in the case of such a sectioning node is to mark the declared section as
being open when it is about to exit the sectioning node's exit event.

**DEFINITION**
A section will be referred to as a "type-2 section", if its scope begins with
the next sibling of its sectioning node. Consequently, a sectioning node that
declares a type-2 section will be referred to as a "type-2 sectioning node".
("type-2" because this first node is the 2nd easiest to implement option).

Note that these two definitions are independent of a tree's structure. That
is, the declared section is empty, if the sectioning node has, depending on the
type of the sectioning node, no first child or no next sibling. Because of that,
there is no constraint on the tree's structure.

<!-- ======================================================================= -->
## Unordered trees

Note that type-2 sections can only be defined, if the underlying tree is an
ordered tree of nodes. That is, because nodes in an unordered tree are not
guaranteed to have a dedicated next sibling, or even a dedicated first child.

Because of that, a sectioning node itself has no order with regards to any
of its siblings or children. Consequently, the result of an algorithm that
attempts to support type-2 section in such a tree would be non-deterministic
(i.e. subsequent runs can potentially produce different results).

Unordered trees can therefore only support type-1 sections.
That is, with the limitation that all child nodes are equal.

<!-- ======================================================================= -->
## Overview of other possible first nodes

Attempting to define any other type of node, as a section's first node, will add
secondary constraints to a definition and to an implementation. Apart from the
additional effort needed to detect when to actually begin associating subsequent
nodes with a section, an implementation would also have to take into account
that the structure of a given tree might not be as required.

In order to justify these constraints, a definition would need to have a clear
reason as to why certain nodes (i.e. those in between the sectioning node and
the section's first node) would have to be excluded. That is, the semantics of
these unrelated nodes must be defined separately and with regards to the declared
section. Because of that, such an attempt is, although technically possible, ill
advised.

### look ahead

In theory, an implementation has the ability to cheat the traversal of the node
tree by directly examining the tree's structure as soon as a certain sectioning
node is entered. Because of that, it could simply determine ahead of schedule,
if that sectioning node has for example a 2nd child, a 2nd subsequent sibling,
or even a any ancestors. Consequently, an algorithm can potentially configure
itself to act accordingly.

The downside of this kind of look ahead would be, that this ability would become
a requirement, if it could not be avoided. That is, implementations that can not
support any kind of look ahead (e.g. due to technical limitations), would become
impossible. However, if it is guaranteed that a section type can be supported
without such an approach, a look ahead could be used as the basis of a more
efficient implementation.

Despite that, a look ahead is an attempt to bypass the current knowledge that
is guaranteed by the traversal of the tree. As such, it represents an attempt
to predict future events.

Because of that, such an approach is ill advised.

### second sibling

As mentioned above, type-2 sectioning nodes define the next sibling of the
sectioning node to be the first node of the declared section. As such, there
must be a definition of what the semantics of the sectioning node's descendants
are with regards to the declared section. Otherwise, there would be no reason
to define any type-2 sectioning node at all.

`<type-2> A </type-2> B C`

Here, node `B` will be the 1st and `C` the 2nd node of the declared section.
Because of that, node `A` can be understood to represent data that can be used
to initialize the section declared by the current sectioning node:

```
// while exiting "type-2"
section = new Section("A")
knownSections.add(section)
section.open()
```

Note that node `A` does not necessarily have to be a single node. As such, node
`A` can represent a whole subtree of nodes, which all must be inactive with
regards to the algorithm. That is, no node within subtree `A` must be allowed
to have any effect on predeclared sections, or declare new sections themselves.

If node `C` would have to become the section's actual 1st node, then node `B`
would have to have semantics defined with regards to the declared section. That
is, `B`'s semantics would have to be similar to those of node `A`. Because of
that, the definition of a 2nd subtree that has similar semantics, does not
justify the additional requirements that would have to be met because of having
to skip subsequent subtree `B`.

Consequently, defining any other subsequent sibling as the section's first node
is unreasonable, because any node in the sequence of skipped nodes could easily
be added to subtree `A`.

### second child

Again, type-1 sectioning nodes define the first child of the sectioning node to
be the first node of the declared section. Because of that, these type of nodes
themselves can not support any data that can be used to initialize the declared
section.

`<type-1> A B </type-1> C`

However, the first child of the sectioning node could be understood to define
data that could be used to configure the declared section before any node will
be associated with it.

```
// while entering "type-1"
section = new Section()
knownSections.add(section)

// while exiting "A"
section.configure("A")
section.open()
```

But in that case, the question would have to be answered as to why node `A`
must not be associated with the declared section. After all, even if subtree
`A` would be associated with that section, it could still be excluded from a
subsequent process (e.g. excluded from being displayed).

`<container> <type-2> A </type-2> B </container> C`

In addition to that, there needs to be sufficient reason to choose this
pattern over the pattern of a type-2 definition. That is, because subtree
`A` could then be understood to be the actual sectioning node.

Out of all the other options, and because a type-1 sectioning node does not
support any initializational data, this option could be seen to be reasonable
enough to justify the above mentioned additional constraints.

### next sibling of an ancestor

Although not every node is guaranteed to have an ancestor node, an algorithm
is technically allowed to begin associating nodes with a declared section, if
one of its ancestor nodes is exited.

`<container> ... <type-x> A ... </type-x> B ... </container> C`

Because of that, nodes `A` and `B` could be used for initializational data.
This, however, would add additional difficulty to a clear definition of such
data.

`<container> ... <type-x> ... <type-x> ... </container> C`

Also, there would have to be a clear answer, as to which section node `C` would
belong, if a child contains multiple sectioning nodes of this type. In addition
to that, the corresponding ancestor could then be understood to be the actual
sectioning node.

### further options

Although there are even further ways to define the first node of a section (e.g.
variable relationship, descendants of siblings or children, etc.), it seems that
the more intricate the relationship between a sectioning node and the section's
first node is, the more questions would have to be answered in order to clearly
define an additional section type.
