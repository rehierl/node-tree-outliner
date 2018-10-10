
<!-- ======================================================================= -->
# the border graphs of subtrees

* (/see/ "border graphs" in "graph theory")

In the discussion below, `S` is required to be a subtree of a component in `G`,
which is because `S` must be a tree. Because of that, `G` can be thought of as
being reduced to such a component. That is, the components in `G`, which are
not essential to the discussions below, can be ignored.

<!-- ======================================================================= -->
## subtree S of super-tree T

The following assumes the super-graph `G := (V,E)` of subtree `S := (M,F)`
to be a tree `T := (N,E)` (i.e. `G := T`).

Note that `(S == T[V(S)])` is true. That is, `S` is equal to the subgraph
that is induced in `T` by the set of vertices in `S`.

### generic subtrees

The generic method used to define subtrees (i.e. `subtreeOf(T,r,LS)`) will be
covered by the following two cases, in which the definition of the respective
induced subtrees is based upon subsets of elements rather than on the outer
set of a given node.

The two aspects that need to be taken into account are, (1) whether or not the
root `r` of subtree `S` is identical to the root of the super-tree `T` (i.e.
`(RN(S) == RN(T))`), and (2) whether or not the subtree contains all the leaf
nodes that can be reached in `T` beginning with the root `r` of `S`.

### induced subtrees T(M)

If `S` is induced by the entire set of nodes in `T` (i.e. `(M == N)`), then
both border graphs are empty (i.e. `(IBG == Ø)` and `(OBG == Ø)`). That is
because `S` then contains all the edges in `T`.

If, in contrary to that, `S` is induced by a proper subset of nodes (i.e.
`(#M < #N)`), then the inner border graph is still empty (i.e. `(IBG == Ø)`).
That is because `T` is itself a tree.

However, the outer border graph is never going to be empty (i.e. `(OBG != Ø)`,
i.e. `(OBGi != Ø)` and/or `(OBGo != Ø)`), if `S` is a proper subtree of `T`.

### induced subtrees T(F)

If `S` is induced by the entire set of edges in `T` (i.e. `(F == E)`), then
both border graphs are empty (i.e. `(IBG == Ø)` and `(OBG == Ø)`). That is,
because `S` then contains all the vertices in `T`.

If, in contrary to that, `S` is induced by a proper subset of edges (i.e.
`(#F < #E)`), then the inner border graph is still empty (i.e. `(IBG == Ø)`).
That is because `T` is itself a tree.

However, the outer border graph is never going to be empty (i.e. `(OBG != Ø)`,
i.e. `(OBGi != Ø)` and/or `(OBGo != Ø)`), if `S` is a proper subtree of `T`.

### summary

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

**CLARIFICATION**
Any proper subtree `S := T[OS(r)]`, induced by the outer set of its root `r`,
is connected to its super-tree `T` by a single edge only, which connects `r`
with its parent in `T`. That edge is incoming in regards to `r` and therefore
reflects the relationship between both trees.

<!-- ======================================================================= -->
## subtree S of super-graph G

The following assumes the super-graph `G := (V,E)` of subtree `S := (M,F)`
to be a non-tree graph.

Note that it is rather conflicting to form a tree from a non-tree graph. That
is because the semantics of a subgraph is by definition equivalent to the
semantics of its super-graph. Because of that, the question arises how the
semantics of `S` could even result in `S` being a tree, but the very same
semantics allowing `G` to not be a tree? The following content therefore needs
to be understood to simply ignore this semantical aspect. Put differently, the
following needs to be understood from a purely theoretical (i.e. structural/
syntactical) perspective.

Note that `(S == T[V(S)])` can not be true. That is because if `S` would be
equal to the subgraph, induced in `T` by the set of vertices in `S`, then `S`
could not be a subtree. That is because `T` is assumed to be reduced to the
relevant component, which is assumed to not be a tree. (In short: If that
component would itself be a tree, then the above section would apply instead).

Note that, because `G` is assumed to not be a tree, `G` needs to have one or
more vertices that have no incoming edge, or one or more vertices that have
more than one such edge. Put differently, `G` is assumed to be a connected
graph that has one or more "root" vertices and/or undirected cycles in `UG(G)`.
(Recall that loops count as 1-cycles).

### generic subtrees

Note that the generic method used to define subtrees (i.e. `subtreeOf(T,r,LS)`)
requires `T` to be a tree. That is because a connected graph that is not a tree
may have several paths which allow to reach a leaf in `LS` starting with the
root node `r`. Because of that, there is no means to decide which path to take
for a given leaf node in `LS`. Because of that, this generic method is not
suited to provide a unique definition for a subtree based upon a non-tree graph.

### induced subtrees G(M)

If `S` is induced by a set of vertices, then `M` must be a proper subset of
`V` (i.e. `(M proper-subset-of V)`). That is because otherwise, `S` would
be equal to `G` and therefore not a tree.

**Continue here ...**

However, and because `G[M]` contains all the edges in the induced subgraph,
the inner border graph `IBG(G,S)` can only be empty (i.e. `(IBG(G,S) == Ø)`).
Otherwise, `S` could not be a tree.

Consequently, the reason as to why `G` is itself not a tree, lies within `G[M]`
as a subset of disconnected vertices, or as 

In this particular case, `S` can not be a subtree that is induced by its set
of nodes (i.e. `(S != G[M])`). That is because `S` would then have all the
edges in `G`, which would require that `G` itself would have to be a tree.
That is obviously in conflict with the current case.

### induced subtrees G(F)

As before, the set of edges `F` used to induce `S` must be a proper subset of
`E` (i.e. `(F proper-subset-of E)`). That is because otherwise, `S` would be
equal to `G` and therefore not a tree.

**Continue here ...**

Because of that, `S` can only be a subtree that is induced by its set of edges
(i.e. `(S == G[F])`). That is, induced by a proper subset of edges and thus
the result of removing one or more edges in `G`.

Note that the inner border graph `IBG(G,S)` between a non-tree super-graph and
its subtree is always non-empty (i.e. `(IBG(G,S) != Ø)`). If that would not be
the case, then `S` would be equal to `G` and as such not a subtree.

### summary
