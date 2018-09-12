
<!-- ======================================================================= -->
# Definitions related to graphs

* a summary of (relevant) standard and non-standard definitions
* the focus is on directed graphs of vertices

Note that, in the context of this discussion, a graph is by default assumed to
have the following characteristics: not a multigraph, not a null graph, not an
edgeless graph, acyclic and oriented. Hence, the underlying endo-relation of
a graph is assumed to be asymmetric.

<!-- ======================================================================= -->
## basic definitions

A (finite directed) graph `G` is defined as a tuple of sets:

* `G := (V,E)` is a binary/endo-relation of vertices
* `V` is the possibly empty finite set of vertices
* `(E subset-of V×V)` is the possibly empty finite set of directed edges
* such that `(E(e) subset-of V)` for all `(e in E)`
* i.e. both endpoints of each edge are vertices in `V`

Each vertex `(v in V)` can be understood to represent some unique object.
That is, vertices represent abstract entities whose object properties are
considered to be non-relevant to the corresponding graph.

* `(o: V -> O)` - is a bijective function
* `o(v)` returns the object that vertex `v` represents
* i.e. `(o(x) !== o(y))` where `(x,y in V)`
* i.e. distinct vertices represent distinct objects
* `(v: O -> V)` - is inverse to `o()`
* `v(o)` returns the id/reference/vertex of object `o`
* i.e. `(o(v(o)) === o)` and `(v(o(v)) === n)`

The following can be said about the vertices of any edge:

* `e := (x,y)` or `(x -> y)`
* `x` and `y` are adjacent to each other
* `x` and `y` are both endpoints of `e`
* `x` and `y` are both neighbors to each other
* `x` is covered by `y`, and `y` is covered by `x`
* `x` is a source to `y`, and `y` a sink to `x`

The following can be said about an edge `e` and the relationship it has
with both of its vertices `x` and `y`:

* `e` is an ordered pair of vertices
* `e` begins in `x` and ends in `y`
* `e` is an outgoing edge of `x`, and an incoming edge to `y`
* `e` has `x` as its source and `y` as its sink
* `e` is incident to `x` and `y`

Each graph can be understood to have an indicator function `E()` such that:

* `(E: V×V -> Bool)` or `E(x,y) := ((x,y) in E)`
* notational: `xEy := E(x,y)`

<!-- ======================================================================= -->
## remarks

A graph `G := (V,E)` is referred to as ...

* an "edgeless graph", if `(#E == 0)`
* a "null graph", if `(#V == 0) and (#E == 0)`
* a "trivial graph", if `(#V == 1) and (#E == 0)`
* an "oriented graph", if `((x,y) in E)`, then `((y,x) !in E)`

An edge `((x,y) in E)` is referred to as ...

* a "loop", if `(x == y)`
* a "link", if `(x != y)`

Note that `E` is a set of ordered pairs. That is, if `xEy` is true for two
vertices `(x,y in V)`, then there is one, and only one edge `(e in E)` such
that `e := (x,y)`. That is, `E` is a simple set, not a multiset of edges.
(Note that `xEy` and `yEx` count as one edge if `(x == y)`). A graph that
has a multiset of edges is referred to as a "multigraph".

Note that for each directed graph `G := (V,E)`, an undirected graph `H := (V,F)`
can be formed such that `xFy` and `yFx` iff `xEy`. That is, for each edge
`((x,y) in G)`, `F` contains both `(x,y)` and `(y,x)`. This underlying graph
may be referred to as the "underlying undirected graph of `G`" (short: `H(G)`).

Note that, `xEx` may be true for any vertex in a graph. That is, edges may in
general exist that begin and end in the exact same vertex `x`. These kind of
edges may in general be referred to as "loops" or "reflexive edges". Because
of that, a graph with no such edges may be referred to as "loopless" or
"irreflexive".

<!-- ======================================================================= -->
## subsets of vertices

* `VI := { (v in V) | xEv for some (x in V) }`
* i.e. the set of vertices that have an incoming edge
* `VO := { (v in V) | vEx for some (x in V) }`
* i.e. the set of vertices that have an outgoing edge

Based on these two sets, the following subsets of `V` can be defined:

* `DV := { (v in V) | (v !in VI) and (v !in VO) }`
* i.e. the set of disconnected/isolated vertices
* `CV := { (v in V) | (v in VI) or (v in VO) }`
* i.e. the set of connected vertices
* `RV := { (v in V) | vEv }`
* i.e. the set of reflexive vertices
* `SRC := { (v in V) | (v !in VI) and (v in VO) }`
* i.e. the set of source vertices
* `SNK := { (v in V) | (v in VI) and (v !in VO) }`
* i.e. the set of sink vertices
* `INT := { (v in V) | (v in VI) and (v in VO) }`
* i.e. the set of internal vertices

Similar to that, the following functions can be defined:

* `(src: N -> P(V))`, or `src(v) := { x | xEv }`
* i.e. `src(v)` returns the set of vertices that are sources to `v`
* i.e. all those vertices to which `v` is a sink
* i.e. `ideg(v), in-degree(v) := #src(v)`
* `(snk: N -> P(V))`, or `snk(v) := { x | vEx }`
* i.e. `snk(v)` returns the set of vertices that are sinks to `v`
* i.e. all those vertices to which `v` is a source
* i.e. `odeg(v), out-degree(v) := #snk(v)`

**TODO**
- define a term equivalent to "siblings"? - i.e. snk(v)
- define a term equivalent to "parent"? - i.e. src(v)

<!-- ======================================================================= -->
## semantics of a graph

The edges of a graph `G := (V,E)` represent the relationship between two
adjacent vertices `(x,y in V)`: e.g. `(x divisible-by y)`. The semantics
of distinct graphs `sem(G)` differ in general.

* `sem(G) := (x divisible-by y)`
* i.e. `((x,y) in E)` iff `x` is divisible by `y`
* `sem(H) := (x multiple-of y)`
* i.e. `((x,y) in E)` iff `x` is a multiple of `y`

However, the semantics of each edge in a single graph is identical to the
semantics of the graph - i.e. `(sem(e) == sem(G))` for any edge `(e in E)`.
Consequently, the semantics of a graph `sem(G)` applies to all of its edges,
which is why all edges in a graph are of the same sort (i.e. have the same
meaning). As such, any graph in the context of this discussion may be
referred to as being "homogenous".

Put differently, the semantics of a graph is the "reason" as to why two
vertices are connected. Furthermore, that reason is the same for any other
pair of adjacent vertices.
