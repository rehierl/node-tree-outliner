
<!-- ======================================================================= -->
# Operations on trees

Any operation on a tree is by definition also an operation on a tree's graph.
Because of that, and unless stated otherwise, any operation defined for a graph
can be used in the context of a tree. The following content therefore focuses
on the problems that arise, if such operations are used in combination with
node trees.

<!-- ======================================================================= -->
## unary operations

Any tree can be transposed. However, the resulting converse graph is no longer
a tree as its semantics will be the `child-of` semantics.

Similar to that, the complement graph `T*` of a tree is not tree because the
nodes in `T*` will in general have more than one "parent" node.

<!-- ======================================================================= -->
## binary operations

The following binary graph-based operations may be used without limitation:

* equal, unequal, distinct
* disjoint, coupled, overlaps
* subgraph/subtree

Recall that binary operations on graphs also need to take the semantics of both
graphs into account. That is, the semantics of both trees, for which such an
operation has to be executed, are expected to be similar (if not identical).

Recall that, if two graphs have an edge in common, then both graphs also have
the endpoints of that edge in common. In contrary to that, two trees may have
nodes but no edge in common.

<!-- ======================================================================= -->
## union (+, or, union)

The result of the graph-based union operation on trees is in general not a tree.
However, depending on the input trees, the result may be a forest, or even a
single tree.

Because a forest of trees is defined as the disjoint union of trees, the union
of two disjoint trees is obviously a disjoint union of trees and therefore a
forest of trees. Hence, the following considerations assume that both trees are
coupled with each other.

<!-- ======================================================================= -->
## intersection (&, and, isect)

<!-- ======================================================================= -->
## graph difference (\, sub, diff)
