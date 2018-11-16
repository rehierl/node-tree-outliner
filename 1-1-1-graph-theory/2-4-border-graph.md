
<!-- ======================================================================= -->
# border graph

* (/see/ "border edge" in "node trees")

The union `T` of the difference graph `(G \ S)` with the subtracted graph `S`
may be, but does not have to be equal to `G`. That is due to the implicit
removal of incident edges.

* `(G <=!=> T)`, where `T := ((G \ S) + S)`
* `(T subgraph-of G)` is however always true
* `(T proper-subgraph-of G)` is not necessarily true

Recall that `S` in `(G \ S)` is expected to be a subgraph of `G`
(i.e. `(G & S) == S`).

<!-- ======================================================================= -->
## inner border graph (IBG)

One aspect of `(G <=!=> T)` is that the "interior" of `S` in `G` may have more
edges than `S` itself (e.g. `G` has loops, but `S` does not). That is, if `S`
is a subgraph of `G`, then `S` may be a proper subgraph of the graph induced by
the vertex-set `V(S)`. These additional edges however do not exist, if `S` is
equal to that induced subgraph (i.e. if `(S == G[V(S)])`), which is because all
those edges are then also edges in `S`.

* `(S subgraph-of G) <-> (S subgraph-of G[V(S)])`
* `(S subgraph-of G) =!> (S proper-subgraph-of G[V(S)])`
* `S <=!=> G[V(S)]`

The **inner border graph** `IBG(G,S)` can be defined as follows:

* `IBG, IBG(G,S) := (V,E)` where
* `E := { (e in E(G)) | (E(e) subset-of V(S)) and (e !in E(S)) }`
* `V := { (v in V(G)) | (v endpoint-of e) for some (e in E(IBG)) }`

That is, the inner border graph `IBG` is a subgraph of `G` such that all the
endpoints of its edges are vertices in `S`. In addition to that, each edge in
`IBG` is an edge in `G`, but not an edge in `S`. Finally, the vertex-set of
`IBG` is the union of all the endpoints of its edges. That is, the vertex-set
of `IBG` is the result of its set of edges (i.e. `(IBG(G,S) == G[E])`) and as
such does not contain any disconnected vertices.

* given `G` and `S` such that `(IBG != Ø)`
* `(E(IBG) subset-of E(G))` and `(E(IBG) disjoint-to E(S))`
* `(V(IBG) subset-of V(G))` and `(V(IBG) subset-of V(S))`

This definition can not result in a commutative operator. That is because
the edges of the resulting graph need to be edges in the first operand, but
must not be edges in the second operand. Hence, swapping the operands will
in general yield different results.

* `(IBG(G,S) =!> Ø)` if `(S subgraph-of G)`
* `(IBG(G,S) == Ø)` if `(S == G[V(S)])` (!)
* `(IBG(G,S) == Ø)` if `(G subgraph-of S)`
* `(IBG(G,S) != IBG(S,G))` is in general true

Note that both endpoints of each edge in `IBG` are vertices in `S` and `G`.
Because of that, each edge in `IBG` can be said to begin in `G` and end in
`S`. However, these edges can also be said to begin in `S` and end in `G`.
The orientation of those edges is therefore unclear. Hence, the edges in an
inner border graph `IBG` do not allow to clarify the relationship between a
super-graph and its sub-graph.

<!-- ======================================================================= -->
## outer border graph (OBG)

The second aspect of `(G <=!=> T)` is that `G` may contain edges that connect
`(G \ S)` with `G[V(S)]`. However, such edges do not exist, if `G[V(S)]` is
equal to the union of maximal components in `G`, which is because components
are not connected with each other.

The **outer border graph** `OBG(G,S)` can be defined as follows:

* `OBG, OBG(G,S) := (V,E)` where `E := (Ei + Eo)` such that
* `Ei := { ((x,y) in E(G)) | (x in (V(G) \ V(S)) and (y in V(S)) }`
* `Eo := { ((x,y) in E(G)) | (x in V(S)) and (y in (V(G) \ V(S)) }`
* `V := { (v in V(G)) | (v endpoint-of e) for some (e in E(OBG)) }`

That is, the outer border graph `OBG` is a subgraph of `G` such that each
edge is an edge in `G` that has one of its endpoints in `(G \ S)` and the
other in `S`. That is, each edge in `OBG` leads from one subgraph to the
other. As before, the set of vertices in `OBG` is defined by its set of
edges (i.e. `(OBG(G,S) == G[E])`).

Note that an outer border graph `OBG` has two subgraphs: One restricted to all
those edges that point inwards from `(G \ S)` to `S` (i.e. `Ei`, aka. `OBGi`),
and one restricted to all those edges that point outwards from `S` to `(G \ S)`
(i.e. `Eo`, aka. `OBGo`). Consequently, these two subgraphs have disjoint sets
of edges, but not necessarily disjoint sets of vertices.

* `OBG == (OBGi + OBGo)`

This definition can not result in a commutative operator. That is because
all the edges in the outer border graph must have an endpoint in `(G \ S)`.
Hence, swapping the operands will in general yield different results.

* `(OBG(G,S) == Ø)` if `(S disjoint-to G)`
* `(OBG(G,S) =!> Ø)` if `(S subgraph-of G)` - i.e. `((G & S) == S)`
* `(OBG(S,G) == Ø)` if `(S subgraph-of G)` - since `((S \ G) == Ø)`
* `(OBG(G,S) == Ø)` if `(G subgraph-of S)`
* `(OBG(G,S) != OBG(S,G))` is in general true

Note that `S` may be considered a **source** of `G`, if `(OBGi == Ø)` and
`(OBGo != Ø)` are both true. Likewise, `S` may be considered a **sink** of `G`,
if `(OBGi != Ø)` and `(OBGo == Ø)`. Hence, `S` may be considered **internal**
to `G`, if `(OBGi != Ø)` and `(OBGo != Ø)`. And finally, `S` may be considered
to be **disconnected** from `(G \ S)`, if `(OBG == Ø)` is true.

Note that, in the last case, `S` may be a subgraph of the union of maximal
components in `G`. However, that is not entirely accurate as `S` must then
have all the vertices in that union, but is not required to have all the
edges of such a union.

<!-- ======================================================================= -->
## general overview

Given two arbitrary non-empty graphs `S := (T,U)` and `G := (V,E)`, then ...

```
       \ border-graph | IBG(G,S) / | OBG(G,S) / |
 condition \          |   IBG(S,G) |   OBG(S,G) |
-------------------------------------------------
1 | (S disjoint-to G) |   Ø / Ø    |   Ø / Ø    |
-------------------------------------------------
2 | (S == G)          |   Ø / Ø    |   Ø / Ø    |
-------------------------------------------------
3 | (S subgraph-of G) |   ? / Ø    |   ? / Ø    |
-------------------------------------------------
4 | (G subgraph-of S) |   Ø / ?    |   Ø / ?    |
-------------------------------------------------
5 | (S == G[V(S)])    |   Ø / Ø    |   ? / Ø    | (!)
-------------------------------------------------
6 | (S overlaps G)    |   ? / ?    |   ? / ?    |
```

* `Ø` - always empty
* `?` - not necessarily empty

Note that `S` in (3), (4) and (5) is also unequal to `G` as otherwise case
(2) would apply. Hence, `S` is in both cases a proper subgraph of `G`.

Note that both graphs in case (6) are distinct from one another since they
could otherwise not overlap each other. Also, both outer graphs in that case
are not necessarily empty since both graphs may have a single disconnected
vertex that is no vertex in the other graph.

<!-- ======================================================================= -->
## border graph (BG)

In the context of this discussion, `S` is in general formed as an induced
subgraph of `G` (i.e. `(S == G[V(S)])`). Because of that, `S` contains all
the edges in `G` that have both of their endpoints in `S`. As a result, the
the inner border graph `IBG(G,S)` will in general be empty. In contrary to
that, `OBG(G,S)` is not necessarily empty because an induced subgraph may
or may not be equal to the union of one or more maximal components in `G`.

* `(S == G[V(S)]) -> (IBG(G,S) == Ø)`
* `(S == G[V(s)]) =!> (OBG(G,S) == Ø)`

Because of that, the term **border graph** `BG(G,S)` (or simply `BG`) is used
by default to refer to the outer border graph `OBG(G,S)` (i.e. `(BG := OBG)`)

* `(G == T + IBG(G,S) + OBG(G,S))`, where `(T := (G \ S) + S)`
* `(G != T)` if `(IBG != Ø)` and/or `(OBG != Ø)`

Note that the union graph `T := ((G \ S) + S)` is equal to `G` if `S` is an
induced subgraph of `G` (i.e. `(S == G[V(S)])`), and if `S` is the union of
one or more maximal component in `G`.

<!-- ======================================================================= -->
## examples

Given the following two graphs, ...

```
super-graph G         sub-graph S
=============         ===========
1 -> 2 -|-> 3*        2 -|-> 3
        |-> 4            |-> 4
```

* where `*` in `3*` denotes a reflexive edge (i.e. `(3,3)`)
* G: `V(G) := {1,2,3,4}` and `E(G) := {(1,2),(2,3),(2,4),(3,3)}`
* S: `V(S) := {2,3,4}` and `E(S) := {(2,3),(2,4)}`

... the border graphs between the two are as follows:

```
 |= G ===========================|
 |        |= S ================| |
 | |= OBG ====|      |= IBG =| | |
 | | 1 -> | 2 | -|-> | 3*    | | |
 | |==========|      |=======| | |
 |        |      |-> 4         | |
 |        |====================| |
 |===============================|
```

* IBG: `V(IBG) := {3}` and `E(IBG) := {(3,3)}`
* OBG: `V(OBG) := {1,2}` and `E(OBG) := {(1,2)}`

Note that, in this particular example, ...

* `(S != G[V(S)])` - due to `(3,3)`
* `(OBG == OBGi)` - due to `(OBGo == Ø)`
