
<!-- ======================================================================= -->
# Design (5)

**CLARIFICATION**
A section can be seen to *end with an associated container*, if the
section's last node is the last subsequent descendant of that container.

**CLARIFICATION**
A section can be seen to *end inside of an associated container*, if the
last subsequent descendant of that container is the section's last node.

Note that this perspective can be misleading. That is, because in order
for that statement to be true, a section must end with the last subsequent
descendant (i.e. not some arbitrarily selected descendant).

**CLARIFICATION**
A section can be seen to *end with an unassociated container*, if the section's
last node is the container's last subsequent descendant. Consequently, any
remaining open section can be seen to end with the tree's root.

**CLARIFICATION**
The last subsequent node of a section will always be a leaf (either by strict,
or by loose association). Put differently, the last node of a section will
never be a parent node.

That is, because a section's last node would not be the section's last node,
if it were a parent node (hint: tree traversal).

However, no such clarification can be derived for the first node of a section.
That is, because the first node of a section depends on the definition of the
sectioning node (as it should). In addition to that, such a definition should
in general be independent of a tree's structure.

**CLARIFICATION**
In contrary to a section's first node, it is in principle not possible to
clearly identify a section's last node independently of any specific structure.
Consequently, the same also applies to the the relationship between a section's
first and last node.

That is, because any associated node can potentially have any number of
descendant nodes. Consequently, if the defined last node had a descendant,
then that last node would not be the section's last node. Due to the loose
associations mentioned earlier, the node tree and the section's definition
would then be in conflict with each other.

<!-- ======================================================================= -->
## question

Because the last node of a section can not be clearly identified, the question
where a section has to end is similar to the definition of intervals on the set
of real numbers. That is, because in between any two real numbers, there always
is an infinite amount of additional numbers.

Apart from any specific and included upper boundary, it is possible to specify
an interval of real numbers by exclusion: `r in [a,b)`. The meaning of this
specification is that `r` may have any positive value in between `a` (inclusive)
and `b` (exclusive). Put differently, any number from `a` to `(b - e)` is
included, if `e` (epsilon) represents an infinitesimal small positive number.

**CLARIFICATION**
Recall, that a type-1 section is defined to begin with the sectioning node's
first child. Because of that, and in order to support empty sections, the
definition requires to open the declared section when the sectioning node's
enter event is about to be exited, not when the first node is being entered.
Because of that, the definition of the section's first node can also be
understood to represent a definition by exclusion: The sectioning node is
the last unrelated node entered, but not exited, before the section's first
node is entered. Note that the first node of a type-2 section can be defined
in a similar fashion.

**QUESTION**
Is it possible to define the end of a section in terms of an (enter or exit)
event, beginning with which no more associations are allowed?

To be more clear, once such an event is entered, the corresponding section or
multiples thereof must be immediately closed. That is, not even the event is
allowed to establish any association before closing these sections.

<!-- ======================================================================= -->
## available events

As mentioned before, a section must be empty, if its first node does not exist.
Because of that, and in theory, the very first event that could possibly be used
to close a section is the exit event of a section's first node. Obviously, using
this particular event to end a section by definition would not only cover one
specific case, but it would also make it impossible to support empty sections.
That is, because it would force a section to always have at least one node.

Note that, because no descendant of a top-level node can be excluded, none
of the events of such a descendant node are suited to generically define the
end of a section. That is, because it is in principle not possible to find a
definition based on the descendants of an associated node, which is also
independent of any additional structural requirement. Such a definition would
simply not be generic.

Note that a generic definition is a necessity, as any node of a section is
subsequent to the section's sectioning node. Allowing a requirement, that some
condition must be true with regards to a subsequent node, would mean that the
semantics of a presequent node (i.e. the sectioning node) would depend on nodes
that are subsequent to it.

Note that, in order to generically define the end of a section, a definition
also needs to be independent of any specific type of sectioning node. That is,
because a definition that is based upon a specific type of sectioning node is
not completely generic (i.e. generic with regards to subsequent nodes, but not
generic with regards to the sectioning node's type). Because of that,  such a
definition needs to define the end of a section in terms of the relationship
the section's end has with regards to the section's first node.

Note that this is yet another indication to not associate sectioning nodes with
the sections they declare: It would otherwise not be possible to define the end
of a section independently of a sectioning node.

**DEFINITION**
The maximum (i.e. widest) scope of a section, that does not produce any
conflict, is said to be "the default scope of a section".

Note that generically defining the end of a section can only define a section's
default scope. In principle, additional rules (e.g. rank) can still be defined
that allow to further limit the scope of a section (hence, default scope).

**CLARIFICATION**
The search for an event that could allow to define the end of a section is
limited to (1) the exit event of a section's last top-level node, (2) the enter
event of the first unrelated node, and (3) an exit event of one of the top-level
node's ancestors.

Note that the enter event of a top-level node can not be taken into account, as
this would produce a conflict: A top-level node is a top-level node, because it
is associated with a section. Making use of the enter event of such a node would
result in not associating the top-level node. Such a definition would therefore
be equivalent to case (2) and, because of that, be in conflict with the
definition of a top-level node.

Note that the enter events of one of the top-level node's ancestors can not be
used. That is, because in order to enter a sectioning node, all of its ancestors
must have already been entered. Put differently, no node can be entered and,
because of that, associated, if its ancestors have not been entered already
(i.e. these enter events are no longer available).

### exit a top-level node

Case (1) is not suited for a generic definition.

That is, because it would require that an algorithm had the means to detect
whether a node is the section's last top-level node. Because of that, such a
definition would add an additional structural requirement (e.g. the n-th
top-level node, or a node of some specific type must exist).

Note that such a definition could also be seen as "a loose definition by
inclusion" ("inclusion" because the last top-level node is explicitly included,
"loose" because of the implicit inclusion of any loosely associated descendant).

However, the most important issue with this case is that it would add the
requirement, that any section must always have at least one node. That is,
because the section's close event could otherwise not be triggered. As such,
this case can not be used for a generic definition.

Apart from that, such a definition could also be considered to be inconsistent
with the definition of a sectioning node: Why consider a sectioning node to not
belong to its own section, but, in contrary to that, associate an end marker
with the section it is supposed to end (i.e. either all in, or all out)?

### enter an unassociated node

Case (2) is not suited for a generic definition.

That is, because it would require to give a guarantee that such a node will
always be entered eventually. Consequently, such a definition would add an
additional requirement and, because of that, would not be generic.

However, it is still possible to define specific nodes that, when entered,
end one or more presequent sections. The focus here is that such a node is
optional and, because of that, not guaranteed to be entered.

### exit an ancestor of the first node

Case (3) is somewhat suited for a generic definition.

Except for the root node, any node in a rooted tree of nodes always has at
least one ancestor. Because of that, and with regards to the ancestors of
the first sectioning node, no additional requirements are added, if case
(3) is limited to the exit event of the first node's parent.

Any attempt to use the exit event of any other ancestor will add an additional
requirement. That is, because from the perspective of the definition of a
sectioning node, other ancestors are not guaranteed to exist. Put differently,
and unless defined otherwise, a sectioning node can be a direct descendant
(i.e. child) of the root and, as such, does not have any ancestor other than
its parent (i.e. the root).

However, this case requires that a section always has a first node ...

**CLARIFICATION**
The exit event of a sectioning node's parent node is the only event that
can be used to generically limit the scope of a section.

<!-- ======================================================================= -->
## the default scope

Just because an event can be used to generically limit the scope of a section,
it does not mean that it would be reasonable to do so. Because of that, it is
necessary to take a look at which effects such a definition would have. **TODO**

Consequently, the definition of a section is actually a definition by exclusion:
`r in (a,b)`. That is, any positive number in between `(a+e)` and `(b-e)` is
included.
