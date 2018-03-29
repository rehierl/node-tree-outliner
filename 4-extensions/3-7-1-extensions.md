
<!-- ======================================================================= -->
# Design - extending the default definitions

The focus of the following considerations is to evaluate those options which
allow to extend the default definitions by the definition of nodes and/or
attributes. Note that these definitions will be referred to as "extended
definitions", or simply as "extensions (to the default definitions)".

> extended description => default description

The first step is to take a look at those aspects which can be altered while
maintaining consistency with the default definitions. That consistency is
required because it must be possible to transform any description of a tree,
which uses extended definitions, into a semantically equivalent description,
which does not use such definitions. In short, for each extended description,
there must exist an equivalent default description.

As such, the definition of extensions is not intended to add entirely new
features to the defualt definitions. These extensions will be a mere matter
of convenience.

**TODO**
Put differently, the use of extended definitions must be optional. That is,
because the default definitions already allow to define any section hierarchy.
In addition to that, the separation of the extended definitions from the
default definitions allows to ...

<!-- ======================================================================= -->
## close modifiers

Obviously, extensions can only change an algorithm's current context.
In addition to that, and because the creation of new sections is already
dealt with by the definition of sectioning nodes, such extensions only
allow to instruct an implementation to close presequent sections.

Note that already closed presequent sections are no longer relevant. That is,
because sections can not be reopened, and because of that, no further nodes
and/or subsections can be associated with sections that are already closed.
Likewise, subsequent nodes and sections are not relevant. Which is, because
those are not even guaranteed to exist. Consequently, extensions can only
represent instructions to close presequent sections.

Note that attributes, which instruct an implementation to close sections, will
be referred to as "(close) modifiers". In addition to that, any node can be
understood to always have a default (close) modifier associated with it (e.g.
`<div close="0">`). Because of that, the term "close modifier" will be used
instead of the terms "extended definition" or "extensions".

Note that a node, which instructs to close a section (i.e. before the end of
the section's default scope is reached), will be referred to as the "end-marker
node" of the corresponding section. However, and due to a section's parent
container, not every section will have an end-marker node.

<!-- ======================================================================= -->
## available options

```
               | an (inactive/sectioning) node's |
               | enter event     | exit event    |
---------------------------------------------------
 when entering | (1/1)           | (0/0)         |
 when exiting  | (0/0)           | (1/0)         |
```

* `1` - this case represents a viable option
* `0` - this case is ill advised, or results in one or more conflicts
* `1/0` - this case represents a viable option with regards to inactive
  nodes (`1`), but not with regards to sectioning nodes (`0`).

```
..., <node>, ..., </node>, ...
     |1/1 |0/0    |0/0  |1/0
```

Note that the only viable two cases are when entering a node's enter
event, and when exiting its exit event. However, the latter case does
not represent a viable option with regards to sectioning nodes.

> case 1 - when entering a node's enter event - (1)

Obviously, presequent sections can be closed before a subsequent node is
associated. Because of that, the current node (and its descendants) will
belong to the parent section of the most significant section of the
to-be-closed sections.

This case could therefore be used in order to define end-marker nodes
(e.g. `<close />`). Note that the effect of such a definition would be to:
(1) first close the (old) current section, and then (2) associate the node
(and potentially any descendant nodes) with the (new) current section.

> case 2 - when entering a sectioning node's enter event - (1)

Closing a presequent section before associating the sectioning node that is
being entered, is a viable option. That is, because it will not result in
conflicting statements with regards to the logical location of a section:
(1) the sectioning node will be associated with one of the current section's
ancestor sections, and (2) the section's content nodes will be associated with
the declared section, which will then be a subsection to the sectioning node's
parent section. That is, the declared section will be strongly connected with
its sectioning node (as it should be).

> case 3 - when exiting a node's enter event - (0)

This case means that the node is associated before presequent sections will be
closed. Because of that, this case will result in conflicting statements: (1)
the node's descendants do not belong to the closed sections, and (2) the node's
descendants, due to implicit associations that result from the association of
the node being entered, belong to the closed section.

> case 4 - when exiting a sectioning node's enter event - (0)

In addition to the issue mentioned in case 3, this case will also result in
conflicting statements with regards to the logical location of a section.

Regardless of what type of section is declared, the conflicting statements
then are: (1) the section is, due to the association of the sectioning node,
located inside of the to-be-closed sections, and (2) the section is, because
of the association of its content nodes (after closing the presequent sections),
*not* located inside of the then-closed sections. That is, the declared section
is not a subsection of the section with which its sectioning node is associated.
And, because of that, the declared section is not strongly connected.

Note that, with regards to type-1 sectioning nodes, the presequent sections
must be closed before the sectioning node's section is opened (i.e. an issue
related to the in-enter event order of operations). Otherwise, the declared
section will be closed by the sectioning node's close modifier. That is,
because the declared section, once it is opened, will then be the new current
section. 

> case 5 - when entering a node's exit event - (0)

As mentioned before, any node is a parent container, if the corresponding node 
has type-2 sectioning nodes as its child nodes. Because of that, such inner
sections must always be closed first, whether the node's close modifier
instructs to close any sections or not. Consequently, case 5 does not apply.

> case 6 - when entering a sectioning node's exit event - (0)

As before, case 6 does not apply because inner sections must always be closed
first, regardless of any potential close modifier.

Note that a type-1 sectioning node is by definition the parent container of
the section it declares. That is, if it is not allowed to close a type-1
section before the end of its default scope is reached, then this node event
will always have to close at least the declared type-1 section.

Note that a type-2 sectioning node by definition never acts as the parent
container of the section it declares. In addition to that, a type-2 sectioning
node is defined to not contain any sectioning node as one of its descendant
nodes. Consequently, a type-2 sectioning node will never act as the parent
container of any section.

> case 7 - when exiting a node's exit event - (1)

Due to case 5, and by the time a node's exit event will be exited, all inner
sections can be considered to be closed. Consequently, such a close modifier
can only instruct to close sections that are still open by the time the
corresponding node was entered.

In addition to that, all descendants of that node have already been associated.
Which is why the close modifier of such a node can also no longer change these
associations.

However, such a modifier can still change the relationship of those nodes and
sections that are subsequent to the node's exit event. Because of that, this
case can only be used to mark the end of a branch of the section tree (i.e.
end-marker nodes). As such, the effect of such a definition would be to: (1)
first associate the node (and its descendants) with the current section, and
(2) if necessary close presequent sections.

Because of that, and if more than one section would have to be closed, it could
be difficult to detect why sections had to be closed. That is, because such a
node would then be located "deep inside" of a subsection and will therefore not
necessarily be easily accessible to its ancestor sections (i.e. a reason as to
why not to associate end-marker nodes with the sections they close).

> case 8.1 - when exiting a type-1 sectioning node's exit event - (0)

Because all nodes have already been associated, closing those sections that
are presequent to the type-1 sectioning node's enter event (while the node
is being exited) *can not result* in conflicting statements with regards
to the location of the declared section.

However, this case has the same issue as parent containers (i.e. presequent
nodes must be edited in order to change the relationship of subsequent nodes
and sections). That is, the relationship that a subsequent section has with
other sections depends on a node which is presequent to the subsequent
section's sectioning node. Consequently, and depending on the exact notation
of close modifiers, authors could have difficulties to understand the reasons
behind the relationship between two sections. As such, this case is, although
technically possible, ill advised.

> case 8.2 - when exiting a type-2 sectioning node's exit event - (0)

Because the content nodes of a type-2 section have not been associated yet
(i.e. in contrary to the sectioning node and its descendant nodes), closing
those sections that are presequent to a type-2 sectioning node's enter event
(while the node is being exited) *will result* in conflicting statements with
regards to the location of the declared section: (1) the sectioning node and
its descendants belong to the closed section, and (2) the declared section's
content nodes do not belong to the closed sections.

<!-- ======================================================================= -->
## benefits of close modifiers

As stated before, a subsequent node must be located inside of the scope of a
presequent section, if the node is supposed to be an element of that a section.
Likewise, if a node is not supposed to become an element of a section, then
the scope of that section must end before the node is entered.

Therefore, and in order to change the relationship of a node, the scope of
one or more presequent sections must be altered. Because of that, the parent
section of a node depends on presequent nodes. That is, the information which
defines a node's location within the section tree is not directly bound to the
node itself. Consequently, and if only the default definitions are used, the
section hierarchy of a node tree is well defined, but not that obvious.

As mentioned above, close modifiers allow to instruct an implementation to
close presequent sections. As such they allow to explicitly limit the scope of
presequent sections and therefore allow to select a different current section.
Because of that, they allow to explicitly change the location of subsequent
nodes within the section hierarchy.

Consequently, close modifiers can be used to express a more obvious section
hierarchy. That is, (1) such modifiers are possible, and (2) they improve the
overall design by making it more convenient to express a specific section
hierarchy.

**CLARIFICATION**
The definition of close modifiers is in general reasonable.

Note however that the above cases do not take into account, whether it should
even be allowed to close presequent sections in a given context. Those cases
only state that, from a technical perspective, it is in general possible and
could be allowed.

<!-- ======================================================================= -->
## a role-based perspective

The term "close modifier" can be understood to represent a role. That is,
because any node can in principle be understood to be associated (or tagged)
with that role. Obviously, there are multiple notations that could be used
to tag a node with a role (e.g. via attributes):

* `<div roles="close:0">`, or `<div close="0">`

Note that this close modifier role instructs to close "0" (i.e. no) sections,
which corresponds with the current definition of inactive nodes and sectioning
nodes.

Therefore, and with the association of roles in mind, the definition of specific
node types can be understood to implicitly tag all nodes of that type with the
appropriate roles. The definition of node types are, because of that, similar
to the definition of a named macros:

* `<div> := [a generic node with no roles]`
* `<end> := <div roles="close:1">`

Note that the term "sectioning node" can also be understood to represent
a role (i.e. "declare a new section of the specified type"):

* `<h> := <div roles="type:2">`

Furthermore, each node can in principle be associated with multiple roles
at the same time:

* `<h1> := <div roles="rank:1, type:2">`

Note that rank values represent a specific notation for close modifiers
(see the subsequent chapters).

In addition to that, a role may implicitly include further roles. That is,
tagging a node with one role may implicitly tag that node with even further
roles. Because of that, a role may act in general as a named group of roles,
which itself (i.e. the group) does not necessarily have to act as a role:

* `role_h1 := (rank:1, type:2)`
* `<h1> := <div roles="role_h1">`

**CLARIFICATION**
With regards to the outline algorithm, only two main roles are relevant:
(1) inactive nodes and (2) active nodes. In addition to that, the set of
active nodes consists of the (3) sectioning nodes and (4) end-marker nodes
(aka. close modifiers). To be more accurate, active nodes are sectioning
nodes and/or end-marker nodes.

Note that a "parent container" role does not exist. That is, because tagging
a node with a role will always associate a node with that role. But, whether a
node is a parent container or not, does not depend on the association of roles:
(1) Even if a node would be associated with that role, such a node can not be
a parent container if it does not have a type-2 sectioning node as one of its
child nodes. (2) Even if a node is not associated with that role, such a node
will act as a parent container if it does have such child nodes.

**CLARIFICATION**
An implementation executes operations based on the roles of a node.

As such, an implementation must have the ability to detect the roles of
a node either by the node's definition, or by some commonly agreed-upon
notation (e.g. via the node's attributes).

<!-- ======================================================================= -->
## derived statements

**TODO**
a section will be closed either by its parent container, or by an end-marker
node - this allows to determine a section's last top-level node when that
section is being closed

**CLARIFICATION**

There is consequently no issue of having to distinguish between different
kinds of close modifiers: (1) has an effect on all the nodes (the node itself,
its descendants and all other subsequent nodes), and (2) only has an effect
on those nodes that are subsequent to the node's exit event.

**CLARIFICATION**
End-marker nodes do not belong to the sections they close.

**TODO**
case 7 in combination with 1 and 2 -
i.e. based on the perspective of roles -

**TODO**
the roles of a node must be clearly separated

* parent container
* end-marker node
* sectioning node
