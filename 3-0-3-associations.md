
<!-- ======================================================================= -->
# Associations

A process of some sort is required to visit the nodes of a tree one after
another (i.e. in some particular order, => tree traversal).

This means that there is some node in a non-empty tree, that will be visited
first and some node that will be visited last. Consequently, any node is,
except for the first and last nodes themselves, subsequent to the first and
presequent to the last node.

* `ns := [n1,...,nk]`, `ni in N`, `ns in N^k`
* `n1` was visited first and `nk` was visited last
* `ns` will be referred to as the "node sequence"

At some point in the above process, specific nodes will eventually be visited
that declare the existence of a new section.

* These kind of nodes will be referred to as "sectioning nodes".
* Assume that there is a one-to-one (in short 1:1) relationship between the
  sectioning nodes and the sections they declare/introduce.
* Any sectioning node always declares a single new section.
* No section can exist without first being introduced by some sectioning node.
* Any section can be identified by its sectioning node.

Once a sectioning node is reached, any subsequent node may be associated with
its section.

* Sections may only have an effect on subsequent nodes.
* No section is defined for presequent nodes.
* **TODO** - associate a sectioning node with its own section?

Naturally, some rules are required that allow to determine with which
predeclared section, or even multiples thereof, a node must be associated.
For the moment, it can only be assumed that such rules exist.

* Nodes may be associated with multiple predeclared sections.

If these rules allow to determine that the current node `n` must be associated
with some predeclared section `s`, then node `n` must be added to section `s`
as one of its elements. From that point on, `(s related-to n)` is true.

* A section is related to a node as soon as the node is added to the section.
* No section can contain a node multiple times.

Because nodes are visited in some particular order and associated with sections
in an order that is based upon the visit order, the general definition of a
section can be clarified as a sequence of nodes:

* `s := [n1,...,nk]` and `(ni != nj)` for `i,j in [1,k]` and `(i != j)`
* Any non-empty section always has a first and a last node.

However, the order of nodes within a section must accurately reflect the order
of nodes within the tree of nodes.
