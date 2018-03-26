
<!-- ======================================================================= -->
# Design - end-marker nodes

**TODO**
so far, only a list of notes

The most relevant option available, with regards to end-marker nodes is case 1:
Close sections while the enter event of an end-marker node is being entered.

The definition of optional end marker nodes (e.g. `<close/>`) must not define
these nodes to be associated with the sections they are supposed close.

That is, because it would be inconsistent with not associating sectioning
nodes with the sections they declare. The subsection's "frame" belongs to
its parent section.

In addition to that, and if such an end marker would be allowed to close
multiple sections at once, then there would be the issue of having to decide
with which of the to-be closed sections it would have to be associated.

The issue with such nodes is that they could be placed inside of a type-1
section. To which section does a subsequent node belong? What happens in
case of user/input errors?

plot twist: see the "extensions" chapter

closing a subsection does not necessarily mean that ancestor sections are
closed as well - in contrary to that, closing an ancestor section requires
that all subsections are closed as well - proof that those nodes must be
associated with the parent section of the most significant section being
closed? - wouldn't add up with close modifiers

a heading that has a rank may/can act as an end-marker node -
that is, a rank value adds an additional role to a heading element -
could that be used to proof that no t1 section can be closed?
