
<!-- ======================================================================= -->
# Subtrees

* (/see/ "subgraph" in "graph theory" /)

<!-- ======================================================================= -->
## subtree

A **(simple) subtree** `S := (T,U)` is a subgraph of a graph `G := (V,E)`
such that `S` has the characteristics of a tree (i.e. `isTree(S)` is true).
(Note that the nodes in `S` are vertices in `G`).

* `(S subtree-of G) := (S subgraph-of G) and isTree(S)`
* `(S subtree-of G) -> (#T <= #V) and (#U <= #E)`

That is, the super-graph `G` is not required to be a tree, which is why `G`
may or may not be a tree `G := (N,E)`. Because of that, the focus of this
definition is on the subgraph. However, depending on a given context, `S`
and `G` may both be required to have further characteristics.

Note that a subtree is commonly defined as: "A connected subgraph of a tree".
Since this definition requires the super-graph `G` to be a tree, the subgraph
`S` is as a consequence a tree. Because of that, this common definition is
more specific than the above.

A **strict/proper subtree** `S := (T,U)` is a subtree formed from a graph
`G := (V,E)` by removing at least one vertex and/or edge. Hence, any tree
is a (simple) subtree, but no proper subtree to itself.

* `(S proper-subtree-of G) := (S subtree-of G) and (S != G)`
* `(S proper-subtree-of G) -> (#T < #V) and/or (#U < #E)`

Note that the graph-based definitions of "related-to", "properly-related-to"
and "unrelated-to" are also applicable in the context of trees.

<!-- ======================================================================= -->
## induced subtree

An **induced subtree** `S := (T,U)` is an induced subgraph formed from another
graph `G := (V,E)` such that `S` is a tree.

* `(S i-subtree-of G) -> (S i-subgraph-of G) and isTree(S)`

Similar as before, this definition does also not require the super-graph `G`
to be a tree. In addition to that, and like any other graph, an induced subtree
may be induced by a subset of vertices (i.e. `S := G[T]`), or by a subset of
edges (i.e. `S := G[U]`).

An **induced strict/proper subtree** `S := (T,U)` is an induced subtree formed
from another graph `G := (V,E)` by removing at least one vertex and/or edge.
(Note that `S` may also be referred to as a "strict/proper induced subtree").

* `(S ip-subtree-of G) -> (S ip-subgraph-of G) and isTree(S)`

<!-- ======================================================================= -->
## remarks

() As can be seen by the following example, not even the super-graph of an
induced proper subtree is necessarily a tree. Because of that, and if needed
in a given context, there would have to be an explicit requirement that the
super-graph of a tree is itself required to be a tree.

Example: `G := (V,E)` is a forest of two trees: a tree that only has a single
node, and another disjoint tree with two or more nodes. `G[E]` is therefore an
induced proper subtree, even though all the edges in `G` are used to form the
subtree. In contrary to that, `G[V]` is equal to `G` and thus not a subtree.

() In general, `G[T]` must be connected, since `S` can otherwise not be a
subtree. Put differently, `S` must be the subtree of a component in `G`.
That requirement is however met, if `G` is itself connected (e.g. a tree).

<!-- ======================================================================= -->
# subtrees of trees

A (simple) **subtree** `S := (T,U)` of tree `G := (N,E)` is formed by removing
nodes and/or edges such that `S` is a tree. As such, a subtree is a connected
subgraph of a tree.

* `(U intersects E) -> (T intersects N)`
* `(S subtree-of G) -> (S subgraph-of G)`
* `(S subtree-of G) -> (T subset-of N) and (U subset-of E)`
* `(S subtree-of G) -> (#T <= #N) and (#U <= #E)`

A **strict/proper subtree** `S := (T,U)` of tree `G := (N,E)` is formed by
removing at least one node and/or edge such that `S` is a tree.

* `(S proper-subtree-of G) -> (S proper-subgraph-of G)`
* `(S proper-subtree-of G) -> (S subtree-of G) and (S != G)`
* `(S proper-subtree-of G) -> (#T < #N) and/or (#U < #E)`

<!-- ======================================================================= -->
## remarks

() In the overall context of this discussion, the super-graph `G := (V,E)` of
a subtree `S := (T,U)` is in general expected to be a tree (i.e. `G := (N,E)`)
and any of its subtrees are assumed to be induced proper subtrees.

() In general, a tree `G := (N,E)` can be formed by adding child nodes to their
parent nodes. As such, a tree has one and only one edge that connects a child
with its parent. And because a tree must by definition have exactly one root,
any tree has `(#N-1)` edges and `(#E+1)` nodes. The number of elements in both
sets are therefore coupled with each other.

* `isTree(G) -> (#E == #N-1)`, if `G := (N,E)` and `(#N > 1)`
* note - `(#E < #N)` is always true for any tree

() If both trees have the same root (i.e. `(RN(S) == RN(G))`), then any subtree
`S := (T,U)` of tree `G := (N,E)` can be formed by iteratively removing a leaf
and its incident edge.

() Any subtree `S := (T,U)` of tree `G := (N,E)` can be formed by successively
removing the root and/or a leaf. (Obviously, a root can only be removed, if it
has one child only).

Note that the removal of a leaf and its incident edge will always yield a
subtree. In contrary to that, the removal of a parent and its incident edges
does not necessarily yield a tree since the result will be a sub-forest (i.e.
a multi-component non-tree subgraph) if the parent is itself a child, or if
the parent has more than one child.

<!-- ======================================================================= -->
## a generic method to form a subtree

Obviously, there are several ways to form a subtree `S := (T,U)` based on a
super-tree `G := (N,E)`. However, and independently of how exactly a subtree
is formed, a subtree must be a tree and therefore always have a single root
`r`. All the nodes of `S` must consequently be descendants of `r` in `G`.

Note that the root of `S` is not required to be identical to the root of `G`
(i.e. `(RN(S) == RN(G)` is not necessarily true).

However, a subtree is in general not required to include all the descendants
of `r` in `G`. Consequently, `S` may have leaf nodes that are no leaf nodes
in `G`. Because of that, the subtree of a tree can in general be defined by
its root `r` and by its set of leaf nodes `LS` since every node in a tree
always has a unique rooted path.

A **generic subtree** may be formed as `S := subtreeOf(G,r,LS)`, where ...

* `subtreeOf(G,r,LS)` := the union of all top-down paths in `P`
* `P(G,r,LS) := { (p in G) | p := (r,...,l) for a leaf (l in LS) }`
* i.e. `(#P == #LS)` is true

That is, the paths in `P`, begin in `r` and end in a leaf `l` of `S`. Hence,
each top-down path in `P` is a root-to-leaf path in `S` and as such understood
to define a path graph. Because of that, the resulting subtree can be formed
as the union of path graphs.

Note that any tree, which can be formed based on this generic method, may be
referred to as a "generic subtree". Hence, the set of all generic subtrees
that can be formed based on a given tree may be referred to as the tree's
"class of generic subtrees".

<!-- ======================================================================= -->
## induced by a subtree's root

A disadvantage of this generic method is that one first has to determine for
each node in `G`, whether or not that node is a node in `S`. Based on these
nodes, one then has to determine the root `r` of `S` and its leaf nodes `LS`.
However, the second aspect (i.e. determining the leaf nodes) can be greatly
simplified, if none of the descendants of `r` in `G` are excluded. That is,
if all the descendants of `r` that are leaf ondes in `G` are included.

An **induced subtree** may be formed as `S := subtreeOf(G,r)`, where ...

* `subtreeOf(G,r) := G[r] := G[OS(r)]`

That is, such a subtree is defined as an induced subtree, induced by a subset
of nodes. Simply put, this class of subtrees contains those subtrees that are
**induced by the subtree's root** (i.e. `G[r]`). Or more accurately, induced
by the outer set of nodes of the subtree's root (i.e. `G[OS(r)]`). (Note that
the outer set of any node includes all the descendants and therefore any leaf
that is descendant to the given root in the super-tree).

Note that the inner sets of nodes in `G` can not be used to induce subtrees.
That is because the subgraphs induced by the inner set of a node are in general
forests (i.e. unions of subtrees). In addition to that, the subgraph induced
by the inner set of a leaf is always empty.

Note that any subtree of a tree, that can be formed based on this (simplified)
method, will be referred to as an "induced subtree". Hence, the set of induced
subtrees that can be formed based on a given tree will be referred to as the
tree's "class of induced subtrees". (Note that an induced subtree is still a
generic subtree as defined above, and that a tree's class of induced subtrees
is a sub-class of the tree's class of generic subtrees).

<!-- ======================================================================= -->
## example

```
tree S            tree T           tree U
=============     ===========      ========
1 -|-> 2 -> 4     1 -> 2 -> 4      1 -|-> 2
   |-> 3                              |-> 3
```

S compared to T:

* `T` is a (generic) subtree of `S`
* `T` and `S` do not overlap/cross each other
* `T` is no induced subtree of `S` - i.e. `(T != S[1])`
* note - `3` is no node and therefore no leaf in `T`

T compared to U:

* `T` and `U` overlap/cross  each other
* note - `4` is no node and therefore no leaf in `U`
* note - `3` is no node and therefore no leaf in `T`

S compared to U:

* `U` is a (generic) subtree of `S`
* `U` and `S` do not overlap/cross each other
* `U` is no induced subtree of `S` - i.e. `(U != S[1])`
* note - `2` is a leaf in `U`, but no leaf in `S`
* note - `4` is no node and therefore no leaf in `U`

Note that not every generic subtree is an induced subtree of the form `G[r]`.
Because of that, the class of induced subtrees of a tree has fewer elements
than its class of generic subtrees.
