
<!-- ======================================================================= -->
## Operations on graphs

* (/see/ "relationships between sets" /)
* the general focus is (still) on directed (simple) graphs

Note that the focus of the following definitions is on the ability to describe
the relationship of a graph with its subgraphs. The definitions below therefore
create new graphs by executing set-based operations  (e.g. union of sets) on
the corresponding sets of vertices and/or on the corresponding sets of edges.
That is, the following definitions won't in general create (entirely) new
entities of vertices and/or edges.

<!-- ======================================================================= -->
## equal, unequal, distinct

* (/see/ "core definitions" /)
* `(S == G)`, iff `(T == V)` and `(U == E)` and `(sem(S) == sem(G))`
* `(S == G) := (S subgraph-of G) and (G subgraph-of S)`
* `(S != G) := not (S == G)`

Note that two unequal graphs are said to be **distinct** (from one another).

<!-- ======================================================================= -->
## disjoint, coupled, overlap

Two graphs `S := (T,U)` and `G := (V,E)` are said to be **disjoint** (to each
other), if and only if they have no vertex and no edge in common:

* `(S disjoint-to G)`, iff `(T disjoint-to V)` and `(U disjoint-to E)`
* `(S disjoint-to G) <-> (G disjoint-to S)`
* note - `(A disjoint-to B) := ((A & B) == {})`

Two graphs `S` and `G` are said to be **coupled** (with each other), if and
only if both graphs have one or more vertices and/or edges in common:

* `(S coupled-with G) := not (S disjoint-to G)`
* `(S coupled-with G)`, iff `(T coupled-with V) and/or (U coupled-with E)`
* `(S coupled-with G) <-> (G coupled-with S)`
* note - `(A coupled-with B) := ((A & B) != {})`

Similar to common elements in coupled simple sets of elements, the above
common vertices and edges act as a "link" between the two graphs involved.
These links can therefore be understood to bind both graphs together, which
is why those graphs can be said to be "connected" or "coupled" with each
other via some "point of contact".

Because both vertices of any edge in a graph `G` must be elements in a graph's
set of vertices, two coupled graphs always have non-disjoint sets of vertices.
That is because the vertices of a common edge always are elements of both sets
of vertices `T` and `V`.

* `(U coupled-with E) -> (T coupled-with V)`

Note that, by definition, any non-empty subgraph `S` of a graph `G` is coupled
with its supergraph. That is, a subgraph is never disjoint to its supergraph.

* `(S related-to G) -> (S coupled-with G)`

Note that the converse is not necessarily true. That is, two coupled graphs
are not necessarily related to each other.

Two graphs `S := (T,U)` and `G := (V,E)` are said to **overlap** (each other),
if both are coupled with each other, but each of them has one or more vertices
and/or edges the other graph does not have.

* `(S overlaps G) := (S coupled-with G) and (S unrelated-to G)`
* `(S overlaps G) <-> (G overlaps S)`

<!-- ======================================================================= -->
## union (+, or, union)

Graph `G := (V,E)` is said to be the **union** graph of two graphs `S := (T,U)`
and `X := (Y,Z)`, if its vertex-set is the union of the vertex sets of both
graphs, and if its edge-set is the union of the edge sets of both graphs.

* `G := (S + X) := ((T+Y), (U+Z))`
* i.e. `(V == (T + Y))` and `(E == (U + Z))`
* associative - `(A + B + C) == ((A + B) + C) == (A + (B + C))`
* commutative - `(A + B) == (B + C)`
* `(sem(S) == sem(X))` must be true

<!-- ======================================================================= -->
## intersection (&, and, isect)

Graph `G := (V,E)` is said to be the **intersection** graph of the two graphs
`S := (T,U)` and `X := (Y,Z)`, if `G` was formed by taking all vertices and
edges that are common to `S` and `X`.

* `G := (S & X) := (V,E)`, where
* `V := { (v in T) | (v in Y) }` and
* `E := { (e in U) | (e in Z) }`
* associative - `(A & B & C) == ((A & B) & C) == (A & (B & C))`
* commutative - `(A & B) == (B & C)`
* `(sem(S) == sem(X))` must be true

Note that `G` is a subgraph to both graphs `S` and `X`.

* `(G subgraph-of S) and (G subgraph-of X)` is true, if `(G == (S & X))`

Two graphs `S` and `X` are said to **intersect** (each other), if
the intersection of both graphs is unequal to the empty graph.

* `(S intersects X) := ((S & X) != ({},{}))`
* `(S intersects X) <-> (X intersects S)`
* `(S intersects X) <-> (S coupled-with X)`

Note that two intersecting graphs do not necessarily overlap each other.

* `(S overlaps G) -> (S intersects G)`

<!-- ======================================================================= -->
## complete graph (Kn)

A graph `G := (V,E)` is **complete**, if each vertex `(v in V)` is adjacent
(as the source of the corresponding edge) to every other vertex.

Note that in an undirected graph, an arc has no source.
That is because both vertices of all arcs are considered to be equal.

undirected complete graphs (UKn)

* an undirected complete graph `UKn` with `n` vertices has `n*(n-1)/2` arcs
* `UK1` is a 1-vertex, edgeless graph
* `UK2` is a 2-vertex graph with one arc

directed complete graphs (DKn)

* a directed complete graph `DKn` with `n` vertices has `n*(n-1)` edges
* `DK1` is a 1-vertex, edgeless graph
* `DK2` is a 2-vertex graph with two edges

Note that an undirected complete graph is equal to the underlying undirected
graph of the corresponding directed complete graph - i.e. `(UKn == UG(DKn))`.

Note that the focus of this discussion is on directed graphs. Hence, `Kn`
will be used to refer to the corresponding directed complete graph `DKn`
rather than its undirected counterpart.

Any graph `G := (V,E)` can be turned into a complete graph, if the missing
edges are added to its set of edges. The resulting complete graph `K(G)` can
therefore be understood to be induced by the input graph's set of vertices
`V(G)`, even though graph `G` may be missing some edges in `K(G)`.

Note that the term "induced" is thus understood as: The resulting graph can
be created "based on a given set of vertices", and "based on a certain rule
which allows to uniquely determine the corresponding (new) edges". Hence,
`K(G)` is understood as an **induced complete graph**.

Note that ...

* `K(G) := S := (V,F)`
* i.e. `(V(S) == V(G))`
* i.e. `(E(G) subset-of E(S))`
* `(E(G) disjoint-to E(S))`, iff `(E(G) == {})`
* `(G == K(G))`, iff `G` is complete
* i.e. `(E(G) == E(S))`, iff `G` is complete

Note that, similar to universal sets in the context of sets of elements,
complete graphs act have the role of "universal graphs". That is, in a given
context, they can be understood to contain every possible vertex and every
possible edge.

<!-- ======================================================================= -->
## complement graph (standard)

By standard definition, the complement graph `G*` (or `comp(G)`) of graph
`G := (V,E)` is formed by removing all its edges from its induced complete
graph `K(G)`.

* `(G*: Graph -> Graph)` where `G* := (V, E(K(G)) \ E(G))`
* `(V(G*) == V(G))` and `(E(G*) disjoint-to E(G))`

Note that, by that definition, the complement graph of a complete graph is
unequal to the empty graph. That is, `Kn*` is an edgeless-graph that has `n`
disconnected vertices.

<!-- ======================================================================= -->
## complement graph (non-standard)

<!-- ======================================================================= -->
## graph difference (\, sub, diff)

<!-- ======================================================================= -->
## symmetric graph difference (^, xor, ex-or)
