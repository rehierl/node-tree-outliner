
<!-- ======================================================================= -->
# Definitions related to graphs

* standard and non-standard, graph-based definitions
* the focus is on directed graphs of vertices `G := (V,E)`

Note that the focus of graph theory is in general on undirected graphs.
In contrary to that, the focus of this discussion is on directed graphs.

Note that, in the context of this discussion, a graph is in general expected to
have the following characteristics: a homogenous set of finitely many vertices,
a directed graph with consistent semantics over its edges, not a null graph, not
an edgeless multigraph, acyclic and oriented.

<!-- ======================================================================= -->
## undirected graphs

A finite undirected graph `G` (or `UG`) is defined as follows:

* `G := UG := (V,A)` is a binary/endo-relation of vertices
* `V` is the possibly empty, finite simple set of vertices
* `A` is the possibly empty, finite simple set of arcs
* i.e. `(a subset-of V)` and `(#a == 2)` for all arcs `(a in A)`
* i.e. `A` is a set of 2-element simple sets over `V`

Each vertex `(v in V)` can be understood to represent some unique object.
That is, vertices represent abstract entities whose object properties
are considered to be non-relevant to the corresponding graph.

* `(o: V -> O)` - is a bijective function
* `o(v)` returns the object that vertex `v` represents
* i.e. `(o(x) !== o(y))` where `(x,y in V)`
* i.e. distinct vertices represent distinct objects
* `(v: O -> V)` - is inverse to `o()`
* `v(o)` returns the id/reference/vertex of object `o`
* i.e. `(o(v(o)) === o)` and `(v(o(v)) === n)`

Note that the set of vertices `V` is in general expected to represent
vertices of some kind. That is, all vertices are assumed share common
characteristics, which is why `V` is expected to be a homogenous simple
set of vertices.

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

For purposes of clarification, the following operators may be used:

* `(V: Graph -> Set)` or `V(G) := V` where `G := (V,A)`
* i.e. the set of vertices of the given graph
* `(A: Graph -> Set)` or `A(G) := A` where `G := (V,A)`
* i.e. the set of arcs of the given graph

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
function `E()` such that:

* `(E: V×V -> Bools` or `E(x,y) := ((x,y) in E) or ((y,x) in E)`
* notational - `xEy := E(x,y) := xEy or yEx`

For purposes of clarification, the following operators may be used:

* `(V: Graph -> Set)` or `V(G) := V` where `G := (V,E)`
* i.e. the set of vertices of the given graph
* `(E: Graph -> Set)` or `E(G) := E` where `G := (V,E)`
* i.e. the set of arcs of the given graph

<!-- ======================================================================= -->
## remarks

A graph `G := (V,E)` is referred to as ...

* "edgeless graph", if `(#E == 0)`
* `Ø` or "null graph" or "empty graph", if `(#V == 0) and (#E == 0)`
* i.e. `G := ({},{})` is the null/empty graph `Ø`
* "trivial graph", if `(#V == 1) and (#E == 0)`
* "oriented graph", if `xEy` then `!yEx` (i.e. one direction only)

Note that the binary relation of an oriented graph is irreflexive/strict
and anti-symmetric. That is, the binary relation of an oriented graph is
consequently a-symmetric.

An edge `((x,y) in E)` is referred to as ...

* a "loop", if `(x == y)`
* a "link", if `(x != y)`

Note that `E` is a set of ordered pairs. That is, if `xEy` is true for two
vertices `(x,y in V)`, then there is one, and only one edge `(e in E)` such
that `e := (x,y)`. That is, `E` is a simple set, not a multiset of edges.
(Note that `xEy` and `yEx` count as one edge if `(x == y)`). A graph that
is based upon a multiset of edges is referred to as a **multigraph**.

Note that, `xEx` may be true for any vertex in a graph. That is, edges may in
general exist that begin and end in the same vertex `x`. These kind of edges
may in general be referred to as "loops" or as "reflexive edges". Because of
that, a graph with no such edges may be referred to as being **loopless** or
"irreflexive".

Note that for each directed graph `G := (V,E)`, an undirected graph
`UG := (V,A)` can be formed such that `({x,y} in A)` if `xEy`. That is, for
each edge `((x,y) in G)`, `A` contains an arc `{x,y}`. (Note that two distinct
edges may correspond with the same arc). An undirected graph formed this way
will be referred to as the **underlying undirected graph** `UG(G)` of the
corresponding directed graph `G`.

Note that for each undirected graph `G := (V,A)`, a directed graph `DG := (V,E)`
can be formed such that `((x,y) in E)` if `xAy`. That is, for each arc
`({x,y} in A)`, `E` may contain `(x,y)` and/or `(y,x)`. If each arc corresponds
with one edge only, then a directed graph formed such way will be referred to
as an **orientation** of an undirected graph. Obviously, and in contrary to
"UG(G)", an undirected graph may in general have several distinct orientations.

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
## equality, inequality, isomorphic

Two directed graphs `S := (T,U)` and `G := (V,E)` are considered to be
**equal** if both graphs have equal sets of vertices, equal sets of edges,
and equal semantics.

* `(S == G)`, iff `(T == V)` and `(U == E)` and `(sem(S) == sem(G))`
* `(S equal-to) := (S == G)`

Note that the "equal semantics" aspect ensures that both graphs are of the
same "sort". In a given context, the graphs in question usually satisfy that
condition, which is why that aspect is in general omitted.

In contrary to that, two directed graphs are **unequal**, if they differ in
their sets of vertices, their sets of edges, and/or in their semantics.

* `(S != G) := not (S == G)`
* `(S != G)`, iff `(T != V)` or `(U != E)` or `(sem(S) != sem(G))`
* `(S unequal-to G) := (S != G)`

Note that two unequal graphs may still be isomorphic to each other. That is,
an isomorphism may still exists that maps one graph onto the other. If such an
isomorphism exists, both graphs are said to be **isomorphic** to each other.

* (/see/ "category theory" /)

Note that two isomorphic graphs may have different semantics. Because of that,
"isomorphic" is understood more in the sense of "both have the same structure"
(i.e. both are **equivalent**), whereas "equal" is understood in the sense of
"both represent the exact same graph" (i.e. both are **identical**).

**TODO** - does "equivalent vs. identical" represent standard convention?
