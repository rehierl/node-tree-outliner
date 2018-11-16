
<!-- ======================================================================= -->
# Subtrees

A **(simple) subtree** `S := (M,F)` is the subgraph of a graph `G := (V,E)`
such that `S` is a tree. (Note that the nodes in `S` are vertices in `G`).

Note that the super-graph `G` is not required to be a tree. The focus of this
definition is thus on the characteristic of the subgraph. However, `S` and `G`
may both still satisfy further restrictions.

Note that a subtree is commonly defined as: "A connected subgraph of a tree".
By that definition, the super-graph `G` is required to be a tree. Because of
that, and because the subgraph `S` is required to be a connected subgraph of
a tree, `S` is itself consequently a tree. This definition is therefore more
specific than the above.

A **strict/proper subtree** `S := (M,F)` is a subtree formed from a graph
`G := (V,E)` by removing at least one vertex and/or edge (i.e. `(#M < #V)`
and/or `(#F < #E)`). Because of that, any tree `T` is a (simple) subtree,
but no proper subtree to itself.

An **induced subtree** `S := (M,F)` is an induced subgraph formed from another
graph `G := (V,E)` such that `S` is a tree. (Note that an induced subtree may
be induced by a subset of vertices (i.e. `G[M]`), or by a subset of edges (i.e.
`G[F]`).

An **induced strict/proper subtree** `S := (M,F)` is an induced subtree formed
from a graph `G := (V,E)` by removing at least one vertex and/or edge. (Note
that `S` may also be referred to as a "strict/proper induced subtree").

<!-- ======================================================================= -->
## general remarks

() As can be seen by the following example, not even the super-graph of an
induced proper subtree is required to be a tree.

Example: `G := (V,E)` is a forest of two trees; a tree that only has a single
node, and another tree with two or more nodes. Hence, `G[E]` is an induced
proper subtree, even though all the edges in `G` are used to form the subtree.

Note that `G[E]` is the only example possible such that the complete set of
vertices, or the complete set of edges in `G` may result in an induced proper
subtree. In contrary to that, `G[V]` will always result in `S` being equal to
`G`. That is because `G` must itself be a tree for `G[V]` to result in a tree.

() In general, `G[M]` must be connected, as otherwise no subtree could be
formed. Put differently, the resulting subtree must be a subtree of a component
in `G`. That requirement is obviously met, if `G` is itself connected (e.g.
a tree).

() A proper subtree `S := (M,F)` of a tree `T := (N,E)`, induced by a proper
subset of nodes (i.e. `S := T[M]` where `(M proper-subset-of N)`), also has
fewer edges than its super-tree (i.e. `(F proper-subset-of E)`). That is
because any tree has a single root and only one parent per child.

* `(#M < #N) -> (#F < #E)` if `(S == T[M])`

() In the context of this discussion, the super-graph `G := (V,E)` of a subtree
`S := (M,F)` is in general a tree (i.e. `G := T` where `T := (N,E)`) and any
subtree is assumed to be a non-empty induced subtree of such a tree.

<!-- ======================================================================= -->
## a generic method to form subtrees

Obviously, there are multiple ways to form a subtree `S` from another tree `T`.
However, and independently of how exactly a subtree is formed, a subtree must
itself be a tree and therefore always have a single root `r`. All the other
nodes in subtree `S` must consequently be descendants of that root.

Note that the root of subtree `S` is not required to be identical to the root
of its super-tree `T` (i.e. `(RN(S) == RN(T)` is in general not true).

Like any other node in a tree, each node in `S` has a unique rooted path in `T`.
However, a subtree is in general not required to include all the descendants `d`
of `r` in `T`. Consequently, `S` may have leaf nodes that are no leaf nodes in
`T`. Because of that, the subtree of a tree can in general be defined by its
root `r` and by its set of leaf nodes `LS`.

A **generic subtree** may be formed as `S := subtreeOf(T,r,LS)`, where ...

* `subtreeOf(T,r,LS)` := the union of all paths in `P`, where ...
* `P(T,r,LS) := { p | p := (r,...,l) for a leaf (l in LS) }`

That is, the top-down paths in `P` over `T`, begin in `r` and end in a leaf `l`
of subtree `S`. (Obviously, each path in `P` is a root-to-leaf path in `S`).
As such, all paths in `P` are understood to define path graphs. Consequently,
the resulting subtree can be formed as the union of such graphs.

Note that any tree, which can be formed based upon the above generic method,
may be referred to as a "generic subtree". Hence, the set of generic subtrees
which can be formed based upon a given tree may be referred to as the tree's
"class of generic subtrees".

Note that any tree, which can be formed based upon the above generic method,
can also be expressed as an induced subtree. That is, if the subtree is
induced by the appropriate subset of vertices or edges.

<!-- ======================================================================= -->
## a simple method to form subtrees 

A disadvantage of the generic method is that one first has to determine for
each node in `T`, whether or not that node is a node of subtree `S`. Based
on these nodes, one then has to determine the root `r` of `S` and its leaf
nodes `LS`. However, the second aspect (i.e. determining the leaf nodes) can
be simplified, if all the descendants of `r` in `T` are included in `S`.

An **induced subtree** may be formed as `S := subtreeOf(T,r)`, where ...

* `subtreeOf(T,r) := T[r] := T[OS(r)]`, and ...
* `r` is the root of `S` in `T`

That is, such a subtree is defined as an induced subtree, induced by a subset
of nodes. Simply put, this class of subtrees contains trees that are **induced
by the corresponding (root) node** (i.e. `T[r]`). Or, more accurately, induced
by the outer set of nodes in `T` of the subtree's root (i.e. `T[OS(r)]`). (Note
that the outer set of any node includes all the leaf nodes that are descendant
to the given node).

Note that the inner sets of nodes in `T` can not be used to induce subtrees.
That is because the subgraphs induced by inner sets of nodes are in general
forests (i.e. unions) of subtrees. In addition to that, the subgraph induced
by the inner set of a leaf node is always empty.

Note that any tree, that can be formed based upon this (simplified) method,
will simply be referred to as an "induced subtree". Hence, the set of induced
subtrees that can be formed based upon a given tree will be referred to as the
tree's "class of induced subtrees". (Note that an induced subtree is still a
generic subtree, and that a tree's class of induced subtrees is a sub-class
of the tree's class of generic subtrees).

<!-- ======================================================================= -->
## example

```
tree S            tree T           tree U
=============     ===========      ========
1 -|-> 2 -> 4     1 -> 2 -> 4      1 -|-> 2
   |-> 3                              |-> 3
```

(T compared-to S)

* `T` is a (generic) subtree of `S`
* `T` and `S` do not overlap each other
* `T` is no induced subtree of `S` - i.e. `(T != S[1])`
* note - `3` is not a node and therefore no leaf in `T`

(U compared-to S)

* `U` is a (generic) subtree of `S`
* `U` and `S` do not overlap each other
* `U` is no induced subtree of `S` - i.e. `(U != S[1])`
* note - `2` is a leaf in `U` but no leaf in `S`
* note - `4` is not a node and therefore no leaf in `U`

(T compared-to U)

* `T` and `U` overlap each other
