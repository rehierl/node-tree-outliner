
<!-- ======================================================================= -->
# Unary operations on graphs

<!-- ======================================================================= -->
## converse/transpose graph

* (/see/ "semantics" /)
* note - converse edges and converse semantics

<!-- ======================================================================= -->
## complete graph (Kn)

A graph `G := (V,E)` is **complete**, if each vertex `(v in V)` is adjacent
(as the source of the corresponding edge) to every other vertex. That is,
the set of edges `E` in a complete (directed) graph is equal to the Cartesian
product over its set of vertices `V`.

* `(E == V×V)`, if `G := (V,E)` is complete

Note that in an undirected graph, an arc has no source vertex.
That is because both endpoints of an arc are considered to be equal.

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
will be used to refer to the corresponding directed complete graph `DKn`,
rather than its undirected counterpart `UKn`.

Any graph `G := (V,E)` can be turned into a complete graph, if the missing
edges are added to its set of edges. The resulting complete graph `K(G)` can
therefore be understood to be induced by the input graph `G`. Hence, `K(G)`
can be understood as an **induced complete graph**. (Recall that, the focus
of the term "induced" is understood to be on a fixed "rule", rather than on
a set of existing edges).

Note that ...

* `(V(S) == V(G))` and `(E(G) subset-of E(S))`, if `S := K(G) := (V,F)`
* `(E(G) disjoint-to E(S))`, if `(E(G) == {})`
* `(G == K(G))`, if `G` is complete
* i.e. `(E(G) == E(S))`, if `G` is complete

Note that, similar to universal sets in the context of sets of elements,
complete graphs fulfill a role of "universal graphs". That is, in a given
context, they can be understood to contain every possible vertex and every
possible edge.

<!-- ======================================================================= -->
## complement graph (*)

By standard definition, the complement graph `G*` (or `comp(G)`) of graph
`G := (V,E)` is formed by removing all of its edges from its induced complete
graph `K(G)`.

* `(G*: Graph -> Graph)` where `G* := (V,F)` and `F := (E(K(G)) \ E(G))`
* `(V(G*) == V(G))` and `(E(G*) disjoint-to E(G))`

Note that, by this definition, the complement graph of a complete graph is not
equal to the empty graph `Ø`. That is, `Kn*` is an edgeless-graph that has `n`
disconnected vertices.

* `(Kn* != Ø)` as `(Kn* == (V(Kn),{})`
* `(G & G*) != Ø)` (i.e. `G` and `G*` are not disjoint)

Note that this is in contrary to the universal set of elements `U` as the
complement of the universal set `U*` is the empty set `{}`.

* `(U* == {})`

Note that, from a less strict perspective, an edgeless graph could still be
understood to be empty (i.e. without meaning). That is, if the meaning of
a vertex is understood to be defined by the set of vertices to which it is
adjacent, then each vertex in such a graph has no meaning as it has no
vertices adjacent to it.
