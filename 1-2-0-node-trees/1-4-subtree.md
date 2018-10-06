
<!-- ======================================================================= -->
# Subtrees

A (simple) **subtree** `S := (T,U)` is a subgraph of a graph `G := (V,E)` such
that `S` is a tree. Obviously, the vertices of `G` will become the nodes of `S`.

Note that the super-graph `G` is not required to be a tree. Hence, the focus of
this definition is on the characteristic of the subtree itself. However, `S` may
still satisfy further restrictions.

Note that a subtree is commonly defined as: "A connected subgraph of a tree".
That is, this definition requires `G` to be a tree. Consequently, and because
`S` is a connected subgraph of `G`, `S` is itself a tree. Because of that, the
common definition is more specific and the above definition more general.

A **strict/proper subtree** is formed by removing at least one vertex and/or
edge (i.e. `(#T < #V)` and/or `(#U < #E)`). That is, any tree `G` is a (simple)
subtree, but no proper subtree to itself.

An **induced subtree** `S := (T,U)` is an induced subgraph formed from a graph
`G := (V,E)` such that `S` is a tree. As such, an induced subtree may be induced
by a subset of vertices (i.e. `G[T]`), or by a subset of edges (i.e. `G[U]`).

An **induced strict/proper subtree** `S` is an induced subtree formed from a
graph `G` by removing at least one vertex and/or edge. Such a subtree may also
be referred to as a "strict/proper induced subtree".

Note that the requirement of having fewer vertices and/or edges is with regards
to the resulting subtree. That is, the subset of vertices or edges used to form
the subtree is itself not required to have fewer elements than the corresponding
set of the super-graph.

Example: `G` may be a forest that holds two trees. One that consists of a single
node, and another that is a tree of two or more node. In such a case, `G[E(G)]`
is an induced proper subtree, even though all the edges in `G` are used to form
the subtree.

Note that not even the super-graph of an induced proper subtree is required to
be a tree (e.g. a subtree in a forest of trees).

Note that an induced proper subtree (i.e. `G[T]`), formed from another tree,
will always have fewer edges than its super-tree - i.e. `(#U < #E)`. That is
because all trees are connected.

<!-- ======================================================================= -->
## generic method to form a subtree

Note that, in the context of this discussion, the super-graph of a sub-tree is
expected to be an arborescence and any sub-tree is assumed to be a non-empty
induced subtree of such a super-tree.

Obviously, there are multiple ways to form a subtree `S` from a given tree
`T`. However, and independently of how exactly a subtree is formed, a subtree
must itself always have a single root `r`. (Note that the root `r` of subtree
`S` may or may not be identical to the root of its super-tree `T` - i.e.
`(RN(S) == RN(T)` is not necessarily true).

Like any other tree, each node in `S` has a unique rooted path in `T`. However,
a subtree is in general not required to include all the descendants `d` of `r`
in `T`. Consequently, `S` may have leaf nodes that are no leafs in `T`. Because
of that, the subtree of a tree can in general be defined by its root `r` and
by its set of leaf nodes `LS`:

* `subtreeOf(T,r,LS)` := the union of all paths in `P`, where
* `P(T,r,LS) := { p | p := (r,...,l) for a leaf (l in LS) }`

That is, because the rooted paths in `P` are treated as path graphs, the
requested subtree is the union of all these subgraphs that begin in `r` and
end in a leaf in `LS`.

<!-- ======================================================================= -->
## remarks on - the generic method

From a graph theoretical point of view, the above generic method to define
a subtree `S` based upon a given tree `T` is perfectly fine. That is because
the result will always be a subtree according to the above definition.

The question however is, because each arborescence defines a partial order,
whether or not the descendants `d` in `T` of a leaf `(l in LS)` can be ignored
that easily. Put differently, what effect does it have, if such descendants
are omitted?

<!-- ======================================================================= -->
## TODO

define - induced subtree - i.e. induced by its root

once the first node of a subtree is selected, all other nodes must
be reachable from that node.

* define `R(T)` as the root of a tree
* an induced subtree is induced by the subtree's root
* only one edge that leads into the subtree
* no edge that leads out of the subtree

however, since an induced subtree is based on a connected component, the
super-graph must contain the subtree as is. that is, an induced subtree
is formed by cutting away outer nodes - i.e. remove what is outside of it.
