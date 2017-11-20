
<!-- ======================================================================= -->
# Associations

A process of some sort is required to visit the nodes of a tree in some
particular order (=> tree traversal). As a result, there is some node in a
non-empty tree, that will be visited first and some node that will be visited
last. Consequently, any node, except for the first and last nodes themselves,
is subsequent to the first and presequent to the last node (=> node sequence).

* `ns := [n1,...,nk]`, `ni in N`, `ns in N^k`
* `n1` was visited first and `nk` was visited last

At some point in the above process, nodes will be visited that introduce a new
section (=> sectioning nodes).

* Any sectioning node always declares/introduces a single new section.
* No section can exist without first being declared by its sectioning node.
* There is a one-to-one (i.e. 1:1) relationship between the sectioning nodes
  and the sections they declare.
* Any section can be identified by its sectioning node.

Once a sectioning node is reached, any subsequent node may be associated with
the sectioning node's section.

* A sectioning node is insequent, and therefore not subsequent, to itself.
* A sectioning node binds its section to presequent nodes/sections.
* Nodes will potentially be associated with multiple predeclared sections.

Naturally, some rules are required that allow to determine with which section,
or multiples thereof, a node must be associated. For the moment, it can only be
assumed that such rules exist.

If the these rules allow to determine that some node `n` must be associated
with some section `s`, then node `n` must be added to section `s` as one of
its elements. From that point on, `(s related-to n)` is true.

* A section is related to a node (and vice versa)
  as soon as the node is added to the section.
* No section can contain a node multiple times.

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
