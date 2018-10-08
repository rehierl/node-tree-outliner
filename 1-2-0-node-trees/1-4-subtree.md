
<!-- ======================================================================= -->
# Subtrees

A (simple) **subtree** `S := (M,F)` is the subgraph of a graph `G := (V,E)`
such that `S` is a tree. (Note that the nodes in `S` are the vertices in `G`
and that `G` itself may or may not be a tree `T := (N,E)`).

Note that the super-graph `G` is itself not required to be a tree. The focus
of this definition is therefore on the characteristic of the subtree itself.
However, `S` may still satisfy further restrictions.

Note that a subtree is commonly defined as: "A connected subgraph of a tree".
By that definition, the super-graph `G` is consequently required to be a tree.
And because the subgraph `S` is required to be a connected subgraph of `G`, `S`
itself is a tree. This definition is therefore more specific than the above.

A **strict/proper subtree** is formed by removing at least one vertex and/or
edge (i.e. `(#M < #V)` and/or `(#F < #E)`). That is, any tree `G` is a (simple)
subtree, but no proper subtree to itself.

An **induced subtree** `S := (M,F)` is an induced subgraph formed from another
graph `G := (V,E)` such that `S` is a tree. (Note that an induced subtree may
be induced by a subset of vertices (i.e. `G[M]`), or by a subset of edges (i.e.
`G[F]`)).

An **induced strict/proper subtree** `S := (M,F)` is an induced subtree formed
from a graph `G := (V,E)` by removing at least one vertex and/or edge (and may
also be referred to as a "strict/proper induced subtree").

Note that the requirement of having fewer vertices and/or edges is with regards
to the resulting subtree. That is, the subset of vertices or edges used to form
the subtree is itself not required to have fewer elements than the corresponding
set of the super-graph.

<!-- ======================================================================= -->
## general remarks

() As can be seen by the following example, not even the super-graph of an
induced proper subtree is itself required to be a tree.

Example: `G := (V,E)` is a forest of two trees; a tree that only has a single
node, and another tree that has two or more nodes. Hence, `G[E]` is an induced
proper subtree, even though all the edges in `G` are used to form the subtree.

Note that `G[E]` is the only example possible such that the complete set of
vertices, or the complete set of edges in `G` will yield an induced proper
subtree. In contrary to that, `G[V]` will always result in `S` being equal to
`G`. That is because `G` must itself be a tree for `G[V]` to result in a tree.

() In general, `G[M]` must be connected, as otherwise no subtree could be formed.
Put differently, the resulting subtree must be a subtree of a component in `G`.
That requirement is obviously met, if `G` is itself a tree.

() A proper subtree `S := (M,F)`, induced from a tree `T := (N,E)` by a proper
subset of nodes (i.e. `S := T[M]` where `(#M < #N)`), also has fewer edges than
its super-tree (i.e. `(#F < #E)`). That is because any tree has a single root
and only one parent per child node.

() In the context of this discussion, the super-graph `G := (V,E)` of a subtree
`S := (M,F)` is itself expected to be a tree (i.e. `G := T` where `T := (N,E)`)
and any sub-tree is assumed to be a non-empty induced subtree of such a tree.

<!-- ======================================================================= -->
## a generic method to form subtrees

Obviously, there are multiple ways to form a subtree `S` from its super-tree
`T`. However, and independently of how exactly a subtree is formed, a subtree
must itself be a tree and therefore always have a single root `r`. All the
other nodes in a subtree must consequently be descendant to that root node.

Note that the root `r` of subtree `S` is not necessarily identical to the root
of its super-tree `T` (i.e. `(RN(S) == RN(T)` is not required to be true).

Like any other tree, each node in `S` has a unique rooted path in `T`. However,
a subtree is in general not required to include all the descendants `d` of `r`
in `T`. Consequently, `S` may have leaf nodes that are no leafs in `T`. Because
of that, the subtree of a tree can in general be defined by its root `r` and
by its set of leaf nodes `LS`.

A **generic subtree** may be formed as `S := subtreeOf(T,r,LS)`, where ...

* `subtreeOf(T,r,LS)` := the union of all paths in `P`, and ...
* `P(T,r,LS) := { p | p := (r,...,l) for a leaf (l in LS) }`

That is, the top-down paths in `P` over `T`, begin in `r` and end in a leaf
`l` of the subtree `S`. (Obviously, each path in `P` is a root-to-leaf path
in `S`). As such, all paths in `P` can be understood to define path graphs.
Consequently, the resulting subtree can be formed as the union of such rooted
paths.

Note that any tree, which can be formed based upon the above generic method,
can also be expressed as an induced subtree. That is, if the subtree is
induced by the appropriate set of elements (i.e. a set of vertices or edges).

Note that any tree, which can be formed based upon the above generic method,
may be referred to as a "generic subtree". Hence, the set of generic subtrees
which can be formed based upon a given tree may be referred to as the tree's
"class of generic subtrees".

<!-- ======================================================================= -->
## a simple method to form subtrees

A disadvantage of the generic method is that one first has to determine for
each node in `T`, whether or not that node is a node of the subtree `S`. Based
on these nodes, one then has to determine the root `r` of `S` and its leaf
nodes `LS`. However, the second aspect (i.e. determining the leaf nodes) can be
simplified, if all the descendants of `r` in `T` are (by definition) included
in `S`.

An **induced subtree** may be formed as `S := subtreeOf(T,r)`, where ...

* `subtreeOf(T,r) := T[OS(r)]`, and ...
* `r` is the root of `S` in `T`

That is, such a subtree is defined as an induced subtree. Simply put, this
class of subtrees contains trees that are "induced by the corresponding (root)
node". Or, more accurately, induced by the outer set of nodes of a subtree's
root. (Note that the outer set of any node includes all the leaf nodes that
are descendant to the given node in `T`).

Note that the inner sets of nodes in `T` can not be used to induce subtrees.
That is because the subgraphs induced by inner sets of nodes are in general
forests (i.e. unions) of subtrees. In addition to that, the induced forests
of leaf nodes are always empty.

Note that any tree, that can be formed based upon this (simplified) method,
will in general be referred to as an "induced subtree". Hence, the set of
induced subtrees that can be formed based upon a given tree will be referred
to as the tree's "class of induced subtrees". (Note that an induced subtree
is still a generic subtree, and that a tree's class of induced subtrees is
a sub-class of the tree's class of generic subtrees).
