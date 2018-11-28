
<!-- ======================================================================= -->
# Subgraphs

Recall that a vertex `(v in V)` in a graph `G := (V,E,P)` is **connected**,
if `vPx` and/or `xPv` is true for some other vertex `(x in V)`. Vertices `v`
and `x` are therefore said to be **connected with** each other.

Also, a vertex `(v in V)` may exist such that neither `vPx` nor `xPv` is true
for another vertex `(x in V)`. That is, a graph may contain vertices that are
no endpoint to any edge `(e in E)`. These kind of vertices will be referred
to as being **isolated** or **disconnected**.

Note that a graph which has no disconnected vertex is not necessarily connected
since such a graph may have more than one maximal component. However, such a
graph can not have any trivial component (i.e. every component in it has two
or more vertices).

<!-- ======================================================================= -->
## remarks

In general, if graphs `S := (T,U)` and `G := (V,E)` have an edge in common,
then both graphs also share both of the endpoints of that edge. Because of
that, two graphs that have intersecting sets of edges also have intersecting
sets of vertices. However, two graphs that have intersecting sets of vertices,
do not necessarily also have intersecting sets of edges.

* `(U intersects E) -> (T intersects V)`

If `(U subset-of E)` is true (i.e. *all the edges in `U` are edges in `E`*),
then a vertex `(v in T)` may still exist that is no vertex in `V`. Vertex `v`
must however be disconnected since an edge incident to `v` would then have to
be an edge in `E`, which in turn would require `v` to also be a vertex in `V`.
Because of that, `(U subset-of E)` does not imply that `(T subset-of V)` is
also true. Likewise, if `(T subset-of V)` is true, then an edge in `U` may
still exist that is no edge in `E`. Because of that, `(T subset-of V)` does
not imply that `(U subset-of V)` is also true.

Put differently, if `(U subset-of E)` is true, then both graphs may still have
overlapping sets of vertices. Likewise, if `(T subset-of V)` is true, then both
graphs may still have overlapping sets of edges. That is, both graphs need to
have further characteristics for both pairs of sets to be related in some way.

* `(U subset-of E) <=!=> (T subset-of V)`

If `(U subset-of E)` is true *in addition to `S` having no disconnected vertex*,
then `(T subset-of V)` is also true. That is because every vertex in `T` then
is an endpoint to one or more edges in `U` and as such also a vertex in `V`.
(Note however that `G` may still have disconnected vertices). In contrary to
that, if `(T subset-of V)` is true in addition to `S` having no disconnected
vertices, then `(U subset-of E)` is still not necessarily true. That is because
`U` may still have an edge not in `E`.

* `(U subset-of E) -> (T subset-of V)`

<!-- ======================================================================= -->
## subgraph

A (simple) **subgraph** `S := (T,U)` is a graph formed from its super-graph
`G := (V,E)` by removing vertices and/or edges from `G`.

* `(S subgraph-of G) := (T subset-of V) and (U subset-of E)`
* `(S subgraph-of G) -> (#T <= #V) and (#U <= #E)`

Note that, if vertex `(v in V)` is removed from a graph, then all the edges
`(e in V)`, to which `v` is an endpoint, must also be removed. That is because
a subgraph must still satisfy the definition of a graph in which the endpoints
of its edges must also be vertices in its set of vertices. Hence, edges may be
removed without further consequence, but the removal of a vertex may trigger
the (implicit) removal of one or more incident edges.

* `T` must include both endpoints of all the edges in `U`
* i.e. `(E(e) subset-of T)` is true for any edge `(e in U)`
* i.e. no edge in `U` leads in-to, or out-of `T`

Note that the semantics of a subgraph is by definition identical to the
semantics of its super-graph. The same applies to an empty subgraph formed
from another graph by removing all of its vertices and edges. And because the
empty graph `Ø` can be formed from any graph (even the empty graph itself),
the semantics of the empty graph needs to be understood to correspond with
the semantics of any (non-empty) graph.

* `(S subgraph-of G) -> (sem(S) == sem(G))`

Similar to simple sets, a **strict/proper subgraph** `S := (T,U)` is formed by
removing at least one vertex and/or edge from its super-graph `G := (V,E)`. Any
graph `G` is therefore a (simple) subgraph, but no proper subgraph to itself.

* `(S proper-subgraph-of G) := (S subgraph-of G) and (S != G)`

In this context, `(S != G)` is equivalent to `(#T != #V) and/or (#U != #E)`.
In addition to that, the sets of vertices and/or edges in `S` must have fewer
elements (i.e. `<` instead of `!=`) than the corresponding set in `G`. That is
because `(S subgraph-of G)` requires any element in `S` to be an element in `G`.

* `(S proper-subgraph-of G) -> (#T < #V) and/or (#U < #E)`

Note that in the context of general graphs, a subgraph may still have the
same amount of vertices and/or edges. In contrary to that, a proper subgraph
may still have at most one set (i.e. vertices ex-or edges) that is equal to
the corresponding set in its super-graph.

<!-- ======================================================================= -->
## related

Two graphs `S := (T,U)` and `G := (V,E)` are said to be **related**
with each other, if one is a subgraph of the other.

* `(S related-to G) := (S subgraph-of G) or (G subgraph-of S)`

Two graphs `S` and `G` are said to be **unrelated** with each other,
if neither of them is a subgraph of the other.

* `(S unrelated-to G) := not (S related-to G)`

Two graphs `S` and `G` are said to be **strictly/properly related**
with each other, if both are related but not equal to each other.
That is, one graph is a proper subgraph of the other.

* `(S strictly-related-to G) := (S related-to G) and (S != G)`

Note that no definition is possible for "strictly unrelated".
