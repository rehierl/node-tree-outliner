
<!-- ======================================================================= -->
# Associations (2)

This section builds upon the fundamental definitions and considerations based on
conclusions mentioned earlier.

<!-- ======================================================================= -->
## Sections (2)

A consequence of the states a section has is, that definitions only need to tell
an algorithm, with which node a section begins and with which node it ends.
Because of that, a section is a subsequence of the corresponding node sequence.
Therefore, ...

**CLARIFICATION** A section is a sequence of strictly subsequent nodes.

In addition to that, a first child node is strictly subsequent to its parent.
Consequently, the next sibling of a parent node can only be loosely subsequent
to it. That is, because a node can only be a parent node, if it has at least one
child node. No sibling can therefore be strictly subsequent to any parent node.

Consequently, the very first node of a section, is not necessarily strictly
subsequent to its sectioning node.

*Scope of a section*

The "scope of a section", respectively the scope of a sectioning node, can be
understood to be the range of strictly subsequent nodes that must be associated
with a section. The scope of a section therefore begins with a section's first
and ends with a section's last node.

Consequently, any non-empty section has a non-empty scope. The scope of an empty
section is said to be empty. However, an empty section can also be seen to have
no scope at all.

<!-- ======================================================================= -->
## Sectioning nodes (2)

As stated before, additional rules are required to tell an algorithm when to
begin and when to end associating nodes with a section. In addition to that,
it must be taken into account that an algorithm needs to have the means to
execute the corresponding operations when entering or exiting certain nodes.

The most distinctive characteristic of a section is the definition of its first
node.

Because of that, the first node of a section is defined in
relation to the corresponding sectioning node. After
that, the last possible node is defined in relation to the first node and in
such a way, that the initially mentioned requirements can still be fulfilled.

Consequently, the general definitions mentioned below define the default scope
for certain types of sectioning nodes. However, it is still allowed to define
additional characteristics (e.g. rank of a heading) which further limit the
scope of a presequent sectioning node.

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

*type-1 sections*

The very first subsequent node that could possibly be associated with a section
is the first child of a sectioning node. That is, because it is unreasonable to
associate a sectioning node with its own section.

A section will be referred to as a "type-1 section", if its scope begins with
the first child of its sectioning node. Consequently, a sectioning node that
declares a type-1 section will be referred to as a "type-1 sectioning node".

*type-2 sections*

The next reasonable subsequent node is the next sibling of a sectioning node.

Because of that, a section that begins with the next sibling of its sectioning
node will be referred to as a "type-2 section". Consequently, a sectioning node
that declares a type-2 section will be referred to as a "type-2 sectioning node".

### Type-1 sectioning nodes

`<container> A </container> B`

*first node*

An algorithm must mark a type-1 section as being open, before the enter event
of a type-1 sectioning node is being exited. Because of that, the scope of a
type-1 section begins with the first child of its sectioning node.

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
## Node sequence (2)

**TODO** -
can a node be allowed to have any effect on itself
(e.g. associate with its own section)?
