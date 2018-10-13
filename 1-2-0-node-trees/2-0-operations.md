
<!-- ======================================================================= -->
# Operations on trees

Any operation on a tree is by definition also an operation on the tree's graph.
Because of that, and unless stated otherwise, any operation defined for a graph
can be used in the context of a tree. The following content therefore focuses
on those aspects that arise, if such operations are executed on node trees.

<!-- ======================================================================= -->
## general remarks

If two graphs have an edge in common, then both graphs also have the endpoints
of that edge in common. In contrary to that, two graphs may have one or more
vertices, but no edge in common.

The execution of binary operations on graphs must in general take the semantics
of both graphs into account. That is, the semantics of two graphs, for which
such an operation has to be executed, are expected to be similar or even
identical.

Because issues arise, if arbitrary trees are processed (i.e. arbitrary sets of
nodes and arbitrary connections between those nodes), the following conditions
are expected to hold:

(1) The nodes in trees `S` and `T` must be connected in a similar fashion.
That is, if trees `S` and `T` have nodes `a` and `b` in common, and if `S`
has a path `p := aPb`, then that path `p` must also exist in `T`. The main
focus is that `a` can not be an ancestor of `b` in `S` and a descendant of
`b` in `T`.

(2) In general, a common node must be a descendant of common ancestors. That is,
if trees `S` and `T` have node `n` in common, and if `n` has `a` as an ancestor
in `S`, then `a` must also be an ancestor of `n` in `T`. The main focus is that
both trees in general need to have all of the ancestors of a common node in
common.

(3) The node trees `S` and `T` must have the same child order. That is, if trees
`S` and `T` have nodes `a` and `b` in common, and if `b` is the next sibling of
`a` in `S`, then `b` must also be the next sibling of `a` in `T`. The main focus
is that `a` can not be presequent to `b` in `S` and subsequent to `b` in `T`.

(4) The non-empty intersection between two trees `S` and `T` must be a single
tree. The main focus is that the non-empty intersection between both trees is
a subtree to both.

In general: Two trees are expected to be of similar kind and content. That is,
the semantics of the contents in both trees are expected to not be in conflict
with each other.

<!-- ======================================================================= -->
## unary operations

Any tree can be transposed. However, the resulting converse graph `T°` is not
a tree. The converse graph of a tree has the "child-of" semantics, which is
because a child becomes the parent of its former parent.

Similar to that, the complement graph `T*` of a tree is not tree. That is
because the nodes in such a complement graph have in general "more than one
parent" node.

<!-- ======================================================================= -->
## binary operations

The following binary, graph-based operations may be used without limitation:

* equal, unequal, distinct
* disjoint, coupled, overlap
* subgraph/subtree

Two trees `S` and `T` are said to be **related** with each other,
if one is a subtree of the other:

* `(S related-to T)`, if `(S subtree-of T) or (T subtree-of S)`
* `(S related-to T) <-> (T related-to S)`

<!-- ======================================================================= -->
## intersection (&, and, isect)

The intersection between two trees is expected to be either empty, or a single
tree. That is, a non-empty intersection between two trees must be a subtree to
both.

<!-- ======================================================================= -->
## union (+, or, union)

The result of the graph-based union operation on trees is in general not a tree.
That is, depending on both trees, the result may be a forest, a single tree, or
none of those two (i.e. a general graph).

Because a forest of trees is defined as the disjoint union of trees, the union
of two disjoint trees is obviously a disjoint union of trees and therefore a
forest.

<!-- ======================================================================= -->
## graph difference (\, sub, diff)
