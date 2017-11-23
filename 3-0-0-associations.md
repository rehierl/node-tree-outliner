
<!-- ======================================================================= -->
# Associations

A process of some sort is required that enters and exits the nodes of a tree
in some particular order (=> tree traversal).

As a result, a non-empty tree always has a node that will be entered first and
a node that will be entered last. Consequently, any node, except for the first
and the last nodes themselves, is, based on the order of enter events,
subsequent to the first and presequent to the last node (=> node sequence).

* `ns := [n1,...,nk]`, `ni in N`, `ns in N^k`
* `n1` was entered first and `nk` was entered last

At some point in this process, nodes will eventually be entered that declare
(aka. introduce) the existence of a new section (=> sectioning nodes).

* Any sectioning node always declares a single new section.
* This defines a one-to-one (1:1, NxS) relation (i.e. `(n declares s)`).
* Any section can be identified by its sectioning node.
* There is no knowledge of a section before its sectioning node is entered.
* No section can exist without first being declared by some sectioning node.

If a node `x` declares section `s`, then any node `(y subsequent-to x)` may be
associated with that section. In addition to that, nodes may be subsequent to
any number of sectioning nodes.

* A sectioning node is insequent and therefore not subsequent to itself.
* However, it still is technically possible to associate a sectioning node
  with the section it declares (i.e. with its own section). That is because
  a section's existence is known as soon as its sectioning node is entered.
* Nodes can potentially be associated with multiple sections, if all of these
  were declared by presequent sectioning nodes (i.e. presequent section).

Naturally, rules are required that allow to determine with which section, or
multiples thereof, a node must be associated. For the moment, it can only be
assumed that such rules exist.

If these rules allow to determine that node `n` must be strictly associated
with section `s`, then node `n` must be added to that section as one of its
elements. Technically, this operation defines an unrestricted many-to-many
(N:M, SxN) relation (i.e. `(s contains n)`).

* A section `s` is related to node `n` (and vice versa),
  as soon as node `n` is added to section `s`.
* No section can contain any node multiple times.
