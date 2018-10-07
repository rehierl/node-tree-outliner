
<!-- ======================================================================= -->
# Subtrees

A (simple) **subtree** `S := (T,U)` is a subgraph of a graph `G := (V,E)` such
that `S` is a tree. Obviously, the vertices of `G` are the nodes of `S`.

Note that the super-graph `G` is itself not required to be a tree. Hence,
the focus of this definition is on the characteristic of the subtree itself.
However, `S` may still satisfy further restrictions.

Note that a subtree is commonly defined as: "A connected subgraph of a tree".
Because of that, this definition requires `G` to be a tree. Consequently, and
because `S` is a connected subgraph of `G`, `S` is itself a tree. The common
definition is therefore more specific than the above definition.

A **strict/proper subtree** is formed by removing at least one vertex and/or
edge (i.e. `(#T < #V)` and/or `(#U < #E)`). That is, any tree `G` is a (simple)
subtree, but no proper subtree to itself.

An **induced subtree** `S := (T,U)` is an induced subgraph formed from another
graph `G := (V,E)` such that `S` is a tree. (Note that an induced subtree may
be induced by a subset of vertices (i.e. `G[T]`), or by a subset of edges (i.e.
`G[U]`)).

An **induced strict/proper subtree** `S` is an induced subtree formed from a
graph `G` by removing at least one vertex and/or edge. Such a subtree may also
be referred to as a "strict/proper induced subtree".

Note that the requirement of having fewer vertices and/or edges is with regards
to the result. That is, the subset of vertices or edges used to form the subtree
is itself not required to have fewer elements than the corresponding set of the
super-graph.

Example: `G` may be a forest that has two trees. One that consists of a single
node, and another that is a tree of two or more nodes. Hence, `G[E(G)]` is an
induced proper subtree, even though all the edges in `G` are used to form the
subtree.

Note that not even the super-graph of an induced proper subtree is required to
be a tree (e.g. a subtree in a forest of trees).

Note that an induced proper subtree `G[T]`, formed from another tree and induced
by a proper subset of nodes, will also have fewer edges than its super-tree -
i.e. `(#U < #E)`. That is because all trees have a single root and one parent
per child.

<!-- ======================================================================= -->
## a generic method to form subtrees

Note that, in the context of this discussion, the super-graph of a sub-tree is
expected to be an arborescence and any sub-tree is assumed to be a non-empty
induced subtree of such a super-tree.

Obviously, there are multiple ways to form a subtree `S` from its super-tree
`T`. However, and independently of how exactly a subtree is formed, a subtree
must itself be a tree and therefore always have a single root `r`. All the
other nodes in a subtree must consequently be descendants of that root node.

Note that the root `r` of subtree `S` is not necessarily identical to the root
of its super-tree `T` (i.e. `(RN(S) == RN(T)` is in general not true).

Like any other tree, each node in `S` has a unique rooted path in `T`. However,
a subtree is in general not required to include all the descendants `d` of `r`
in `T`. Consequently, `S` may have leaf nodes that are no leafs in `T`. Because
of that, the subtree of a tree can in general be defined by its root `r` and
by its set of leaf nodes `LS`.

A **generic subtree** may be formed as `S := subtreeOf(T,r,LS)`, where ...

* `subtreeOf(T,r,LS)` := the union of all paths in `P`, and ...
* `P(T,r,LS) := { p | p := (r,...,l) for a leaf (l in LS) }`

That is, the top-down paths in `P` over `T`, begin in `r` and end in a leaf
`l` of the subtree `S`. As such, all paths in `P` can be understood to define
path graphs. Consequently, the resulting subtree can be formed as the union
of these rooted paths.

Note that any tree that can be formed based upon the above method may be
referred to as a "generic subtree". Hence, the set of generic subtrees that
can be formed based upon a given tree may be referred to as the tree's "class
of generic subtrees".

<!-- ======================================================================= -->
## a simple method to form subtrees

A of the disadvantages of the above generic method is that one first has to
determine for each node in `T`, whether or not that node is a node of the
subtree `S`. Based on these nodes, one then has to determine the root `r` of
`S` and its leaf nodes `LS`. However, the second aspect (i.e. determining
the leaf nodes) can be simplified, if all the descendants of `r` in `T` are
(by definition) included in the subtree `S`.

An **induced subtree** may be formed as `S := subtreeOf(T,r)`, where ...

* `subtreeOf(T,r) := T[OS(r)]`, and ...
* `r` is the root of `S` in `T`

That is, such a subtree is defined as an induced subtree. Simply put, these
kind of subtrees are "induced by the corresponding (root) node". Or, more
accurately, induced by the outer set of nodes of the subtree's root. (Note
that the outer set of any node includes all the leaf nodes that are descendant
to the given node).

Note that the inner sets of nodes in `T` can not be used to induce subtrees.
That is because the subgraphs induced by inner sets of nodes are in general
forests (i.e. unions) of subtrees. In addition to that, the induced forests
of leaf nodes are always empty.

Note that any tree that can be formed based upon this (simplified) method will
in general be referred to as an "induced subtree". Hence, the set of induced
subtrees that can be formed based upon a given tree will be referred to as the
tree's "class of induced subtrees". (Note that an induced subtree is still a
generic subtree, and that a tree's class of induced subtrees is a sub-class
of the tree's class of generic subtrees).
