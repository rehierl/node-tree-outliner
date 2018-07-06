
This chapter contains an overview of relations and orders:

* The **semantics of a relation** associate meaning with its tuples.
* An **ordered set** is a simple set paired with an order relation.
* A **linear set** is an ordered set paired with a linear order.
* A **linear sequence** is a sequence that defines a linear set.
* The semantics of a linear order is the **subsequent-to** (>),
  or (due to duality) the **presequent-to** (<) order.

General context:

The nodes within a node tree are not necessarily ordered; they may represent
data of any kind. That is, the nodes are not required to old some property
according to which the nodes are ordered.

In the context of this discussion, the order required is a consequence of the
tree's traversal. That is, the node which will be visited first, is the first
node in that order. Obviously, this order is "volatile/mutable" as it changes
with every change of the tree's structure; it does not necessarily change with
some node property. That is, if the change of a node property does not also
result in a change of the tree's structure (e.g. balancing operations).

Put together, the tree's traversal is understood to produce a trace of nodes.
As such, it contains each node exactly once (i.e. a set). In addition to that,
for any pair of nodes it can be stated which node was visited before the other
(i.e. which node is subsequent to the other).

Note that this linear order is reflected by the index each node has within
the node trace. That is, each node is associated with a unique/distinct number
value, and the nodes are ordered according to that value (i.e. a strict
monotone mapping - see also: order isomorphism).
