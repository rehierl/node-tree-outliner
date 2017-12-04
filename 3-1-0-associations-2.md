
<!-- ======================================================================= -->
## Sections (2)

A consequence of the states of a section is, that definitions only need to
tell an algorithm, where a section begins and where it ends. Because of that,
a section is a subsequence of the corresponding node sequence. Therefore, ...

**CLARIFICATION** A section is a sequence of strictly subsequent nodes.

In addition to that, a first child node is strictly subsequent to its parent.
Consequently, the next sibling of a parent node can only be loosely subsequent
to that parent node. That is, because a node can only be a parent node, if it
has at least one child node. No sibling can therefore be strictly subsequent
to any parent node.

Consequently, the very first node of a section, is not necessarily strictly
subsequent to its sectioning node.

*Scope of a section*

The "scope of a section", respectively the scope of a sectioning node, can be
understood to be the range of subsequent nodes that must be associated with a
section. The scope of a section therefore begins with a section's first and
ends with a section's last node.

Consequently, any non-empty section has a non-empty scope. The scope of an empty
section is said to be empty. An empty section can also be seen to have no scope.

<!-- ======================================================================= -->
## Sectioning nodes (2)

As stated before, additional rules are required to tell an algorithm when to
begin and when to end associating nodes with a section. In addition to that,
it must be taken into account that an algorithm needs to have the means to
execute the corresponding operations when entering or exiting certain nodes.
That is, it must be possible to implement these rules.

### Node sequence

```
ns := [...,gi,...,pi,...,ni,...,nj,...,pj,...,gj,...]
                       ...][ s1  ][ s2  ][ s3  ][...
(exit events)                    ni     pi     gi
```

* `ni` represents the current sectioning node
* `[ni+1,nj]` contains all the descendants of `ni`
* `pi` represents the parent of node `ni`
* `[pi+1,pj]` contains all the descendants of `pi`
* `gi` represents the grandparent of `ni`
* `[gi+1,gj]` contains all the descendants of `gi`

### Types of sections

This overview of the general characteristics of sectioning nodes defines the
scope of a section independently of any particular node tree. Because of that,
the definitions first define with which node a certain type of a section always
has to begin. In addition to that, the last possible node is defined such that
the initially mentioned requirements can still be fulfilled. Consequently, the
general definitions mentioned here define the default maximum scope allowed for
these type of sections.

However, it is still possible to define additional characteristics (e.g. rank
of a heading) that allow to further reduce the scope of a presequent section.

*type-1 sections*

The very first subsequent node that could possibly be associated with a section
is the first child of a sectioning node. That is, because it is unreasonable to
associate a sectioning node with its own section.

A section will be referred to as a "type 1 section", if its scope begins with
the first child of its sectioning node. Consequently, a sectioning node that
declares a type-1 section will be referred to as a "type 1 sectioning node".

*type-2 sections*

The next reasonable subsequent node is the next sibling of a sectioning node.

Because of that, a section that begins with the next sibling of its sectioning
node will be referred to as a "type 2 section". Consequently, a sectioning node
that declares a type-2 section will be referred to as a "type 2 sectioning node".

### Type-1 sectioning nodes

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

*first node*

An algorithm must mark a type-2 section as being open, before the exit event of
a type-2 sectioning node is being exited. Because of that, the scope of a type-2
section begins with the next sibling of its sectioning node.

*last node*

### Are there any other reasonable section types?

<!-- ======================================================================= -->
## Node sequence (2)

**TODO** - 
associate nodes when entering

**TODO** -
can a node be allowed to have any effect on itself
(e.g. associate with its own section)?

<!-- ======================================================================= -->
## The root node

Because a section can not exist without a presequent sectioning node, the root
node, with which an algorithm has to begin, can not be associated with any
predeclared section. That is, because there is no sectioning node that is
presequent to the root.

*The universal section (u)*

However, the root node can be thought of as being embedded into some universal
section `u`. This special section can be understood to represent a theoretical
section that contains any tree of nodes.

As such, that universal section must be seen to be declared by some virtual
sectioning node that is presequent to any possible node. As such, the universal
section never ends.

Consequently, any node of a tree therefore belongs to at least the universal
section. Put differently, there is no node that does not belong to any section
at all.

*The root node is a sectioning node*

Without any further clarification, and assumed that a given root does itself
not (strictly or loosely) contain any other sectioning node, all the nodes in
the root's subtree would therefore only belong to the universal section.
Because of that, it would in theory not be possible to locate the root's inner
nodes inside of said universal section.

Consequently, the root node must always be seen to declare its own section.
As such, the root must itself be understood to represent a sectioning node.
