
<!-- ======================================================================= -->
# Design - extensions to the default definitions

The focus of the following considerations is on the introduction of modifier
properties which allow to extend the default definitions. Attributes, as a
form of notation, can then be defined that allow to specify such a property.
In addition to that, the definition of an existing node type, in combination
with such an attribute, then allows to define new dedicated nodes.

Example:

1. `close:N` -
   A modifier property which instructs to close `N` sections.
2. `<node close="N">` -
   The "close" attribute allows to specify the "close" modifier property.
3. `<close /> := <div close="1" />` -
   The "close" node instructs to close the current (parent) section.

Note that these modifier properties can be referred to as "extended definitions"
or "extensions (to the default definitions)".

<!-- ======================================================================= -->
## transformations

The first step is to take a look at those aspects which can be altered while
maintaining consistency with the default definitions. That consistency is
required because it must be possible to transform any description of a tree,
which uses extensions, into a semantically equivalent description, which
does not use such definitions. In short, for each extended description, there
must exist a semantically equivalent default description (->).

Obviously, if an extended pattern exists that can be transformed into a default
pattern, it does not mean that any default pattern can be transformed back into
an extended pattern. However, if an extended pattern was replaced by its default
pattern, then that default pattern can obviously be transformed back into at
least one extended pattern (<-).

* extended description <-> default description
* i.e. always (->), but not necessarily (<-)
* similar to that: extended language <-> strict language

Because of that, the definition of extensions is not intended to add entirely
new features. These extensions are intended to be be optional and are therefore
a mere matter of convenience.

Hence, in order to proof a statement, a proof can be reduced to a statement
with regards to the default definitions. That is, a proof may ignore, based
on the above transformations, any extended definition:

1. Proof that extensions are by design consistent with the default definitions.
2. Based on the default definitions, proof or disproof a given statement.

**TODO**
with regards to close modifiers -
proof of consistency -

<!-- ======================================================================= -->
## close modifiers

Obviously, any extension can only have an effect on an algorithm's current
context. In addition to that, and because the declaration of new sections is
covered by the definition of sectioning nodes, the closure of sections is
the only option left that can be used to define any extension. Consequently,
extensions can only represent instructions to close presequent sections.

Note that already closed sections are no longer relevant. That is, because
sections can not be reopened, and because of that, no further nodes and/or
subsections can be associated with closed sections. Likewise, subsequent nodes
and sections must be ignored. Which is, because these are not even guaranteed
to exist.

An attribute that instructs to close zero or more sections will be referred to
as a "(close) modifier". In addition to that, any node can be understood to have
a default (close) modifier associated with it (e.g. `close="0"`). That is, and
in the context of the following considerations, the close modifier property,
which instructs to close zero sections (default definitions), will be extended
in such a way that it is allowed to instruct to close one or more sections (an
extended definition).

Note that, in cases where the modifier instructs to close no sections, the
modifier is said to be not relevant. In contrary to that, such a modifier is
in general relevant, if it instructs to close one or more sections.

Because the only option left to define any extension is to close sections, the
term "close modifier" will be used instead of the terms "extended definition"
or "extensions". In addition to that, a node which instructs to close a section
before the end of the section's default scope is reached (i.e. a node that has
such a non-zero attribute), will be referred to as an "end-marker node". That
is, a node which has a non-relevant close modifier (i.e. close 0 sections) is
not an end-marker node.

<!-- ======================================================================= -->
## benefits of close modifiers

As stated before, a subsequent node must be located inside of the scope of a
section, if the node is supposed to be an element of that section. Likewise, if
a node is no longer supposed to be an element of a section, the section's scope
must end before the node is going to be entered.

Therefore, and in order to change the relationship of a node, the scope of one
or more sections must be altered. And, because of that, the parent section of a
node depends on presequent nodes (i.e. sectioning nodes and parent containers).
That is, the information which defines a node's location within the section
hierarchy is not directly bound to the node itself. Consequently, and if a node
tree is restricted to the default definitions, the section hierarchy is well
defined, but not necessarily that obvious.

As mentioned above, close modifiers allow to instruct an implementation to close
sections that would otherwise remain to be open. As such, those modifiers allow
to explicitly reduce the scope of sections and thus allow to change the current
(parent) section. Because of that, close modifiers allow to explicitly change
the location of subsequent nodes and sections within the section hierarchy.

Consequently, close modifiers can be used to express a more obvious section
hierarchy. That is, (1) such modifiers are possible, and (2) they improve the
overall design by making it more convenient to express a specific hierarchy.

**CLARIFICATION**
The definition of close modifiers is in general reasonable.

Note that the below cases do not take into account, whether it should even be
allowed to close sections in a given context. All cases only state whether, from
a limited technical perspective, it is in general possible to close sections.

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

If sections are closed before the current node being entered is associated,
then that node, and any other node subsequent to it, will be associated with
an ancestor section of those recently closed sections. Because of that, this
case can not result in any conflict. This case is therefore a viable option.

Note that this case could be used to define end-marker nodes (e.g. `<close />`).
If such a node would be understood to only close the current section, then the
effect of these nodes would be to: (1) first close the (old) current section,
and then (2) associate the node and potentially also its descendant nodes with
the (new) current section.

> case 2 - when entering a sectioning node's enter event - (1)

This case is a viable option because it will not trigger conflicting statements
with regards to the logical location of a section: (1) the sectioning node will
be associated with one of the current section's ancestor sections, and (2) the
section's content nodes will be associated with the declared section, which is
going to be a subsection to the sectioning node's parent section. That is, the
declared section will be strongly connected with its sectioning node (as it
should be).

> case 3 - when exiting a node's enter event - (0)

This case means that the node is associated before sections will be closed.
Because of that, this case will trigger conflicting statements: (1) the
node's descendants do not belong to the closed sections, and (2) the node's
descendants, due to implicit associations that result from the association of
the node being entered, belong to the closed sections. As such, this case can
not be used for the definition of extensions (i.e. not a viable option).

> case 4 - when exiting a sectioning node's enter event - (0)

In addition to case 3, this case will also trigger conflicting statements with
regards to the logical location of a section. That is, because regardless of
what type of section is declared, the conflicting statements then are: (1) the
section is, due to the association of the sectioning node, located inside of
the to-be-closed sections, and (2) the section is, because of the association
of its content nodes (after closing the sections), *not* located inside of the
then-closed sections. That is, the declared section is not a subsection of the
section with which its sectioning node is associated. And, because of that,
the declared section is not strongly connected.

Note that, with regards to type-1 sectioning nodes, the sections must be
closed before the declared section is opened (i.e. an issue related to the node
event's order of operations). Otherwise, the declared section will be closed by
the sectioning node's close modifier. That is, because the declared section, as
soon as it is open, will become the new current section. 

> case 5 - when entering a node's exit event - (0)

As mentioned before, any node is a parent container, if the corresponding
node has type-2 sectioning nodes as its child nodes. Because of that, inner
sections must always be closed first, whether the node's close modifier
instructs to close a section or not (i.e. regardless of the node's close
modifier). Consequently, this case can not be used to define extensions.

> case 6 - when entering a sectioning node's exit event - (0)

Due to case 5, this case can not be used because inner sections must always
be closed first, regardless of a sectioning node's close modifier.

Note that a type-1 sectioning node is by definition the parent container of
the section it declares. That is, if it would not allowed to close a type-1
section before the end of its default scope is reached, then this node event
will always have to first close at least the declared type-1 section.

Note that a type-2 sectioning node by definition never acts as the parent
container of the section it declares. In addition to that, a type-2 sectioning
node is defined to not contain any sectioning node as its descendant nodes.
Consequently, a type-2 sectioning node will by definition never act as the
parent container of any section. That is, if user/input errors are ignored.

> case 7 - when exiting a node's exit event - (1)

By the time a node's exit event is being exited, all the inner sections of the
node being exited have already been closed (see case 5). Consequently, such a
close modifier can only instruct to close sections that were still open by the
time the node being exited was entered. In addition to that, the node, and all
descendants of that node, have already been associated. Which is why the close
modifier of such a node can no longer change the association of these nodes.

However, such a modifier can still change the relationship of those nodes and
sections that are subsequent to the node's exit event. And, because of that,
this case could still be used to mark the end of a branch of the section tree
(i.e. end-marker nodes). As such, the effect of such a definition would be to:
(1) first associate the node and its descendants with the current section, and
(2) if necessary close one or more sections after closing the node's inner
sections.

Note that, if such an end-marker node would instruct to close more than one
sections, then it would always be strictly associated with the least significant
closed section. And, because of that, the node would be loosely associated with
all other closed and still open ancestor sections.

Because of that, and if more than one section would have to be closed, it could
be difficult to detect (by humans and/or implementations) why sections had to
be closed. That is, because such a node would then be located "deep inside" of
a subsection and will therefore not necessarily be easily accessible to its
ancestor sections (Note that this can be understood too represent a reason as
to why not to associate end-marker nodes with the sections they close).

> case 8 - when exiting a sectioning node's exit event - (0)

Because all nodes have already been associated, closing those sections that
are presequent to a type-1 sectioning node's enter event (while the node is
being exited) *will not result* in conflicting statements with regards to the
location of the declared section.

However, this has the same issue as parent containers (i.e. presequent nodes
must be edited in order to change the relationship of subsequent nodes and
sections). That is, the relationship a section has with other sections depends
on a sectioning node which is presequent to the section's sectioning node.
Consequently, and depending on the exact notation of close modifiers, authors
could have difficulties to notice the reasons behind the relationship between
two sections. As such, this case is does not allow to express a more obvious
section hierarchy (i.e. no significant advantage over the default definitions).

Because the content nodes of a type-2 section have not been associated yet
(i.e. in contrary to the sectioning node and its descendant nodes), closing
those sections that are presequent to a type-2 sectioning node's enter event
(while the node is being exited) *will result* in conflicting statements with
regards to the location of the declared section: (1) the sectioning node and
its descendants belong to the closed sections, and (2) the declared section's
content nodes do not belong to the closed sections.

<!-- ======================================================================= -->
## types of end-marker nodes

```
..., <node>, ..., </node>, ...
     |1/1 |0/0    |0/0  |1/0
cases 1,2, 3,4,    5,6,  7,8
```

In general, two types of close modifiers are possible:

* type-1: close sections before entering a node (see cases 1,2), and
* type-2: close sections after exiting a node (see cases 7,8).

And, because of that, the definition of close modifiers would have to allow
to distinguish between those two types. That is, additional effort would be
required to define close modifiers, if both types would have to be supported.
For example via ...

* notation 1: `<div roles="close_enter:N">` vs. `<div roles="close_exit:N">`
* notation 2: `<div roles="close:N">` vs. `</div roles="close:N">`

Because of that, one would always have to be aware of the differences between
those two types. Apart from that, the close modifier role is in principle
independent of any other role. As such, the combination of roles (close-modifier,
sectioning-node, etc.) must not result in conflicting statements (compare with
case 8). And because tagging a node with multiple roles is prone to user/input
errors, the use of type-2 close modifiers is in general ill advised.

Note that, in order to avoid contradictory statements, a type-2 close modifier
would always have to be ignored, if it was used to tag a type-2 sectioning
node. And, because of that, such a close modifier would not be generic as an
implementations would always have to test whether the tagged node is a type-2
sectioning node or not.

Note that a type-2 close modifier would also require to define an "order of
roles" for when exiting a node's exit event: (1) close inner sections, then
(2) close presequent sections, and finally (3) open the declared section.

That is, and in order to avoid the issues related to the support of multiple
different types of close modifiers, the definition of type-1 close modifiers
is the only true generic option that remains.

**CLARIFICATION**
The only viable generic option to define conflict free close modifiers is,
if sections are closed when entering a node's enter event (i.e. case 1 and 2).

<!-- ======================================================================= -->
## a role-based perspective

The term "close modifier" can be understood to represent a role. That is,
because any node can in principle be understood to be associated (or tagged)
with that role. Obviously, there are multiple notations which could be used
to tag a node with a role (e.g. via attributes):

* `<div close="0">`, or `<div roles="close:0">`

Note that this role instructs to close "0" (i.e. no) sections, which
corresponds with the default definition of active and inactive nodes.

Therefore, and with the association of roles in mind, the definition of a
node type can be understood to implicitly tag all nodes of that type with
those roles that are associated with the corresponding type definition:

* `<div>` := "a generic node that has no role"
* `<close> := <div roles="close:1">`

Note that the term "sectioning node" can also be understood to represent
a role (i.e. "declare a new section of the specified type"):

* `<h> := <div roles="type:2">`

Furthermore, each node can in principle be associated with multiple roles
at the same time:

* `<h1> := <div roles="rank:1, type:2">`

Note that rank values can be understood to represent a specific notation
of a close modifier.

In addition to that, a role may implicitly include further roles. That is,
tagging a node with one role may implicitly tag that node with even further
roles. Because of that, a role may act in general as a named group of roles,
which itself (i.e. the group) does not necessarily have to act as a role.
That is, a group does not necessarily need its own semantics, other than what
is defined by the roles it includes:

* `h(i) := (rank:i, type:2)`
* `<h1> := <div roles="h:1">`

Note that a "parent-container" role does not exist. That is, because tagging
a node with a role will always associate a node with that role. But, whether a
node is a parent container or not, does not depend on the association of roles:

* Even if a node would be associated with a parent-container role, that node
  is not a parent container, if it does not have a type-2 sectioning node as
  one of its child nodes.
* Even if a node is not associated with a parent-container role, that node
  will still be a parent container, if it has even one such child node.
* Put differently, if a node is a parent container or not solely depends on
  the relationship it has with optional descendant sectioning nodes.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
With regards to this design, the only relevant roles are:
(1) inactive nodes and (2) active nodes. In addition to that, the set
of active nodes contains (3) sectioning nodes and (4) end-marker nodes.
That is, active nodes are sectioning nodes and/or end-marker nodes.

* `sectioning-node` := "declares a new subsection"
* `end-marker-node` := "closes sections when being entered"
* `active-node := (sectioning-node, end-marker-node)`
* `inactive-node` := "not an active node", or "does not affect the outline"

**CLARIFICATION**
An implementation will have to execute operations based on the roles that a node
has. That is, because any node, even type-1 and type-2 sectioning nodes, can be
tagged with a close modifier.

Because of that, an implementation must have the means to detect all the roles
of a node either by the node's definition (e.g. via the node's name), or by
some agreed-upon notation that is used to tag nodes with roles (e.g. via node
attributes).
