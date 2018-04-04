
<!-- ======================================================================= -->
# Design - extensions to the default definitions

The focus of the following considerations is on the definition of modifier
properties which allow to extend the default design. Based on these properties,
node attributes can be defined, which allow to manually specify the a property
(i.e. syntax/notation). In addition to that, the definition of an existing node
type, in combination with a specific attribute, then allows to even define new
dedicated nodes.

Example:

1. `close:N` - This modifier property instructs to close `N` sections.
2. `<node close="N">` - The "close" attribute implements the "close" property.
3. `<close /> := <div close="1" />` - This node instructs to close a single
   section only. The closed section will always be the current section.

Note that these modifier properties can be referred to as "extended definitions"
or "extensions (to the default definitions)".

<!-- ======================================================================= -->
## semantical transformations

The first step is to take a look at those aspects which can be altered while
maintaining consistency with the default definitions. That consistency is
required because it must be possible to transform any description of a tree,
which uses extensions, into a semantically equivalent description, which
does not use such definitions. In short, for each extended description, there
must exist a semantically equivalent default description (->).

Obviously, if an extended pattern exists that can be transformed into a default
pattern, then that does not mean that any default pattern can be transformed
backwards into an extended pattern. However, if an extended pattern was replaced
by its default pattern, then that default pattern can be transformed backwards
into at least one extended pattern (<-).

* extended description <-> default description
* similar to: extended language <-> strict language

Because of that, the definition of extensions is not intended to add entirely
new features. These extensions are intended to be be optional and are therefore
only a matter of convenience.

Consequently, and in order to proof a statement, a proof can be reduced to
prove a given statement with regards to the default definitions. That is,
a proof may ignore, based on the above transformations, any extensions:

1. Proof (e.g. by design) that all extensions
   are consistent with the default definitions/design.
2. Based on the default definitions, proof or disproof the statement.

<!-- ======================================================================= -->
## close modifiers

Obviously, any extension can only change an algorithm's current context.
In addition to that, and because the declaration of new sections is already
covered by the definition of sectioning nodes, the closure of sections is
the only option left that can be used to define any extension. Consequently,
extensions can only represent instructions to close presequent sections.

Note that already closed presequent sections are no longer relevant. That is,
because sections can not be reopened, and because of that, no further nodes
and/or subsections can be associated with closed sections. Likewise, subsequent
nodes and sections must be ignored. Which is, because these are not guaranteed
to exist.

An attribute that instructs to close zero or more sections will be referred
to as a "(close) modifier". In addition to that, any node can be understood
to have a default (close) modifier associated with it (e.g. `<div close="0">`).

Because of the above considerations, the term "close modifier" will be used
instead of the terms "extended definition" or "extensions". In addition to
that, a node which instructs to close a section before the end of the section's
default scope is reached (i.e. a node that has such an attribute), will be
referred to as an "end-marker node".

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

As explained below, the only viable cases are when entering a node's enter event
(`1/1`) and when exiting a node's exit event (`1/0`). However, the latter case
does not represent a viable option with regards to sectioning nodes.

> case 1 - when entering a node's enter event - (1)

If presequent sections are closed before the node being entered is associated,
then that node, and any other node subsequent to it, will be associated with an
ancestor section of those recently closed sections. Because of that, this case
can not result in any conflict. This case therefore represents a viable option.

Note that this case could be used to define end-marker nodes (e.g. `<close />`).
If such a node would be defined to only close the current section, then the
effect of these nodes would be to: (1) first close the (old) current section,
and then (2) associate the node and potentially also its descendant nodes with
the (new) current section.

> case 2 - when entering a sectioning node's enter event - (1)

Closing a presequent section before associating the sectioning node being
entered, is a viable option. That is, because it will not result in conflicting
statements with regards to the logical location of a section: (1) the sectioning
node will be associated with one of the current section's ancestor sections, and
(2) the section's content nodes will be associated with the declared section,
which is going to be a subsection to the sectioning node's parent section. That
is, the declared section will be strongly connected with its sectioning node
(as it should be).

> case 3 - when exiting a node's enter event - (0)

This case means that the node is associated before presequent sections will be
closed. Because of that, this case will result in conflicting statements: (1)
the node's descendants do not belong to the closed sections, and (2) the node's
descendants, due to implicit associations that result from the association of
the node being entered, belong to the closed sections. As such, this case can
not be used for the definition of extensions (i.e. not a viable option).

> case 4 - when exiting a sectioning node's enter event - (0)

In addition to the issue mentioned in case 3, this case will also result in
conflicting statements with regards to the logical location of a section.

Regardless of what type of section is declared, the conflicting statements then
are: (1) the section is, due to the association of the sectioning node, located
inside of the to-be-closed sections, and (2) the section is, because of the
association of its content nodes (after closing the presequent sections), *not*
located inside of the then-closed sections. That is, the declared section is not
a subsection of the section with which its sectioning node is associated. And,
because of that, the declared section is not be strongly connected.

Note that, with regards to type-1 sectioning nodes, the presequent sections
must be closed before the declared section is opened (i.e. an issue related to
the enter event's order of operations). Otherwise, the declared section will be
closed by the sectioning node's close modifier. That is, because the declared
section, as soon as it is open, will be the new current section. 

> case 5 - when entering a node's exit event - (0)

As mentioned before, any node is a parent container, if the corresponding
node has type-2 sectioning nodes as its child nodes. Because of that, inner
sections must always be closed first, whether the node's close modifier
instructs to close any section or not (i.e. regardless of the node's close
modifier). Consequently, this case can not be used to define extensions.

> case 6 - when entering a sectioning node's exit event - (0)

Due to case 5, this case can not be used because inner sections must always
be closed first, regardless of a sectioning node's close modifier.

Note that a type-1 sectioning node is by definition the parent container of
the section it declares. That is, if it would not allowed to close a type-1
section before the end of its default scope is reached, then this node event
will always have to close at least the declared type-1 section.

Note that a type-2 sectioning node by definition never acts as the parent
container of the section it declares. In addition to that, a type-2 sectioning
node is defined to not contain any sectioning node as its descendant nodes.
Consequently, a type-2 sectioning node will by definition never act as the
parent container of any section. That is, if user/input errors are ignored.

> case 7 - when exiting a node's exit event - (1)

By the time a node's exit event is being exited (see case 5), all the inner
sections of the node being exited have already been closed. Consequently, such
a close modifier can only instruct to close sections that are still open by the
time the node being exited was entered.

In addition to that, the node, and all descendants of that node, have already
been associated. Which is why the close modifier of such a node can no longer
change the association of these nodes.

However, such a modifier can still change the relationship of those nodes
and sections that are subsequent to the node's exit event. Because of that,
this case could still be used to mark the end of a branch of the section tree
(i.e. end-marker nodes). As such, the effect of such a definition would be to:
(1) first associate the node and its descendants with the current section, and
(2) if necessary close one or more presequent sections after closing the node's
inner sections.

Because of that, and if more than one section would have to be closed, it could
be difficult to detect (by humans and implementations) why sections had to be
closed. That is, because such a node would then be located "deep inside" of a
subsection and will therefore not necessarily be easily accessible to its
ancestor sections (Note that this can be understood too represent a reason as
to why not to associate end-marker nodes with the sections they close).

> case 8 - when exiting a sectioning node's exit event - (0)

Because all nodes have already been associated, closing those sections that
are presequent to a type-1 sectioning node's enter event (while the node is
being exited) *will not result* in conflicting statements with regards to the
location of the declared section.

However, this has the same issue as parent containers (i.e. presequent nodes
must be edited in order to change the relationship of subsequent nodes and
sections). That is, the relationship that a subsequent section has with other
sections depends on a sectioning node which is presequent to the subsequent
section's sectioning node. Consequently, and depending on the exact notation
of close modifiers, authors could have difficulties to notice the reasons
behind the relationship between two sections. As such, this case is does
not allow to express a more obvious section hierarchy (i.e. no significant
advantage over the default definitions).

Because the content nodes of a type-2 section have not been associated yet
(i.e. in contrary to the sectioning node and its descendant nodes), closing
those sections that are presequent to a type-2 sectioning node's enter event
(while the node is being exited) *will result* in conflicting statements with
regards to the location of the declared section: (1) the sectioning node and
its descendants belong to the closed sections, and (2) the declared section's
content nodes do not belong to the closed sections.

<!-- ======================================================================= -->
## benefits of close modifiers

As stated before, a subsequent node must be located inside of the scope of a
presequent section, if the node is supposed to be an element of that section.
Likewise, if a node is not supposed to be an element of a section, then the
scope of that section must end before the node is entered.

Therefore, and in order to change the relationship of a node, the scope of one
or more presequent sections must be altered. And, because of that, the parent
section of a node depends on presequent nodes. That is, the information which
defines a node's location within the section hierarchy is not directly bound
to the node itself. Consequently, and if only the default definitions are used,
the section hierarchy of a node tree is well defined, but not necessarily that
obvious.

As mentioned above, close modifiers allow to instruct an implementation to
close presequent sections. As such they allow to explicitly end the scope of
presequent sections and therefore to switch to a different current section
(aka. the current parent section). Because of that, close modifiers allow to
explicitly change the logical location of subsequent nodes and sections within
the section hierarchy.

Consequently, close modifiers can be used to express a more obvious section
hierarchy. That is, (1) such modifiers are possible, and (2) they improve the
overall design by making it more convenient to express a specific hierarchy.

**CLARIFICATION**
The definition of close modifiers is in general reasonable.

Note that the above cases do not take into account, whether it should even be
allowed to close presequent sections in a given context. Those cases only state
that, from a technical perspective, it is in general possible and that it could
be allowed.

<!-- ======================================================================= -->
## a role-based perspective

The term "close modifier" can be said to represent a role. That is, because any
node can in principle be understood to be associated (or tagged) with that role.
Obviously, there are multiple notations that could be used to tag a node with a
role (e.g. via attributes):

* `<div close="0">`, or `<div roles="close:0">`

Note that this role instructs to close "0" (i.e. no) presequent sections,
which corresponds with the default definition of active and inactive nodes.

Therefore, and with the association of roles in mind, the definition of a
node type can be understood to implicitly tag all nodes of that type with
those roles that are associated with the type:

* `<div>` := "a generic node that has no role associated with it"
* `<close> := <div roles="close:1">`

Note that the term "sectioning node" can also be understood to represent a
role (i.e. "declare a new section of the specified type"):

* `<h> := <div roles="type:2">`

Furthermore, each node can in principle be associated with multiple roles
at the same time:

* `<h1> := <div roles="rank:1, type:2">`

Note that rank values can be understood to represent a specific notation of
a close modifier.

In addition to that, a role may implicitly include further roles. That is,
tagging a node with one role may implicitly tag that node with even further
roles. Because of that, a role may act in general as a named group of roles,
which itself does not necessarily have to act as a role. That is, a group
does not necessarily need its own semantics, other than what is implied by
the roles it includes:

* `role_h1 := (rank:1, type:2)`
* `<h1> := <div roles="role_h1">`

**CLARIFICATION**
With regards to the outline algorithm, only the following roles are relevant:
(1) inactive nodes and (2) active nodes. In addition to that, the set of
active nodes consists of (3) sectioning nodes and (4) end-marker nodes (aka.
close modifiers). To be more clear, active nodes are sectioning nodes and/or
end-marker nodes.

* `sectioning-node` := "declares a new subsection"
* `end-marker-node` := "closes sections when being entered"
* `active-node := (sectioning-node, end-marker-node)`
* `inactive-node` := "does not affect the node tree's outline",
                     or alternatively "not an active node"

Note that a "parent-container" role does not exist. That is, because tagging
a node with a role will always associate a node with that role. But, whether a
node is a parent container or not, does not depend on the association of roles:

* Even if a node would be associated with a parent-container role, that node is
  not a parent container, if it does not have a type-2 sectioning node as one of
  its child nodes.
* Even if a node is not associated with a parent-container role, that node will
  still be a parent container, if it has even one such child node.

**CLARIFICATION**
An implementation will have to execute operations based on the roles of a node.

That is, because any node can potentially be an end-marker node
(Note that this includes all type-1 and all type-2 sectioning nodes).

Because of that, an implementation must have the means to detect all the roles
of a node either by the node's definition (e.g. via the node's name), or by
some commonly agreed-upon notation used to tag nodes with roles (e.g. via node
attributes).

<!-- ======================================================================= -->
## derived statements

```
..., <node>, ..., </node>, ...
     |1/1 |0/0    |0/0  |1/0
cases 1,2, 3,4,    5,6,  7,8
```

**CLARIFICATION**
There is only one generic type of end-marker nodes. That is, the only viable
option to define conflict free close modifiers is, if presequent sections are
closed when entering a node's enter event (i.e. cases 1 and 2).

That is, because initially only two types are possible:

* type-1: close sections before entering a node (see cases 1,2), and
* type-2: close sections after exiting a node (see cases 7,8).

And, because of that, the definition of close modifiers would have
to allow to distinguish between those two types. For example via ...

* notation 1: `<div roles="close_enter:N">` vs. `<div roles="close_exit:N">`
* notation 2: `<div roles="close:N">` vs. `</div roles="close:N">`

Apart from that, a close modifier role is independent of any other role. As
such, the combination of roles (close-modifier, sectioning-node, etc.) must not
result in conflicting statements (see case 8). That is, because such definitions
are prone to trigger user/input errors. Consequently, the use of type-2 close
modifiers is in general ill advised, which is why the definition of a type-1
close modifier is the only generic option left.

Note that, in order to avoid contradictory statements, a type-2 close modifier
would always have to be ignored, if it was used to tag a type-2 sectioning node.
And, because of that, such a close modifier would not be generic as one would
always have to test whether the tagged node is a type-2 sectioning node.

Note that a type-2 close modifier would also require to define an "order of
roles" for when exiting a node's exit event: (1) close inner sections, then
(2) close presequent sections, and finally (3) open the declared section.

**CLARIFICATION**
End-marker nodes do not belong to the sections they close.

That is because type-1 close modifiers are the only viable option. Consequently,
end-marker nodes will never be associated with the section's they close.

Note that this is yet another reason as to why not to associate sectioning
nodes with the sections they declare: Because sectioning nodes can be tagged
with the end-marker role, associating sectioning nodes with the sections they
declare would be inconsistent with that role. That is, because (1) end-marker
nodes will be by definition associated with the parent section of the most
significant to-be-closed section (i.e. the then-new current section). In
contrary to that, and if sectioning nodes would have to be associated with
the sections they declare, (2) the sectioning nodes would then be associated
with a subsection of that then-new current section. Consequently, there would
have to be a clear reason as to why such an inconsistency can not be avoided.
The default case applies (i.e. associate with a presequent section), if such
a reason does not exist.
