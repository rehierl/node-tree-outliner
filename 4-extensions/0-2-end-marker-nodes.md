
<!-- ======================================================================= -->
# A dedicated end-marker node

**CLARIFICATION**
End-marker nodes do not belong to the sections they close.

That is because type-1 close modifiers are the only generic option. Because of
that, end-marker nodes will never be associated with the section's they close.

<!-- ======================================================================= -->
## associating end-marker nodes

End-marker nodes do not belong to the sections they close:
Consistency with the association of sectioning nodes.

Because sectioning nodes can be tagged with the end-marker role, associating
sectioning nodes with the sections they declare would be inconsistent with that
role. That is, because (1) end-marker nodes are by definition associated with
the parent section of the most significant to-be-closed section (i.e. the new
current section). In addition to that, (2) sectioning nodes are defined to be
associated with the parent section of the section they declare.

In essence, and because sectioning nodes can in principle also be end-marker
nodes, the association of both roles is consistent throughout all nodes that
can be associated with the corresponding roles. That is, there are no cases
in which nodes will be associated any other way than what is required by their
default definition.

Note that this is yet another reason as to why not to associate sectioning
nodes with the sections they declare (see "Association of sectioning nodes").

<!-- ======================================================================= -->
## associating end-marker nodes

End-marker nodes do not belong to the sections they close:
Consistent association of section borders (aka. a section's frame).

Sectioning nodes must be associated with the parent section of the section they
declare. If, in contrary to that, a subsequent end-marker node would have to be
associated with the (first) section it is supposed to close, then the frame of
the section would partially belong to its parent section (sectioning node) and
partially to the subsection itself (end-marker node).

In contrary to that, and if a section would end with its parent container (i.e.
no end-marker node), then a subsection's frame would have no contact with the
subsection itself. That is, because a section's parent container either belongs
to a section's parent section, or to one of its ancestor sections.

Consequently, the most "accurate" statement that can be made with regards to a
section's border is, that those nodes belong to a section's ancestor sections.

<!-- ======================================================================= -->
## dedicated end-marker nodes

**CLARIFICATION**
As mentioned before, a dedicated end-marker node can be defined, which
instructs to always close the current section:

* `<close /> := <div close="1"/>`

Note that such a node would act as a counter-part to type-2 sectioning nodes.
That is, sectioning nodes declare a new subsection, and such a dedicated node
closes the last declared subsection.

Note that an implementation will still have to ignore the close modifier of
such a node, if closing a section would result in contradictory statements.
That is, the placement of such a node by itself does not guarantee that its
close modifier is relevant.

**CLARIFICATION**
The descendants of an end-marker node can not have a meaning with regards to
those sections that will be closed by it. These nodes can only have a meaning
with regards to an end-marker node's parent section.

That is, because in contrary to type-2 sectioning nodes, the descendants of
such a (type-1 end-marker) node will be entered after closing the corresponding
sections. And, because of that, those descendant nodes can no longer be used
to change any property (e.g. footer) of the then-already closed sections. This
would otherwise be in conflict with the closed state of a section.

In addition to that, an attempt to associate the meaning of descendants with a
to-be-closed section would mean that the section has to remain open until the
dedicated end-marker node will be exited. Because of that, the node and all of
its descendants will be associated with the to-be-closed section. And because
of that, the dedicated end-marker node would instead be a type-2 end-marker
node (i.e. `<div close_exit="1"/>` instead of `<div close_enter="1"/>`, or
simply `<div close="1"/>`) . By itself, that would not be an issue. However, it
would still add inconsistency to the design, as then some end-marker nodes would
be associated with the sections they close, and others would not. Consequently,
additional logic would be required in order to tell those cases apart. Note that
this aspect not just applies to reading the outline, but also to the support of
transformations.

**CLARIFICATION**
In order to avoid confusion, dedicated end-marker nodes should in general be
defined to be empty (i.e. have no descendants).

Note that it is not possible to define that the descendants of end-marker nodes
must be treated as inactive nodes. That is, because type-1 sectioning nodes may
very well be tagged with the end-marker role.
