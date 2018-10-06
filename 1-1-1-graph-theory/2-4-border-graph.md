
<!-- ======================================================================= -->
# border graph

The union `T` of the difference graph `(G \ S)` with the subtracted graph `S`
is not necessarily equal to `G` (i.e. it may be, but it does not have to be).
That is due to the required implicit removal of incident edges.

* `G <=!=> T`, where `T := ((G \ S) + S)`
* `(T subgraph-of G)` is always true
* `(T proper-subgraph-of G)` is not necessarily true

<!-- ======================================================================= -->
## inner border graph (IBG)

One aspect of `(G <=!=> T)` is that the "interior" of `S` in `G` may have more
edges than `S` (e.g. `G` has loops, but `S` does not). That is, if `S` is a
subgraph of `G`, then `S` may be a proper subgraph of the graph induced by
the vertex-set `V(S)`. Such edges however do not exist, if `S` is an induced
subgraph of `G` (i.e. if `(S == G[V(S)])`).

* `G[V(S)] <=!=> S`
* `(S subgraph-of G) <-> (S subgraph-of G[V(S)])`
* `(S subgraph-of G) =!> (S proper-subgraph-of G[V(S)])`

Note that the **inner border graph** `IBG(G,S)`, that reduces `G` to the above
subset of edges, can be defined as follows:

* `IBG, IBG(G,S) := (V,E)` where
* `E := { (e in E(G)) | (e !in E(S)) and (E(e) subset-of V(S)) }`
* `V := { (v in V(G)) | (v endpoint-of e) for some (e in E(IBG)) }`
* note - `(IBG(A,B) == IBG(B,A))`

That is, the inner border graph `IBG` is a subgraph of `G` such that all the
endpoints of its edges are in `S`. In addition to that, each edge in `IBG` is
an edge in `G`, but not an edge in `S`. Finally, the vertex-set of `IBG` is
the union of all the endpoints of its edges. That is, the vertex-set in `IBG`
is defined by its set of edges (i.e. `(IBG(G,S) == G[E])`).

Note that the endpoints of each edge in `IBG` are vertices in `S` and `G`.
Because of that, each edge in `IBG` can be said to begin in `G` and to end in
`S`. All of these edges can however also be said to begin in `S` and to end
in `G`. The orientation, with regards to `S` and `G`, of the edges in `IBG` is
therefore unclear. Hence, an inner border graph `IBG` does not allow to clarify
the relationship between a super-graph and its sub-graph.

<!-- ======================================================================= -->
## outer border graph (OBG)

The second aspect of `(G <=!=> T)` is that `G` may contain edges that connect
`(G \ S)` with `G[V(S)]`. However, such edges do not exist, if `G[V(S)]` is a
maximal component in `G`.

Note that the **outer border graph** `OBG(G,S)` can be defined as follows:

* `OBG, OBG(G,S) := (V,E)` where `E := (Ei + Eo)` such that
* `Ei := { ((x,y) in E(G)) | (x in (V(G) \ V(S)) and (y in V(S)) }`
* `Eo := { ((x,y) in E(G)) | (x in V(S)) and (y in (V(G) \ V(S)) }`
* `V := { (v in V(G)) | (v endpoint-of e) for some (e in E(OBG)) }`
* note - `(OBG(A,B) == OBG(B,A))`

That is, the outer border graph `OBG` is a subgraph of `G` such that each edge
in it is an edge in `G` where one of its endpoints is in `(G \ S)` and the
other in `S`. That is, each edge in `OBG` leads from one subgraph to another.
As before, the set of vertices in `OBG` is defined by the set of its edges (i.e.
`(OBG(G,S) == G[E])`).

Note that an outer border graph `OBG` has two subgraphs: One that is limited
to all the edges that point inwards from `(G \ S)` to `S` (i.e. `Ei`, aka.
`OBGi`), and one that is reduced to all the edges that point outwards from
`S` to `(G \ S)` (i.e. `Eo`, aka. `OBGo`). That is, these two subgraphs have
disjoint sets of edges.

* `OBG == (OBGi + OBGo)`
* `(OBGi(A,B) <=!=> OBGi(B,A))`
* `(OBGo(A,B) <=!=> OBGo(B,A))`

Note that `S` may be considered a **source** of `G`, if `(OBGi == Ø)` and
`(OBGo != Ø)` are both true. Likewise, `S` may be considered a **sink** of `G`,
if `(OBGi != Ø)` and `(OBGo == Ø)`. Hence, `S` may be considered **internal**
to `G`, if `(OBGi != Ø)` and `(OBGo != Ø)`. Finally, `S` may be considered to
be **disconnected** from `(G \ S)`, if `(OBGi == Ø)` and `(OBGo == Ø)`. In the
last case, `S` is a subgraph of a maximal component in `G`.

<!-- ======================================================================= -->
## border graph (BG)

In the context of this discussion, `S` is in general formed as an induced
subgraph of `G` (i.e. `(G[V(S)] == S)`). Because of that, `S` contains all
the edges in `G` that have both of their endpoints in `S`. Because of that,
the inner border graph `IBG(G,S)` is expected to be empty.

* `(S == G[V(S)]) -> (IBG(G,S) == Ø)`

Because of that, the term **border graph** `BG(G,S)` (or simply `BG`) is in
general used to refer to the outer border graph `OBG(G,S)` (i.e. `(BG := OBG)`).

Similar to that, `S` is in general formed as a proper induced subgraph of `G`.
The outer border graph between the two is therefore not required to be empty
or to even have a single edge. That is, such a subgraph may or may not be a
maximal component in `G`.

Note that `(G == T)` is true if, and only if `S` is an induced subgraph of
`G` (i.e. `(S == G[V(S)])`) and if `S` represents a maximal component in `G`.
That is, `G` is in any other case unequal to `T`.

* in general `(G == T + IBG(G,S) + OBG(G,S))`
* `(G != T)` if `(IBG != Ø)` and/or `(OBG != Ø)`
* `(G == T)` if `(IBG == Ø)` and `(OBG == Ø)`

<!-- ======================================================================= -->
## example

Given the following two graphs, ...

```
super-graph G              sub-graph S
=============              ===========
1 -> 2 -|-> 3 <-> 3        2 -|-> 3
        |-> 4                 |-> 4
```

* G: `V(G) := {1,2,3,4}` and `E(G) := {(1,2),(2,3),(2,4),(3,3)}`
* S: `V(S) := {2,3,4}` and `E(S) := {(2,3),(2,4)}`

... the corresponding border graphs are as follows:

```
 |= G ===========================|
 |        |= S ================| |
 | |= OBG ====|    |= IBG ===| | |
 | | 1 -> | 2 | -> | 3 <-> 3 | | |
 | |==========|    |=========| | |
 |        |     -> 4           | |
 |        |====================| |
 |===============================|
```

* IBG: `V(IBG) := {3}` and `E(IBG) := {(3,3)}`
* OBG: `V(OBG) := {1,2}` and `E(OBG) := {(1,2)}`

Note that, in this particular example, ...

* `(S != G[V(S)])`, i.e. due to edge `(3,3)`
* `(OBGo == Ø)` and `(OBG == OBGi)`
