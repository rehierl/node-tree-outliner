
<!-- ======================================================================= -->
# Derived statements

The focus of the following statements is not to be overly accurate, but
to have easy to understand and easy to remember statements. Because of
that, these statements do no represent any definitions. They merely allow
to loosely describe certain conditions.

**CLARIFICATION**
A section can be understood to *end with an associated container*, if the
section's last node is the last subsequent descendant of that container.

**CLARIFICATION**
A section can be understood to *end inside of an associated container*,
if the section ends with the last subsequent descendant of that container.

Note that this perspective can be misleading. That is, because in order
for that statement to be true, a section must end with the last subsequent
descendant (i.e. not some arbitrary descendant).

**CLARIFICATION**
A section can be understood to *end with an unassociated container*, if
the section's last node is the container's last subsequent descendant. Any
remaining open section can therefore be understood to end with the root node.

Note that the section's sectioning node will either be the unassociated
container itself (type-1), or one of its descendant nodes (type-2). In case
of a descendant type-1 sectioning node, the declared section ends with its
sectioning node, not with the unassociated container.

Note that this perspective is based upon the exit event of the corresponding
unassociated container.

**CLARIFICATION**
A section can be understood to *end with an unassociated node*, if the
last node of a section is strictly presequent (e.g. previous sibling) to
the unassociated node, or if the last top-level node of a section is the
unassociated node's previous sibling.

Note that this perspective is based upon the enter event of the corresponding
unassociated node.

**CLARIFICATION**
Any section can always be understood to end with the next unassociated
container or node.

Note that it depends on the distance between the event of the associated node
and the event of the unassociated container or node: The closer the events are
to each other, the more accurate the statement will be.
