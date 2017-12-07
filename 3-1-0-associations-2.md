
<!-- ======================================================================= -->
# Associations (2)

This section builds upon the fundamental definitions, considerations and
conclusions mentioned previously.

<!-- ======================================================================= -->
## Sections (2)

**CLARIFICATION**
Nodes must be associated with sections while they are being entered.

That is, because otherwise the location of a node (with regards to a tree's
sections) could be affected by nodes that are subsequent to it. Because of that,
a node could then be affected by nodes that are not within its actual context,
which would consequently be in conflict with the definition of the context of
a node.

**CLARIFICATION**
A section is a sequence of strictly subsequent nodes.

A consequence of the states a section has is, that definitions only need to
tell an algorithm, with which node a section begins and with which node it ends.
Because of that, a section is a subsequence of the corresponding node sequence.
Consequently, a section is a sequence of strictly subsequent nodes. That is, a
section has no gaps in between its nodes.

However, this statement requires that all the nodes are being associated with
their sections while they are being entered. That is, because exit events are
executed in reversed order.

<!-- ======================================================================= -->
## Sectioning nodes - first node (2)

As stated before, additional rules are required to tell an algorithm when to
begin associating nodes with a section. In addition to that, an algorithm must
have the means to implement the corresponding operations efficiently.

Because an algorithm knows about a section as soon as it enters the section's
sectioning node, it has the ability to execute operations that prepare itself
for the association of the section's first node (e.g. mark the section as being
open). That is, either when entering or when exiting the sectioning node.
Because of that, the first node of a section must be defined in terms of the
structural relationship it has with the sectioning node.

The very first node that could possibly be associated with a section is the
first child of a sectioning node. That is, because it is unreasonable to
associate a sectioning node with its own section. All an algorithm would have
to do in the case of such a sectioning node is to mark the declared section as
being open when it is about to exit the sectioning node's enter event.

**DEFINITION**
A section will be referred to as a "type-1 section", if its scope begins with
the first child of its sectioning node. Consequently, a sectioning node that
declares a type-1 section will be referred to as a "type-1 sectioning node".
("type-1" because the section's first node is the first subsequent node possible).

Likewise, an algorithm can easily implement a rule that defines the next sibling
of a sectioning node as the section's first node. All an algorithm would have to
do in the case of such a sectioning node is to mark the declared section as being
open when it is about to exit the sectioning node's exit event.

**DEFINITION**
A section will be referred to as a "type-2 section", if its scope begins with
the next sibling of its sectioning node. Consequently, a sectioning node that
declares a type-2 section will be referred to as a "type-2 sectioning node".
("type-2" because this first node is the 2nd easiest to implement option).

Note that these two definitions are independent of the tree's actual structure.
That is, the declared section is empty, if the sectioning node has, depending on
the type of the sectioning node, no first child or no next sibling. Consequently,
the corresponding tree is not required to have any specific structure.

The attempt to define any other node as a section's first node will undoubtedly
add additional requirements to a definition and to an implementation. Apart from
the difficulty to detect when to actually begin associating nodes with a section,
an implementation would also have to take into account that a given tree might
violate the required structure. In order to justify the additional requirements
for an implementation, a definition would need to have a clear reason as to why
certain nodes (i.e. those in between the sectioning node and the section's first
node) would have to be excluded. Because of that, such an attempt is, although
technically possible, ill advised.

### other descendant nodes

### other non-descendant nodes

<!-- ======================================================================= -->

Because a sectioning node can only be defined independently of any node tree,

Consequently, the general definitions mentioned below define the default scope
for certain types of sectioning nodes. However, it is still allowed to define
additional characteristics (e.g. rank of a heading) which further limit the
scope of a presequent sectioning node.

Attempting to define any other descendant node as the section's first node
would force a specific pattern upon the descendants. This would add unnecessary
difficulty to an implementation, because an algorithm would then have to be able
to detect when the section's actual first node is being entered.

Apart from that, there would have to be a definition of the relationship
between the intended first node and the sectioning node. In order to define
such a relationship independent of any node tree, the relationship would have
to be constant in nature. That is, because a variable relationship would require
additional semantics that would allow to explicitly markup the first node.
Because of that, an attempt to define any other node as the first node of such a
sectioning node does not seem to be reasonable.

In addition to that, the semantics of those nodes, that are subsequent to the
sectioning node and presequent to the first node, would have to be defined (i.e.
What meaning do these have with regards to the declared section?).

Finally, the previous sibling of the intended first node could then be seen as
the actual sectioning node (type-2). This would especially be the case, if the
sectioning node's first child node would be intended to represent a container
that would have to be used to hold section specific data (e.g. a title).

*node sequence*

```
ns := [...,gi,...,pi,...,ni,...,nj,...,pj,...,gj,...]
                       ...][ s1  ][ s2  ][ s3  ][...
exit events:                     ni     pi     gi
```

* `ni` represents the current sectioning node
* `[ni+1,nj]` contains all the descendants of `ni`
* `pi` represents the parent of node `ni`
* `[pi+1,pj]` contains all the descendants of `pi`
* `gi` represents the grandparent of `ni`
* `[gi+1,gj]` contains all the descendants of `gi`

### Type-1 sectioning nodes

`<container> A </container> B`

*first node*

An algorithm must mark a type-1 section as being open, before the enter event
of a type-1 sectioning node is being exited. Because of that, the scope of a
type-1 section begins with the first child of its sectioning node.

*last node*

### Type-2 sectioning nodes

`<container> A <data> B </data> C <container> D`

*first node*

An algorithm must mark a type-2 section as being open, before the exit event of
a type-2 sectioning node is being exited. Because of that, the scope of a type-2
section begins with the next sibling of its sectioning node.

*last node*

### Are there any other reasonable section types?

<!-- ======================================================================= -->
## Sections (3)

**CLARIFICATION**
The very first node of a section is not necessarily strictly subsequent to its
sectioning node.

The next sibling of a parent node can only be loosely subsequent to it. That is,
because a node can only be a parent node, if it has at least one child node. No
sibling can therefore be strictly subsequent to any parent node.

Because of that, the first node of a section is strictly subsequent to the
section's sectioning node, if it is also the sectioning node's first child node.
In contrary to that, the first node of a section is only loosely subsequent to
the section's sectioning node, if it is the sectioning node's next sibling and
if the sectioning node is a parent node.

<!-- ======================================================================= -->
## Node sequence (2)

**TODO** -
can a node be allowed to have any effect on itself
(e.g. associate with its own section)?