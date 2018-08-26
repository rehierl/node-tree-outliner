
<!-- ======================================================================= -->
# Design - last nodes

**CLARIFICATION**
The last subsequent node of a section will always be a leaf node (either by
strict, or by loose association). Put differently, the last node of a section
never is a parent node.

That is because a section's last node would not be the section's last node, if
it were a parent. This is a mere consequence of the tree traversal as any node
will be entered if (and only if) all of its ancestors and all of its previous
siblings have already been entered.

Note that no such clarification can be derived for the first node of a section.
That is because the first node of a section depends on the definition of the
sectioning node (as it should be). In addition to that, such a definition
should not require any specific first node (i.e. no additional constraints).

**CLARIFICATION**
In contrary to a section's first node, it is in principle not possible to
pinpoint a section's last node independently of any specific structure.
Consequently, the relationship between a section's first and last node can
not be clearly defined.

That is because any associated node can potentially have any number of
descendant nodes. Because of that, and if the last node had a descendant,
that last node would then not be the section's last node. Due to the loose
associations mentioned earlier, the node tree and the section's definition
would then be, if one would try to pinpoint a section's last node, in
conflict with each other.

<!-- ======================================================================= -->
## question

Because the last node of a section can not be clearly identified, the question
where a section has to end by default is similar to the definition of intervals
on the set of real numbers. That is because in between any two real numbers,
there always is an infinite amount of additional numbers.

Apart from any specific and included upper boundary, it is however possible
to specify an interval of real numbers by exclusion: `r in [a,b)` where
`a,b,e in R+`. The meaning of this specification is that `r` may have any
value in between `a` (inclusive) and `b` (exclusive). Put differently, any
number from `a` to `(b - e)` is included, if `e` (epsilon) represents an
infinitesimal small positive number.

Obviously, the same approach can be used to specify the lower boundary by
exclusion: `r in (a,b]` where `a,b,e in R+` means that `r` may have any value
in between `a` (exclusive) and `b` (inclusive). In other words, any number from
`(a + e)` to `b` is included, if `e` is an infinitesimal small positive number.

**CLARIFICATION**
A type-1 sectioning node is the last unrelated node entered, but not exited,
before a section's first node is entered. Similar to that, a type-2 sectioning
node is the last unrelated node exited, before a section's first node is
entered.

Note that a type-1 section is defined to begin with the sectioning node's
first child. Because of that, and in order to support empty sections, the
definition requires to open the declared section when the sectioning node's
enter event is about to be exited, not when the first node is being entered.
Because of that, the definition of the first node of a type-1 section can
also be seen as a definition by exclusion.

Note that the definition of a type-2 section is similar with that regards.

**QUESTION**
Is it possible to define the end of a section in terms of an (enter or exit)
event, beginning with which no more associations are allowed?

To be more clear, once such an event is entered, the corresponding section must
be closed immediately. That is, even the event is not allowed to establish any
further association before closing the corresponding section.

<!-- ======================================================================= -->
## available events

One of the first events that could be used to close a section is the exit event
of a section's first (top-level) node. Obviously, using this particular event
to close a section by default won't help much as (1) a section would always
need to have at least one node (i.e. empty sections could not be supported
because an empty section could then not be closed) and (2) any such section
would always have to end with its first top-level node (i.e. multiple top-level
nodes could not be supported because a section can not be re-opened).

Because no descendant of a top-level node can be excluded, none of the events
of any descendant is suited to generically define the end of a section. That
is, because choosing one particular descendant as a section's last node would
represent an attempt to exclude any potential subsequent descendant. And,
because of that, the only event that could be used would be the exit event
of the last subsequent descendant. Obviously, such a definition can not be
independent of any particular structure and thus would not be generic.

A generic definition is in principle a necessity because any structural
requirement will undoubtedly add additional complexity to an implementation.
That is because an implementation would have to include additional logic
in order to handle potential user/input errors.

In order to generically define the end of a section, the definition should
also be independent of the section's actual type. That is because a definition,
which is based upon a specific type of sectioning node, is not completely
generic (i.e. generic with regards to subsequent nodes, but not with regards
to the sectioning node's type). Because of that, it would be preferable to
define the end of a section in terms of the relationship the section's last
node has with regards to its first node.

Note that this already indicates, that a completely generic definition can not
exist. That is because the definition of a section's last node, with regards
to its first node, builds upon the existence of a first node.

Note that all sections have to be closed, or otherwise their contents would
be undefined. Also, in order to close a section, that section has to be opened
first. Recall that sections have strict state transitions.

**DEFINITION**
The maximum (i.e. widest) scope of a section, that does not produce any
kind of conflict, will be referred to as "the default scope of a section".

Note that a generic definition of the end of a section can only define a
section's default scope. However, additional rules can in principle still
be defined which can be used to further limit the scope of a section (hence,
default scope).

**CLARIFICATION**
The search for an event that could be used to define the end of a section, with
regards to its first node, can be limited to (1) the exit event of a section's
last top-level node, (2) the enter event of the first unrelated node, and (3)
an exit event of one of the top-level node's ancestors.

The enter events of a section's top-level nodes can not be taken into account,
as this would produce a conflict: A top-level node is a top-level node, because
it is associated with a section. Using the enter event of such a node would
result in not associating the top-level node. Apart from being in conflict with
the definition of a top-level node, such a definition would be equivalent to
case (2).

The enter events of one of the top-level node's ancestors can also not be taken
into account. That is because in order to enter and associate a top-level node,
all of its ancestors must have been entered already. Because of that, the enter
event of a top-level node's ancestor can not be used.

### exit the last top-level node

Case (1) is not suited for a generic definition.

That is because it would require that an algorithm had the means to detect
whether a node is the section's last top-level node. Because of that, such a
definition would add an additional structural requirement (e.g. the n-th
top-level node, or a node of some specific type must exist).

Note that such a definition could also be seen as "a loose definition by
inclusion" ("inclusion" because the last top-level node is explicitly included,
"loose" because of the implicit inclusion of any loosely associated descendant).

However, the most important issue with this case is that it would add the
requirement, that any section must always have at least one node. That is,
because the section's close event could otherwise not be executed. As such,
this case can not be used for a generic definition.

Despite that, such a definition could also be seen to be inconsistent with
the definition of a sectioning node: Why consider a sectioning node to not
belong to its own section, but, in contrary to that, associate an end marker
node with the section it is supposed to end (i.e. either all in, or all out)?

### enter the first unassociated node

Case (2) is not suited for a generic definition.

That is because it would require to give a guarantee that such a node will
always be entered eventually. Consequently, such a definition would add a
structural requirement and, because of that, would not be generic.

However, it is still possible to define specific nodes (e.g. headings or
an end marker node) that, when entered, end one or more presequent sections.
The difference is that such a node is optional and, because of that, does
not have to exist.

Note also the switch in perspective: "forwards" from the current sectioning
node and "backwards" from an optional subsequent end-marker node.

### exit an ancestor of a top-level node

Case (3) is somewhat suited for a generic definition.

Except for the root node, any node in a rooted tree of nodes always has at least
one ancestor. Because of that, and with regards to the ancestors of a top-level
node, no additional requirements are added. That is, if this case is limited to
the exit event of the first/nearest ancestor (i.e. its parent node).

Any attempt to use the exit event of any other ancestor will add a structural
requirement. That is because from the perspective of the definition of a
sectioning node, other ancestors are not guaranteed to exist. Put differently,
a sectioning node, unless defined otherwise, can be a direct descendant of
the root (i.e. child) and, as such, does not have any ancestor other than its
parent node (i.e. root).

However, this case also requires, that a section always has at least one node.

### conclusion

None of the above cases is completely suited to support empty sections. That
is, because all of them, one way or another, add a requirement that at least
one subsequent node must exist. Even if there were corresponding definitions,
it simply is not possible to truly guarantee that such a node always exists
(e.g. user/input errors).

However, because the sectioning node has already been entered, the sectioning
node itself is guaranteed to exist. Because of that, its events can be used
to end the section it declares.

For obvious reasons, it is unreasonable to use the same event to open and
close a declared section. That is because it would guarantee that these
sections would always be empty. Consequently, the only event that can be
used is the sectioning node's exit event.

In addition to that, and except for the root node itself, any sectioning node
always has a parent node. Because of that, the events of a sectioning node's
parent are also candidates to close a section by default. However, the parent's
enter event is unavailable because it will always be executed even before the
sectioning node is entered. Consequently, the only event that remains is the
parent's exit event.

**CLARIFICATION**
The only events that can be used to generically limit a section's default
scope are: (1) the exit event of its sectioning node, and (2) the exit
event of its sectioning node's parent.

<!-- ======================================================================= -->
## the default scope

Would it even be reasonable to use the definition of a sectioning node to
restrict the default scope of a declared section?

```
1) ... n1:s </parent> n2:s ...
2) ... <group> n1:s </parent> n2:s </group> ...
```

Assumed that nodes `n1` and `n2` are the only nodes of section `s` and that
`n2` is the first node subsequent to `n1`.

Obviously, consistent transformations (and consequently dynamic support) are
unreasonably difficult (if not impossible), if a section contains top-level
nodes that belong to different parent nodes. Because of that, sections must
end with the exit event of the first node's parent.

**DEFINITION**
The parent node of a section's first node
is said to be the section's "parent container".

Note that the parent container of a section either is identical to the section's
sectioning node (type-1), or the parent node of its sectioning node (type-2).

Note that allowing a section to contain nodes, that are subsequent to the exit
event of its parent container, can potentially add a descendant of a presequent
sibling (i.e. the parent container) to the context of a subsequent node. Such
an option would therefore be in conflict with the definition of a node's
context.

Consequently, the definition of sectioning nodes must also include when a
section has to be closed by default. That is because consistent dynamic
support could otherwise not be guaranteed.

### type-1, first child

**DEFINITION**
The default scope of a type-1 section
ends with its sectioning node.

**CLARIFICATION**
An algorithm must close a type-1 section when it enters the exit event of its
sectioning node. Consequently, a type-1 sectioning node represents the parent
container of the declared section.

Note that, because the root node must always be treated as a type-1 sectioning
node, there is no need to take the root's non-existent parent node into account.

Note that no two type-1 sections have the same parent container. That is,
because any sectioning node always declares a single section. And, because of
that, a second type-1 section either is independent of the first type-1 section
(i.e. outside of and subsequent to it), or one of its descendants.

**CLARIFICATION**
Even if the default scope of a type-1 section has to end with the section's
sectioning node, a type-1 section could technically still be closed by an event
that is subsequent to the section's open and presequent to its default close
event.

However, just because an option is technically possible, does not imply that
it would be reasonable to support such an option.

### type-2, next sibling

**DEFINITION**
The default scope of a type-2 section
ends with the parent of its sectioning node.

**CLARIFICATION**
An algorithm must close a type-2 section when it enters the exit event
of the sectioning node's parent. Consequently, the parent of a type-2
sectioning node represents the parent container of the declared section.

Note that this definition does not have to take into account what kind of
node that parent container is. That a node is a section's parent container
is a requirement of a section, not a characteristic of the node. That is,
any parent node can potentially be the parent container of a type-2 section.

Note that the parent container of a type-2 section is presequent to its
sectioning node. That is because the parent container is an ancestor of
the sectioning node and, as such, will be entered before the sectioning
node is entered.

Note the switch in perspective: (1) a type-2 sectioning node with regards to
its guaranteed-to-exist parent container, and (2) a parent node with regards
to optional child type-2 sectioning nodes.

Note that multiple type-2 sections may have the same parent container. In
addition to that, the parent container of a type-2 section may even be the
parent container of a type-1 section (i.e. a type-1 sectioning node).

Note that the parent container of a type-2 section is guaranteed to exist.
That is because an algorithm must always treat its initial node as a type-1
sectioning node, even if that node is by definition a type-2 sectioning node.
Consequently, any type-2 sectioning node, that will be treated as such, will
always be a descendant of the root and, as such, will always have a parent
node.

**CLARIFICATION**
No type-2 sectioning node will ever act as the parent container of another
section.

That is because the type-2 sectioning nodes are defined to never have active
nodes as their descendants. Put differently, active descendant nodes must be
treated as inactive nodes, which is why a type-2 sectioning node will never
have any inner sections. A type-2 sectioning node will therefore never act as
the parent container of another section.

**CLARIFICATION**
Closing a type-2 section when its parent container is exited is a necessity,
if the type-2 definition is strict (/see/ "Why no loose type-2 definition?" /).

That is because if a type-2 sectioning node had no next sibling, the first
node associated would then be the next sibling of the sectioning node's next
relevant ancestor (i.e. the next upper ancestor that has a next sibling).
Because of that, the type-2 section would be in conflict with a strict type-2
definition.

<!-- ======================================================================= -->
## derived statements

**Memory hook**
A section, as a logical group of subsequent nodes, can be seen to be located
in between the section's parent container and the section's top-level nodes.
As such, a section can be understood to separate its nodes from the rest of
the node tree. Any node beneath that separator belongs to the section, and
any other node above or next to it does not.

```
          n1                              n4
          |                               |
 ---------------------      ------------------------
  |     section     |        |     |    section   |
 =====================       |    ==================
  |    separator    |        |     |   separator  |
  n2                n3       n5    n6             n7
```

(`n1` represents a type-1 and `n5` a type-2 sectioning node)

Similar to that, and if a node tree is drawn on a flat two-dimensional surface,
a closed line can be drawn around the nodes of a section. Any node within such
an enclosed area/segment belongs to the section, any node outside of it does
not.

Note that the only edges that pass through the section borders are the edges
between a section's top-level nodes and its parent container. No other edges
will cross such a border.

**CLARIFICATION**
As stated before, a section is subordinate to its sectioning node. In
addition to that, a section can also be understood to be superordinate
to its subordinate content nodes.

Note that, from a logical perspective, a section is located in between its
sectioning node and its content nodes. Consequently, a sectioning node can
be understood to be superordinate to the section's subordinate content nodes.

**CLARIFICATION**
The default scope of any section ends with its parent container.

Note that this statement neither turns a section's parent container into an
active node, nor does it force a section's parent container to be an inactive
node (e.g. type-1 sectioning node). Put differently, whether a parent container
is active or inactive only depends on the node's own definition, not on the
requirement that a section's default scope has to end with it.

**CLARIFICATION**
The default scopes of multiple sections may end with the same parent container.

Obviously, a parent container may have multiple type-2 sectioning nodes as
its child nodes. Because of that, such a parent container marks the end of
the default scopes of all of its inner sections.

Consequently, there is a 1:M relationship (not 1:1) between the set of parent
containers and the set of sections (or sectioning nodes).

**CLARIFICATION**
A parent container does not belong to any section
whose default scope has to end with it.

*With regards to a type-1 section*:

A sectioning node is defined to not be part of the section it declares.
This consequently also includes the parent container of a type-1 section.

*With regards to a type-2 section*:

If a parent container would belong to such a section, it would have to become
one of the section's top-level nodes. (To be more clear, the parent container
would then be the section's only top-level node). Consequently, nodes that
are presequent to a type-2 sectioning node, would, because of the associated
parent container, implicitly be associated with a subsequent section. That
is, the subsequent sectioning node would have an effect on nodes that are
presequent to it. As such, associating a parent container with a type-2
section would be in conflict with the definition of a node's context.

In addition to that, and because multiple type-2 sections may have the same
parent container, the question that would then have to be answered would be
with which inner section to associate such a parent container: With the first
inner section, or an inner section that is subsequent to it?

In short: A parent container must not be associated with a type-2 section.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Any section ends with the first event that belongs to an unassociated node.

Because the default scope of a section always ends with the first exit event
of an unassociated node, the only events that can be used to manually end a
section before the end of its default scope is reached, are the enter events
of optional and unassociated nodes. Note the switch in perspective: forwards
vs. backwards, and formal vs. optional.

Note that the exit event of an associated optional end marker node could be
used. However, this would be inconsistent with not associating sectioning
nodes with the sections they declare. Such nodes must therefore not be
associated with the sections they close.

**CLARIFICATION**
A section is not some arbitrary subsequence of the tree's node sequence.

In addition to being a subsequence, any event executed in between two nodes
of a section belongs to an associated node. To be more accurate, any event in
between entering a section's first and exiting a section's last node belongs
to an associated node. That is because (1) all nodes must be associated
while they are being entered and (2) the section's default scope ends with
the first exit event of a presequent (i.e. with regards to the first node)
and unassociated node.
