
<!-- ======================================================================= -->
# the border graphs of subtrees

* (/see/ "border graphs" in "graph theory")

( **TODO** - It is quite difficult to clearly express what I have in mind.
Try to grasp the intentions behind the following explanations ... )

In the discussions below, `G` is expected to be a connected graph because `S`
must be a tree. That is, `S` is in general a subtree of a connected component
in `G`, which is why `G` can be thought of as being reduced to such a component.

<!-- ======================================================================= -->
## subtree S of super-graph G

The following assumes the super-graph `G := (V,E)` of subtree `S := (M,F)`
to be a non-tree graph.

Note that, because `G` is assumed to not be a tree, `G` needs to have at least
one or more vertices that have more than one incoming edges and/or at least
one or more vertices that have no such edge at all. Put differently, `G` is
assumed to be a connected graph that has one or more "root" vertices and/or
cycles. (Recall that loops count as 1-cycles).

### generic subtrees

Note that the generic method used to define subtrees (i.e. `subtreeOf(T,r,LS)`)
requires `T` to be a tree. That is because a connected graph that is not a tree
may have several paths that allow to reach a leaf in `LS` beginning with the
root node `r`. Because of that, there is no means to decide which path to take
for a given leaf node in `LS`. Because of that, this generic method is not
suited to provide a unique definition of a subtree based upon a non-tree graph.

### induced subtrees G(M)

If `S` is induced by a set of vertices, then `M` must be a proper subset of
`V` (i.e. `(M proper-subset-of V)`). That is because otherwise, `S` would
be equal to `G` and therefore not a tree.

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

Similar as before, the set of edges `F` used to induce `S` must be a proper
subset of `E` (i.e. `(F proper-subset-of E)`). That is because otherwise,
`S` would be equal to `G` and therefore not a tree.

Because of that, `S` can only be a subtree that is induced by its set of edges
(i.e. `(S == G[F])`). That is, induced by a proper subset of edges and thus
the result of removing one or more edges in `G`.

Note that the inner border graph `IBG(G,S)` between a non-tree super-graph and
its subtree is always non-empty (i.e. `(IBG(G,S) != Ø)`). If that would not be
the case, then `S` would be equal to `G` and as such not a subtree.

### summary

<!-- ======================================================================= -->
## subtree S of super-tree T

The following assumes the super-graph `G := (V,E)` of subtree `S := (M,F)`
to be a tree `T := (N,E)` (i.e. `G := T`).

### generic subtrees

The generic method used to define subtrees (i.e. `subtreeOf(T,r,LS)`) will be
covered by the following two cases, in which the definition of the respective
induced subtrees is based upon subsets of elements rather than the outer set
of a node.

The two aspects that need to be taken into account are, whether or not the
root `r` of subtree `S` is identical to the root of the super-tree `T` (i.e.
`(RN(S) == RN(T))`), and whether or not the subtree contains all the leaf
nodes that can be reached in `T` beginning with the root `r` of `S`.

### induced subtrees T(M)

If `S` is induced by the entire set of nodes in `T` (i.e. `(M == N)`),
then both border graphs are empty (i.e. `(IBG == Ø)` and `(OBG == Ø)`).

If, in contrary to that, `S` is induced by a proper subset of nodes (i.e.
`(#M < #N)`), then the inner border graph is empty (i.e. `(IBG == Ø)`).
That is because `T` is itself a tree.

However, the outer border graph is never going to be empty
(i.e. `(OBG != Ø)`, i.e. `(OBGi != Ø)` and/or `(OBGo != Ø)`),
if `S` is a proper subtree of `T`.

### induced subtrees T(F)

If `S` is induced by the entire set of edges in `T` (i.e. `(F == E)`),
then both border graphs are empty (i.e. `(IBG == Ø)` and `(OBG == Ø)`).

If, in contrary to that, `S` is induced by a proper subset of edges (i.e.
`(#F < #E)`), then the inner border graph is empty (i.e. `(IBG == Ø)`).
That is because `T` is itself a tree.

However, the outer border graph is never going to be empty
(i.e. `(OBG != Ø)`, i.e. `(OBGi != Ø)` and/or `(OBGo != Ø)`),
if `S` is a proper subtree of `T`.

### summary

The inner border graph `IBG` between the subtree of a tree is always empty.

* `(IBG(T,S) == Ø)`

In contrary to that, the outer border graph `OBG` between the subtree of a
tree is not necessarily empty. That is because `OBGi` is not empty if the
subtree's root is not identical to the root of the super-tree. Likewise,
`OBGo` is not empty if not all of the leaf nodes of `r` in `T` are also
leaf nodes in `S`. Put differently, `T` may in general have a single edge
that ends in `S` and one or more edges that begin in `S` and end in `T`.

* `OBG := OBGi + OBGo`
* `(OBG(T,S) <=!=> Ø)` - due to `(OBGi <=!=> Ø)` and `(OBGo <=!=> Ø)`
* `(#OBGi(T,S) == 1)`, if `(RN(S) != RN(T))`

Note that the outer border graph `OBGo` between the subtree of a tree,
induced by the outer set of a node, is always empty.

* `(OBGo(T,S) == Ø)`, if `S := T[OS(n)]`

**CLARIFICATION**
Any proper subtree `S := T[OS(r)]`, induced by the outer set of its root `r`
in `T`, is connected to its super-tree by a single edge which connects the
subtree's root with its parent node in `T`. That edge is incoming in regards
to `r` and therefore reflects the relationship between both trees `S` and `T`.
