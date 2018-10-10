
<!-- ======================================================================= -->
# the border graphs of subtrees

* (/see/ "border graphs" in "graph theory")

In the discussion below, `S` is formed as a subtree of `G`. Hence, `S` must be
a subtree of a component in `G`. That is because `S` could otherwise not be a
tree as trees are by definition connected. Consequently, `G` can be thought of
as being reduced to the relevant component, which is why `G` can be treated as
a connected graph. That is, the components in `G`, which are not essential to
the following discussion, can and will be ignored.

<!-- ======================================================================= -->
## subtree S of super-tree T

The following assumes the super-graph `G := (V,E)` of subtree `S := (M,F)`
to be a tree `T := (N,E)` (i.e. `G := T`).

Note that `(S == T[V(S)])` is true. That is, `S` is equal to the subgraph,
induced in `T` by the set of vertices in `S`.

**generic subtrees**

The generic method used to define subtrees (i.e. `subtreeOf(T,r,LS)`) will be
covered by the following two cases, in which the definition of the respective
induced subtrees is based upon subsets of elements rather than on the outer
set of a given node.

The two aspects that need to be taken into account are, (1) whether or not the
root `r` of subtree `S` is identical to the root of the super-tree `T` (i.e.
`(RN(S) == RN(T))`), and (2) whether or not the subtree contains all the leaf
nodes that can be reached in `T` beginning with the subtree's root `r`.

**induced subtrees T(M)**

If `S` is induced by the entire set of nodes in `T` (i.e. `(M == N)`), then
both border graphs are empty (i.e. `(IBG == Ø)` and `(OBG == Ø)`). That is
because `S` then contains all the edges in `T`.

If, in contrary to that, `S` is induced by a proper subset of nodes (i.e.
`(#M < #N)`), then the inner border graph is still empty (i.e. `(IBG == Ø)`).
That is because `T` is itself a tree.

However, the outer border graph is never going to be empty (i.e. `(OBG != Ø)`,
i.e. `(OBGi != Ø)` and/or `(OBGo != Ø)`), if `S` is a proper subtree of `T`.

**induced subtrees T(F)**

If `S` is induced by the entire set of edges in `T` (i.e. `(F == E)`), then
both border graphs are empty (i.e. `(IBG == Ø)` and `(OBG == Ø)`). That is,
because `S` then contains all the vertices in `T`.

If, in contrary to that, `S` is induced by a proper subset of edges (i.e.
`(#F < #E)`), then the inner border graph is still empty (i.e. `(IBG == Ø)`).
That is because `T` is itself a tree.

However, the outer border graph is never going to be empty (i.e. `(OBG != Ø)`,
i.e. `(OBGi != Ø)` and/or `(OBGo != Ø)`), if `S` is a proper subtree of `T`.

**summary**

The inner border graph `IBG` in between `T` and `S` is always empty.

* `(IBG(T,S) == Ø)`

In contrary to that, the outer border graph `OBG` in between `T` and `S` is not
necessarily empty. That is because `OBGi` is not empty, if the root of `S` is
not identical to the root of `T`. Likewise, `OBGo` is not empty, if not all of
the leaf nodes of `r` in `T` are also leaf nodes in `S`. Put differently, `T`
may have a single edge that ends in `S` and one or more edges that begin in `S`
and end in `T`.

* `(OBG(T,S) <=!=> Ø)`, where `OBG := OBGi + OBGo`
* i.e. `OBGi` and `OBGo` both not necessarily empty

Note that the outer border `OBGi` in between `T` and `S` is not empty, if `S`
is induced by the outer set of a child in `T`. That is because the `r` is then
unequal to the root of `T`. In addition to that, `OBGi` then contains a single
edge only.

* `p` is the parent of `r` in `T` - i.e. `(r in CN(T))`
* `(OBGi(T,S) == {e})`, if `S := T[OS(r)]` and `(e == (p,r))`

Note that the outer border `OBGo` in between a `S` and `T` is empty, if `S` is
induced by the outer set of its root.

* `(OBGo(T,S) == Ø)`, if `S := T[OS(r)]`

That is, any proper subtree `S := T[OS(r)]`, induced by the outer set of its
root `r`, is connected to its super-tree `T` by a single edge `e`. That edge
connects `r` with its parent in `T` and is incoming in regards to `r`. Because
of that, `e` reflects the relationship between both trees.

<!-- ======================================================================= -->
## subtree S of super-graph G

The following assumes the super-graph `G := (V,E)` of subtree `S := (M,F)`
to be a connected, non-tree graph.

Recall that the overall focus is on subtrees of trees. The considerations
below are therefore non-substantial to the overall discussion and need to
be understood as an attempt to provide a wider perspective.

Note that the semantics of a subgraph is by definition equivalent to the
semantics of its super-graph. Because of that, the question arises how the
semantics of `S` could result in `S` being a tree, but the very same semantics
allowing `G` to not be a tree? The following content therefore needs to be
understood to ignore this semantical aspect. That is, the following needs to be
understood from a purely theoretical (i.e. structural/syntactical) perspective.

**main considerations**

Recall that the focus is on the component in `G` to which `S` is a subtree.
Because of that, the edges in another component in `G` can not be edges in
`S` or in the border graphs between the two.

Another consequence is that `G` needs to satisfy one or more of the following
conditions. That is because `G` would otherwise be a tree.

1. `G` has no vertex with no incoming edge (i.e. no root)
2. `G` has several vertices with no incoming edge (i.e. more than one root)
3. `G` has vertices with more than one incoming edge

Note that (3) does not necessarily result in (directed) cycles (e.g. the root
may have an alternative route to one of its descendants). However, `UG(G)`
(i.e. the underlying undirected graph of `G`) will have (undirected) cycles,
if there is even one such vertex in `G`.

Note that, due to these conditions, `S` can not be equal to `G`. That is, `S`
and `G` are distinct graphs, which is why `S` must be a proper subtree of `G`.

**overview of case-1 and case-2**

In regards to a non-tree graph `G`, two main cases can be distinguished:
(1) `S` is equal to the subgraph `I`, induced in `T` by the set of vertices in
`S` (i.e. `(S == I)` where `I := G[V(S)]`), and (2) `S` is distinct from `I`.

In case-1, the inner border graph between `S` and `G` is empty (i.e.
`(IBG(G,S) == Ø)`). That is, because `S` will contain all the edges in `I`.
The focus of case-1 is therefore on the edges in `B`, which (in its core)
contains the elements of `G` not in `S` (i.e. `B := ((G \ S) + OBG(G,S))`).

Note that `(G \ S)` contains all those vertices that are not adjacent to any
node in `S`. In contrary to that, `OBG(G,S)` contains only those edges in
`G` that are incident to a node in `S`. And because `G` is connected, the
outer border graph between the two is non-empty (i.e. `(OBG(G,S) != Ø)`).

In case-2, the inner border graph is non-empty (i.e. `(IBG(G,S) != Ø)`). In
contrary to that, the outer border graph between the two is not necessarily
empty (i.e. `(OBG(G,S) <=!=> Ø)`). The focus of case-2 is therefore on the
edges in `I` that are no edges in `S`.

**in regards to "generic subtrees"**

The generic method used to define subtrees (i.e. `subtreeOf(T,r,LS)`) requires
`T` to be a tree. That is because, in a connected non-tree graph, several
distinct paths may in general be formed which allow to reach a leaf in `LS`
beginning with the subtree's root `r`. Because of that, any only based upon
the root and a leaf, there is no means to decide which path to take for a
given leaf in `LS`. Consequently, this generic method does not allow to
uniquely define a subtree in a non-tree graph.

**TODO** - continue here ...

<!-- ======================================================================= -->
## subtree S of super-graph G: case-1

Graph `G := (V,E)` is the connected non-tree super-graph of the
proper subtree `S := (M,F)` such that `(S == G[V(S)])` is true.

Note that `(IBG(G,S) == Ø)` and `(OBG(G,S) != Ø)`. The focus of case-1 is
therefore on the edges in `OBG(G,S)` (i.e. those in `G`, but not in `S`,
that are incident to a node in `S`). In regards to the (possible) edges in
`IBG`, see case-2.

Note that, because `S` must be a proper subtree of `G`, `S` can not be
induced by all the elements of the corresponding set in `G`. That is,
`S` must be distinct from `G[V]` and `G[E]`.

**induced subtrees G(M)**

* The reason as to why `G` is not a tree is due to its edges in `OBG`.
* `(S == G[M])` is possible

**induced subtrees G(F)**

* `(S == G[F])` is true

<!-- ======================================================================= -->
## subtree S of super-graph G: case-2

Graph `G := (V,E)` is the connected non-tree super-graph of the
proper subtree `S := (M,F)` such that `(S != G[V(S)])` is true.

Note that `(IBG(G,S) != Ø)`, but `(OBG(G,S) <=!=> Ø)`. The focus of case-2 is
therefore on the edges in `I := G[V(S)]` that are no edge in `S`. In regards
to the (possible) edges in `OBG`, see case-1.

**induced subtrees G(M)**

In this particular case, `S` can not be a subtree that is induced by its set
of nodes (i.e. `(S != G[M])`). That is because `S` would then also contain
all the edges in `IBG`, which would turn `S` into a non-tree graph. That is
`G[M]` is in conflict with case-2.

Consequently, `S` can not be induced by its set of nodes.
That is, `S` must be induced by its set of edges (i.e. `(S == G[F])`).

**induced subtrees G(F)**

As mentioned before, the edges in `IBG` do not allow to clarify the relationship
between `G` and `S` because each edge can be understood to point from one graph
to the other. Because of that, such edges, if possible, need to be avoided.

In addition to `(IBG != Ø)`, the outer border graph may be non-empty. That is,
`(OBG != Ø)` may be true. Therefore, case-1 applies in regards to the edges in
the outer border graph.
