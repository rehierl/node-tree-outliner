
<!-- ======================================================================= -->
# the border graphs of (induced) subtrees

* (/see/ "border graphs" in "graph theory")

In the discussion below, `S` is formed as a subtree of `G`. Because of that, `S`
must be the subtree of a component in `G` as `S` could otherwise not be a tree
because trees are by definition connected. Consequently, `G` can be thought of
as being reduced to the relevant maximal component in `G`, which is why `G` can
be treated as a connected graph. That is, the components in `G` that are not
connected with `S` will be ignored as they are non-essential to the following
discussion.

<!-- ======================================================================= -->
## subtree S of super-tree T

The following assumes the super-graph `G := (V,E)` of subtree `S := (M,F)` to
be a tree `T := (N,E)` (i.e. `G := T`). Because of that, `(S == T[M])` is true.
That is, `S` is equal to the subgraph, induced by the set nodes in `S`.

**generic subtrees**

The generic method used to define subtrees (i.e. `subtreeOf(T,r,LS)`) will
be covered by the following two cases in which the definition of the induced
subtrees is based upon subsets of elements rather than on the outer set of a
node.

The two aspects that need to be taken into account are, (1) whether or not the
root `r` of subtree `S` is identical to the root of the super-tree `T` (i.e.
`(RN(S) == RN(T))`), and (2) whether or not the subtree contains all the leaf
nodes that can be reached in `T` beginning with the subtree's root.

**induced by a subset of nodes - i.e. T(M)**

If `S` is induced by the entire set of nodes in `T` (i.e. `(M == N)`), then
both border graphs are empty (i.e. `(IBG == Ø)` and `(OBG == Ø)`). That is
because `S` is then identical to `T` (i.e. `(S == T)`).

If, in contrary to that, `S` is induced by a proper subset of nodes (i.e.
`(M proper-subset-of N)`), then the inner border graph is still empty (i.e.
`(IBG == Ø)`). That is because `T` is a tree and because `S` then contains
all the edges whose endpoints are both in `S`.

However, the outer border graph is never going to be empty (i.e. `(OBG != Ø)`,
i.e. `(OBGi != Ø)` and/or `(OBGo != Ø)`), if `S` is a proper subtree of `T`.
To be more accurate, `OBGi` is non-empty, if the root of `S` is unequal to
the root of `T`. Likewise, `OBGo` is non-empty, if not all of the leaf nodes
of `r` in `T` are also leaf nodes in `S`.

**induced by a subset of edges - i.e. T(F)**

If `S` is induced by the entire set of edges in `T` (i.e. `(F == E)`), then
both border graphs are empty (i.e. `(IBG == Ø)` and `(OBG == Ø)`). That is,
because `S` then is identical to `T` (i.e. `(S == T)`).

If, in contrary to that, `S` is induced by a proper subset of edges (i.e.
`(F proper-subset-of E)`), then the inner border graph is still empty (i.e.
`(IBG == Ø)`). That is because `T` is and `S` must be a tree. Put differently,
every edge in `T` in between the nodes of `S` must be included.

However, the outer border graph is never going to be empty (i.e. `(OBG != Ø)`,
i.e. `(OBGi != Ø)` and/or `(OBGo != Ø)`), if `S` is a proper subtree of `T`.
As before, `OBGi` is non-empty, if the root of `S` is unequal to the root of
`T`. Likewise, `OBGo` is non-empty, if not all of the leaf nodes of `r` in `T`
are also leaf nodes in `S`.

<!-- ======================================================================= -->
## subtree S of super-tree T, summary

The inner border graph `IBG` in between `T` and `S` is (always) empty.

* `(IBG(T,S) == Ø)`

In contrary to that, the outer border graph `OBG` in between `T` and `S` is not
necessarily empty. That is because `OBGi` is not empty, if the root of `S` is
not identical to the root of `T`. Likewise, `OBGo` is not empty, if not all of
the leaf nodes of `r` in `T` are also leaf nodes in `S`. Put differently, `T`
may in general have a single edge that ends in `S` and one or more edges that
begin in `S` and end in `T`.

* `(OBG(T,S) <=!=> Ø)`, where `OBG := (OBGi + OBGo)`
* i.e. `OBGi` and `OBGo` are both not necessarily empty
* `(OBG(T,S) == Ø)` if, and only if `(T == S)`

Note that the outer border `OBGi` in between `T` and `S` is non-empty, if `S`
is induced by the outer set of a descendant of the root `t` of `T`. That is
because the root `r` of `S` is then unequal to `t`. Furthermore, `OBGi` then
has one edge only.

* `r` is the root of `S` and `S := T[OS(r)]`
* `p` is the parent of `r` in `T` - i.e. `(r != t)`
* `(OBGi(T,S) == {e})` where `(e == (p,r))`

Note that the outer border `OBGo` in between `S` and `T` is empty, if `S` is
induced by the outer set of its root `r` in `T`. That is because `S` then has
all the leaf nodes of `r` in `T`.

* `(OBGo(T,S) == Ø)`, if `S := T[OS(r)]`

**SUMMARY**
Any proper subtree `S := T[OS(r)]`, induced by the outer set of nodes of its
root `r`, is connected to its super-tree `T` by a single edge `(e in OBGi)`.
That edge connects the subtree's root `r` with its parent node in `T` and is
incoming in regards to `r` (i.e. root `r` is the sink of `e`). Because of
that, `e` reflects the relationship between both trees.

Note that, due to the above, the single edge `e` in `OBGi` will simply be
referred to as the **border edge** (in short: `BE(T,S) := e`). This border
edge does however not exist if, and only if `(S == T)`.

**CLARIFICATION**
Due to the above, no other class of subtrees can be defined such that the
relationship between a super-tree and one of its subtrees can be uniquely
determined. That is, because in any other case, the additional edges in the
border graphs break the above unique relationship. The focus of the overall
discussion is therefore on subtrees that are induced by their root node.

<!-- ======================================================================= -->
## subtree S of super-tree T, example

Given the following two trees, ...

```
super-tree T      sub-tree S
=============     ==========
1 -> 2 -|-> 3     2 -|-> 3
        |-> 4        |-> 4
```

* T: `V(T) := {1,2,3,4}` and `E(G) := {(1,2),(2,3),(2,4)}`
* S: `V(S) := {2,3,4}` and `E(S) := {(2,3),(2,4)}`
* i.e. `(S == T[2])`

... the border graphs between the two are as follows:

```
 |= T ===================|
 |        |= S ========| |
 | |= OBG ====|        | |
 | | 1 -> | 2 | -|-> 3 | |
 | |==========|  |-> 4 | |
 |        |============| |
 |=======================|
```

* `(IBG == Ø)`, `(OBGo == Ø)` and `(OBGi == ({1,2}, {(1,2)}) )`
* i.e. `(BE(T,S) == (1,2))`

Note that `(T supertree-of S)` because `(e in OBGi)` is oriented from a node
in `T` towards the root of `S`. That is, because `e` still has the parent-of
semantics (i.e. `(1 parent-of 2)`) and is therefore oriented from a super-
ordinate node towards a sub-ordinate node. The relationship between `T` and
`S` therefore corresponds with the relationship between both nodes. That is,
`T` is super-ordinate to `S`.

<!-- ======================================================================= -->
## subtree S of super-graph G

The following assumes the super-graph `G := (V,E)` of subtree `S := (M,F)`
to be a connected, non-tree graph.

Recall that the overall focus is on subtrees of trees. The considerations below
are therefore non-substantial to the overall discussion, do not claim to be
complete and therefore need to be understood as an attempt to provide an even
wider perspective.

Note that the semantics of a subgraph is by definition equivalent to the
semantics of its super-graph. Because of that, the question arises how the
semantics of `S` could result in `S` being a tree, but the very same semantics
allowing `G` to be a non-tree graph? As the content below will not attempt
to answer that question, the following needs to be understood from a purely
theoretical (i.e. structural/syntactical) perspective.

**main considerations**

Recall that the focus is on the component in `G` to which `S` is a subtree.
That is because the edges of any other component in `G` can not be edges in
`S` or in the border graphs between the two. Hence, these edges are outside
of the scope of the following discussion and will therefore be ignored.

Another consequence of the that case (i.e. `G` is a non-tree graph) is that
`G` needs to satisfy one or more of the following conditions. That is because
`G` would otherwise be a tree.

1. All vertices in `G` have at least one incoming edge (i.e. no root)
2. `G` has several vertices with no incoming edge (i.e. more than one root)
3. `G` has vertices with more than one incoming edge (i.e. more than one parent)

Note that (3) does not necessarily result in (directed) cycles. That is because
a root vertex may have an alternative downward oriented path to one of its
descendants. However, `UG(G)` (i.e. the underlying undirected graph of `G`)
will have (undirected) cycles, if even one such vertex exists in `G`.

Note that, due to the above conditions, `S` can not be equal to `G` since `G`
is required to be a non-tree graph. That is, `S` and `G` are distinct graphs,
which is why `S` has to be a proper subtree of `G`.

**overview of case-1 and case-2**

In regards to a non-tree graph `G`, two cases may be distinguished:
(1) `S` is equal to the subgraph `I`, induced in `G` by the set
of vertices in `S` (i.e. `(S == I)` where `I := G[V(S)]`), and
(2) `S` is a proper subtree of `I`.

In case-1, the inner border graph between `S` and `G` is empty (i.e.
`(IBG == Ø)`). That is because `S` will, due to being induced by its set
of vertices `V(S)`, contain all the edges in `I`. The focus of case-1 is
therefore on the set of edges in `B`, which contains those edges in `G`
that are not in `S` (i.e. `B := ((G \ S) + OBG)`).

Note that `(G \ S)` contains all those edges that are not incident to a node
in `S`. In contrary to that, `OBG` contains those edges that are incident to
a node in `S`. And because `G` is connected and `S` a proper subtree of `G`,
the outer border graph between the two is non-empty (i.e. `(OBG != Ø)`).

In case-2, the inner border graph is non-empty (i.e. `(IBG != Ø)`). In contrary
to that, the outer border graph between the two is not necessarily empty (i.e.
`(OBG <=!=> Ø)`). The focus of case-2 is therefore on the edges in `I` that
are no edges in `S`.

**in regards to "generic subtrees"**

The generic method used to define subtrees (i.e. `subtreeOf(T,r,LS)`) requires
`T` to be a tree. That is because, in a connected non-tree graph, several paths
may in general be formed that allow to reach a leaf in `LS` beginning with the
subtree's root `r`. Because of that, there is no means to decide which path to
take in order to reach a given leaf in `LS`. Consequently, this generic method
does not allow to uniquely define a subtree in a non-tree graph.

<!-- ======================================================================= -->
## subtree S of super-graph G: case-1, (OBG != Ø)

Graph `G := (V,E)` is the connected non-tree super-graph of the proper subtree
`S := (M,F)` such that `(S == G[V(S)])` is true. Hence, the reason for `G` not
being a tree is due to the edges in `B := ((G \ S) + OBG)`.

Note that `(IBG == Ø)` and `(OBG != Ø)`. The focus of this case is therefore
on the edges in `OBG` (i.e. those in `G` but not in `S` and incident to a node
in `S`).

Note that, because `S` must be a proper subtree of `G`, `S` can not be induced
by all the elements of the corresponding set in `G`. That is, `S` is distinct
from `G[V]` and `G[E]`.

Note that `(S == G[M])` and `(S == G[F])` are due to`(IBG == Ø)` both true.
Hence, `S` may be induced by its set of nodes, or its set of edges. Because of
that, a distinction between those two is in that particular case not required.

**edges in OBG**

Every node in `S`, including its leaf nodes, may be adjacent to a vertex in
`(G \ S)` such that the corresponding edge `e` is incoming in regards to the
node in `S` (i.e. the node in `S` is the sink of `e`).

Likewise, every node in `S`, including its root node, may be adjacent to
a vertex in `(G \ S)` such that the corresponding edge `e` is outgoing in
regards to the node in `S` (i.e. the node in `S` is the source of `e`).

Consequently, `S` may be a source, a sink or even internal in regards to `G`.
As such, the edges in `B` do in general not allow to uniquely determine the
relationship between `G` and `S`.

<!-- ======================================================================= -->
## subtree S of super-graph G: case-2, (IBG != Ø)

Graph `G := (V,E)` is the connected non-tree super-graph of the proper subtree
`S := (M,F)` such that `(S != G[V(S)])` is true. Hence, the reason for `G` not
being a tree is due to the edges in `I`, and possibly also due to those edges
in `B := ((G \ S) + OBG)`.

Note that `(IBG != Ø)` and `(OBG <=!=> Ø)`. The focus of this case is therefore
on the edges in `I := G[V(S)]` that are no edge in `S`.

**induced by a subset of vertices - i.e. G(M)**

In this particular case, `S` can not be a subtree that is induced by a set of
vertices (i.e. `(S != G[M])`). That is because `S` would then also contain all
the edges in `IBG`, which would turn `S` into a non-tree graph.

Consequently, `S` must be induced by its set of edges (i.e. `(S == G[F])`).

**induced by a subset of edges - i.e. G(F)**

As mentioned before, the edges in `IBG` do not allow to clarify the relationship
between `G` and `S` because each edge can be understood to be oriented from one
graph to the other. Because of that, these edges need to be avoided.

In addition to `(IBG != Ø)`, the outer border graph may aso be non-empty
(i.e. `(OBG != Ø)` may be true). Therefore, case-1 still in regards to
those edges in `OBG`.
