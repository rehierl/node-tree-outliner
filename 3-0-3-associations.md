
<!-- ======================================================================= -->
# Associations

A process of some sort is required that enters and exits the nodes of a tree
in some particular order (=> tree traversal).

As a result, there is some node in a non-empty tree, that will be entered first
and some node that will be entered last. Consequently, any node, except for the
first and last nodes themselves, is, based on the order of enter events,
subsequent to the first and presequent to the last node (=> node sequence).

* `ns := [n1,...,nk]`, `ni in N`, `ns in N^k`
* `n1` was entered first and `nk` was entered last

At some point in this process, nodes will eventually be entered that declare
(aka. introduce) the existence of a new section (=> sectioning nodes).

* Any sectioning node always declares a single new section.
* This defines a one-to-one (1:1) relation (NxS) on the
  sectioning nodes and the sections they declare.
* Any section can be identified by its sectioning node.
* There is no knowledge of a section before its sectioning node is entered.
* No section can exist without first being declared by some sectioning node.

If a sectioning node `n` declares section `s`, then any node entered at some
later point in time (i.e. subsequent node) may be associated with section `s`.

* A sectioning node is insequent, and therefore not subsequent, to itself.
* However, technically it is still possible to associate a sectioning node
  with the section it declares (i.e. with its own section). That is because
  a sectioning node has knowledge of the section it declares.
* Nodes can potentially be associated with multiple sections, that all must
  be declared by some presequent nodes (i.e. predeclared sections).

Naturally, rules are required that allow to determine with which section, or
multiples thereof, a node must be strictly associated. For the moment, it can
only be assumed that such rules exist.

If these rules allow to determine that node `n` must be strictly associated
with section `s`, then node `n` must be added to section `s` as one of its
elements. This operation defines the relation (SxN) on the sections and nodes
of a node tree.

* A section `s` is related to node `n` (and vice versa),
  as soon as node `n` is added to section `s`.
* No section can contain any node multiple times.

<!-- ======================================================================= -->
## root node

Because a section can not exist without a presequent sectioning node, the root
node, with which a process has to start, can not strictly be associated with
any section as there is no sectioning node that is presequent to the root.

universal section (u)

The only thing that can be done is to think of the root as being associated
with some universal section `u`. This special section can be understood to
represent a section that hypothetically contains any possible node.

With that in mind, any node of a node tree always belongs to one or multiple
sections. That is, there is no node that does not belong to any section.

the root is sectioning node

Without any further clarification, and assumed that a given root does itself
not (strictly or loosely) contain any other sectioning node, all the nodes in
the root's subtree would be lost inside the universal section. That is, there
is no section that corresponds with their relationship (i.e. located inside of
the very same subtree).

In order to establish that kind of relationship, the root itself needs to
introduce its own section. Consequently, the root node is always considered
to be a sectioning node.

<!-- ======================================================================= -->
## associate operation

Because nodes are visited in some particular order and because nodes are
associated with sections in an order that is based upon the visit order,
the general definition of a section can be clarified as a sequence of nodes:

* `s := [n1,...,nk]` and `(ni != nj)` for `i,j in [1,k]` and `(i != j)`
* Any non-empty section always has a first and a last node.

However, the order of nodes within a section must reflect the order of nodes
within the node tree. After all, any section is intended to accurately represent
some part of the node tree.

<!-- ======================================================================= -->
## sectioning nodes

* A sectioning node binds its section to presequent nodes and sections.
