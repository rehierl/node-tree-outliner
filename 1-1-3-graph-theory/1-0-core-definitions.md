
<!-- ======================================================================= -->
# Definitions related to graphs

* a summary of (relevant) standard and non-standard definitions
* the focus is on directed graphs of vertices

Note that, in the context of this discussion, a graph is in general assumed
to have the following characteristics: a directed graph, not a null graph,
finitely many vertices, not an edgeless multigraph, is acyclic and oriented.
Hence, the underlying relation of a graph is assumed to be asymmetric.

<!-- ======================================================================= -->
## undirected graphs

A finite undirected graph `G` (or `UG`) is defined as follows:

* `G := UG := (V,A)` is a binary/endo-relation of vertices
* `V` is the possibly empty, finite simple set of vertices
* `A` is the possibly empty, finite simple set of arcs
* i.e. `(a subset-of V)` and `(#a == 2)` for all arcs `(a in A)`
* i.e. `A` is a set of 2-element sets over `V`

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

The following can be said about the vertices of any arc `(a in A)`:

* `a := {x,y}`
* `x` and `y` are both endpoints of `a`
* `x` and `y` are adjacent to each other
* `x` and `y` are neighbors to each other
* `x` is covered by `y`, and `y` is covered by `x`
* i.e. `x` and `y` are considered to be equal

The following can be said about an arc `a` and the relationship it has
with both of its vertices `x` and `y`:

* `a` is an un-ordered pair of vertices
* `a` is incident to `x` and `y`

Each graph can be understood to have an indicator function `A()` such that:

* `(A: V×V -> Bool)` or `A(x,y) := ({x,y} in A)`
* notational - `xAy := A(x,y)`

<!-- ======================================================================= -->
## directed graphs

A (finite directed) graph `G` (or `DG`) is defined as a tuple of sets:

* `G := DG := (V,E)` is a binary/endo-relation of vertices
* `V` is the possibly empty, finite simple set of vertices
* `E` is the possibly empty, finite simple set of directed edges
* i.e. `(E subset-of V×V)` - i.e. `(E(e) subset-of V)` for any `(e in E)`

As before, a vertex `(v in V)` in a directed graph is understood to represent
a distinct object. That is, `o(v)` returns the object a vertex represents,
and `v(o)` the vertex of a given object.

The following can be said about the vertices of any edge `(e in E)`:

* `e := (x,y)` or `(x -> y)`
* `x` and `y` are both endpoints of `e`
* `x` and `y` are adjacent to each other
* `x` is covered by `y`, and `y` is covered by `x`
* `x` is a source to `y`, and `y` a sink to `x`
* i.e. `x` and `y` are considered to be un-equal
* i.e. edges are directed arcs, and arcs undirected edges

The following can be said about an edge `e` and the relationship it has
with both of its vertices `x` and `y`:

* `e` is an ordered pair of vertices
* `e` begins in `x` and ends in `y`
* `e` is an outgoing edge of `x`, and an incoming edge to `y`
* `e` has `x` as its source and `y` as its sink
* `e` is incident to `x` and `y`

Each graph can be understood to have an indicator function `E()` such that:

* `(E: V×V -> Bool)` or `E(x,y) := ((x,y) in E)`
* notational - `xEy := E(x,y)`

In addition to that, a directed graph can be understood to have an indicator
function `A()` such that:

* `(A: V×V -> Bools` or `A(x,y) := ((x,y) in E) or ((y,x) in E)`
* notational - `xAy := A(x,y) := xEy or yEx`

<!-- ======================================================================= -->
## remarks

Note that the focus of this discussion is on directed graphs `DG := (V,E)`
rather than on undirected graphs `UG := (V,A)`.

A graph `G := (V,E)` is referred to as ...

* an "edgeless graph", if `(#E == 0)`
* a "null graph" or an "empty graph", if `(#V == 0) and (#E == 0)`
* a "trivial graph", if `(#V == 1) and (#E == 0)`
* an "oriented graph", if `((x,y) in E)`, then `((y,x) !in E)`

Note that the binary relation of an oriented graph is irreflexive (aka.
strict) and anti-symmetric. That is, the binary relation of such a graph
is a-symmetric.

An edge `((x,y) in E)` is referred to as ...

* a "loop", if `(x == y)`
* a "link", if `(x != y)`

Note that `E` is a set of ordered pairs. That is, if `xEy` is true for
two vertices `(x,y in V)`, then there is one, and only one edge `(e in E)`
such that `e := (x,y)`. That is, `E` is a simple set, not a multiset of
edges. (Note that `xEy` and `yEx` count as one edge if `(x == y)`). A graph
that is based upon a multiset of edges is referred to as a **multigraph**.

Note that, `xEx` may be true for any vertex in a graph. That is, edges
may in general exist that begin and end in the exact same vertex `x`.
These kind of edges may in general be referred to as "loops" or as
"reflexive edges". Because of that, a graph with no such edges may be
referred to as **loopless** or "irreflexive".

Note that for each directed graph `G := (V,E)`, an undirected graph
`UG := (V,A)` can be formed such that `({x,y} in A)` iff `xEy`. That is,
for each edge `((x,y) in G)`, `A` contains an arc `{x,y}`. An undirected
graph formed such way will be referred to as the "underlying undirected
graph of a directed graph" (short: **UG(G)**).

Note that for each undirected graph `G := (V,A)`, a directed graph
`DG := (V,E)` can be formed such that `((x,y) in E)` iff `xAy`. That is,
for each arc `({x,y} in A)`, `E` contains an edge `(x,y)`. A directed
graph formed such way will be referred to as an "orientation of an
undirected graph". Obviously, and in contrary to "UG(G)", an undirected
graph has in general several different orientations.

<!-- ======================================================================= -->
## subsets of vertices

The following subsets of `V` can be defined:

* `VI := { (v in V) | xEv for some (x in V) }`
* i.e. the set of vertices that have an incoming edge
* i.e. all vertices that are a sink to one or more edges
* `VO := { (v in V) | vEx for some (x in V) }`
* i.e. the set of vertices that have an outgoing edge
* i.e. all vertices that are a source to one or more edges

Based on these two sets, the definition of further subsets is possible:

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

* `(src: V -> P(V))`, or `src(v) := { x | xEv }`
* i.e. `src(v)` returns a set of vertices that are sources to `v`
* i.e. all those vertices to which `v` is a sink
* i.e. `ideg(v), in-degree(v) := #src(v)`
* `(snk: V -> P(V))`, or `snk(v) := { x | vEx }`
* i.e. `snk(v)` returns a set of vertices that are sinks to `v`
* i.e. all those vertices to which `v` is a source
* i.e. `odeg(v), out-degree(v) := #snk(v)`

<!-- ======================================================================= -->
## semantics of a graph

The edges of a graph `G := (V,E)` represent the relationship between two
adjacent vertices `(x,y in V)` - e.g. `(x divisible-by y)`. Hence, and in
general, the semantics of two distinct graphs differ in general. (Note that
`sem(G)` will be used to refer to the semantics of the corresponding graph).

* `sem(G) := (x divisible-by y)`
* i.e. `((x,y) in E)` iff `x` is divisible by `y`
* `sem(H) := (x multiple-of y)`
* i.e. `((x,y) in E)` iff `x` is a multiple of `y`

However, the semantics of each edge in a single graph is identical to the
semantics of the graph - i.e. `(sem(e) == sem(G))` for any edge `(e in E)`.
Because of that, the semantics of a graph `sem(G)` can be said to apply to
all of its edges. All edges in a graph are therefore understood to be of
the same sort (i.e. have the exact same meaning). As such, any graph in the
context of this discussion can be referred to as being "homogenous", or to
have "homogenous/consistent semantics".

Put differently, the semantics of a graph is the "reason" as to why two
vertices are connected. Furthermore, that reason is the same for any other
pair of adjacent vertices.
