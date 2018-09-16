
<!-- ======================================================================= -->
# Subtrees

A (simple) **subtree** `S := (T,U)` is a subgraph of a graph `G := (V,E)` such
that `S` is a tree.

Note that the super-graph `G` is not required to be a tree. Hence, the focus of
this definition is on the characteristic of the subtree itself. In addition to
that, `S` may or may not satisfy further restrictions.

Note that a subtree is commonly defined as: "A connected subgraph of a tree".
That is, this definition requires `G` to be a tree. Consequently, and because
`S` is a connected subgraph of `G`, `S` is itself a tree. Because of that,
the common definition is more specific and the above definition more general.

A **strict/proper subtree** is formed by removing at least one node and/or
edge - i.e. `(#T < #V)` and/or `(#U < #E)`. That is, any tree `G` is a (simple)
subtree, but no proper subtree to itself.

An **induced subtree** `S := (T,U)` is an induced subgraph formed from another
graph `G := (V,E)` such that `S` is a tree.

A **strict/proper induced subtree** `S` is an induced subtree formed from
another graph `G` by removing at least one vertex - i.e. `(#T < #V)`.

Note that not even the super-graph of a proper induced subtree is itself
necessarily a tree (e.g. a subtree in a forest of trees). 

Note that a proper induced subtree, formed from another tree, will always have
fewer edges than its super-tree - i.e. `(#U < #E)`. That is because any tree
is connected.

<!-- ======================================================================= -->
## remarks

There are obviously several ways to form a subtree `S` from a given tree `T`.
However, and independently of how exactly a subtree is formed, a subtree will
always have a root `r`. (Note that the `r` of `S` may or may not be identical
to the root of the super-tree `T` - i.e. `(RN(S) == RN(T)` may be true).

Like any other tree, each node in `S` has a unique rooted path in `T`. In
addition to that, a subtree is not required to contain all the descendants `d`
of `r` in `T`. Consequently, `S` may have leaf nodes that are no leafs in `T`.

That is, a subtree is in general defined by its root and its leaf nodes.

Note that, in the context of this discussion, the super-graph of a sub-tree
is in general assumed to be an arborescence and any sub-tree is assumed to
be a non-empty induced subtree of such a super-tree.

once the first node of a subtree is selected, all other nodes must
be reachable from that node.

<!-- ======================================================================= -->
## TODO

* define `R(T)` as the root of a tree
* an induced subtree is induced by the subtree's root
* only one edge that leads into the subtree
* no edge that leads out of the subtree

--

however, since an induced subtree is based on a connected component, the
super-graph must contain the subtree as is. that is, an induced subtree
is formed by cutting away the exterior - i.e. what is outside of it.
