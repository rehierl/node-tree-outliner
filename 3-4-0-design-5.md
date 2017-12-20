
<!-- ======================================================================= -->
# Design (5)

**CLARIFICATION**
A non-empty section can be seen to *end with an associated container*, if the
section's last node is the last subsequent descendant of that container.

**CLARIFICATION**
A section can be seen to *end inside of an associated container*, if the last
subsequent descendant of that container is the section's last node.

Note that this perspective can be misleading. That is, because a section can
only end with the last subsequent descendant (i.e. not some arbitrarily selected
descendant).

**CLARIFICATION**
A section can be seen to *end with an unassociated container*, if the section's
last node is the container's last subsequent descendant. Consequently, any
remaining open section can be seen to end with the tree's root node.

**CLARIFICATION**
The last node of a non-empty section will always be a leaf (either by strict,
or by loose association). Put differently, the last node of a section will never
be a parent node.

That is, because the last descendant entered will always be a leaf. After all,
a section's last node would not be the section's last node, if it were a parent.

However, no such clarification can be derived for the first node of a section.
That is, because the first node of a section depends on the definition of the
sectioning node. In addition to that, such a definition should in general be
independent of a tree's structure.

**CLARIFICATION**
In contrary to a section's first node, it is in principle not possible to
clearly identify a section's last node independently of any specific structure.
For obvious reasons, the same applies to the the relationship between a
section's first and last node.

That is, because any associated node can potentially have any number of
descendant nodes. Consequently, if the defined last node had a descendant,
then that last node would not be the section's last node. Due to the loose
associations mentioned earlier, the node tree and the definition would then
be in conflict with each other.

<!-- ======================================================================= -->
## question

Because the last node of a section can not be clearly identified, the question
where a section has to end is similar to the definition of intervals on the set
of real numbers. That is, because in between any two real numbers, there always
is an infinite amount of additional numbers.

Apart from a specific and included upper boundary, it is possible to specify
an interval of real numbers by exclusion: `r in [a,b)`. The meaning of this
specification is that `r` may have any positive value in between `a` (inclusive)
and `b` (exclusive). Put differently, any number from `a` to `(b - e)` is
included, if `e` (epsilon) represents an infinitesimal small positive number.

**QUESTION**
Is it possible to define the end of a section in terms of an (enter or exit)
event, beginning with which no more associations are allowed?

To be more clear, once such an event is entered, the corresponding section or
multiples thereof must be immediately closed. That is, not even the event is
allowed to establish any association before closing these sections.

<!-- ======================================================================= -->
## available events

The first events possible, that can be used to end a given section are the exit
events of the last node's ancestors.

<!-- ======================================================================= -->
## Sectioning nodes (3) - last nodes

Consequently, the general definitions mentioned below define the default scope
for certain types of sectioning nodes. However, it is still allowed to define
additional characteristics (e.g. rank of a heading) which further limit the
scope of a presequent sectioning node.
