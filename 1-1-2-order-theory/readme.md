
<!-- ======================================================================= -->
# Order theory

This content contains notes on order theory:

* An **ordered set** is a simple set paired with an order relation.
* A **linear set** is an ordered set paired with a linear order.
* A **linear sequence** is a sequence that defines a linear set.

General context:

The nodes within a node tree are not necessarily ordered. That is, each node
may represent data of any kind. Nodes are therefore not required to hold some
property according to which the nodes are, or can be ordered.

In the context of this discussion, the order required is a consequence of a
tree traversal. That is, the node which will be visited first, is the first
node in that order. Furthermore, each node is visited once, which is why the
traversal of a tree can be understood to define an ordered set on the set of
nodes.

Obviously, this kind of node order is "volatile/mutable" as it changes with the
tree's structure; it does not necessarily change with some node property. That
is, if the change of a node property does not also result in a change of the
tree's structure (e.g. balancing operations).

Put together, the traversal of a tree is understood to produce a trace of nodes.
As such, it contains each node exactly once (i.e. a set of nodes). In addition
to that, for any pair of nodes it can be stated which node was visited before
the other (i.e. which node is subsequent to the other, i.e. a totally ordered
set of nodes).

Note that this linear order is reflected by the index each node has within
the node trace. That is, each node is associated with a unique/distinct number
value, and the nodes are ordered according to that value (i.e. a strict
monotone mapping - see also: order isomorphism).
