
<!-- ======================================================================= -->
# Subgraphs

Note that a vertex `(v in V)` in a graph `G := (V,E,P)` is **connected**, if
`vPx` and/or `xPv` is true for some other vertex `(x in V)`. In addition to
that, `v` is said to be **connected with** vertex `x`.

Note that a vertex `(v in V)` may exist such that neither `vPx` nor `xPv` is
true for any vertex `(x in V)`. That is, a graph may contain vertices that
are no endpoint to any edge `(e in E)`. These kind of vertices are said to
be **isolated/disconnected**.

<!-- ======================================================================= -->
## subgraph

A (simple) **subgraph** `S := (T,U)` is a graph derived from another graph
`G := (V,E)` by removing some of its vertices and/or edges.

* `(T subset-of V)` and `(U subset-of E)`
* `(S sub-graph-of G) <-> (G super-graph-of S)`

Note that, if vertex `(v in V)` is removed from a super-graph, then all edges
`(e in V)` that have `v` as an endpoint, but are not also incident to another
vertex `(x in V)`, must be removed as well. That is because the resulting
sub-graph still needs to satisfy the definition of a graph. Hence, edges may
be removed without further consequence, but the removal of a vertex may trigger
the removal of additional edges.

* `T` must include all endpoints of all edges in `U`
* i.e. `(E(e) subset-of T)` is true for all edges `(e in U)`
* i.e. no edge in `U` leads in-to, or out-of `S`

Note that the semantics of a subgraph is, by the construction of a subgraph,
identical to the semantics of its super-graph. The same therefore also needs
to apply to an empty subgraph.

* `(S subgraph-of G) -> (sem(S) == sem(G))`

Similar to simple sets, a **strict/proper subgraph** is formed by removing
at least one vertex and/or edge - i.e. `(#T < #V)` and/or `(#U < #E)`. That
is, any graph `G` is a (simple) subgraph, but no proper subgraph to itself.

<!-- ======================================================================= -->
## subgraph-of

Given the two graphs `S := (T,U)` and `G := (V,E)`, a subgraph-of operator
can be defined.

* `(S subgraph-of G)` is true, if the following conditions hold:
* (1) `(T subset-of V)` and `(U subset-of E)` are both true
* (2) `(E(e) subset-of T)` is true for all `(e in U)`
* (3) `(sem(S) == sem(G))` is true

Similar to that, a proper/strict-subgraph-of operator can be defined.

* `(S strict-subgraph-of G)` is true, if the following conditions hold:
* (4) `(S subgraph-of G)` is true
* (5) `(S != G)` is true
* synonymous - proper-subgraph-of

Note that, if condition (2) is not met, then `S` is not even a graph. Also,
(5) can be simplified as `(#T < #V)` and/or `(#U < #E)`. That is, the test
for in-equality can be reduced to a test of in-equality with regards to the
corresponding numbers of elements.

Note that the subgraph-of operator is no longer a removal-based operator.

<!-- ======================================================================= -->
## related-to, unrelated-to

Two graphs `S := (T,U)` and `G := (V,E)` can be said to be **related** with
each other, if one is a subgraph of the other.

* `(S related-to G) := (S subgraph-of G) or (G subgraph-of S)`

Likewise, two graphs `S` and `G` can be said to be **strictly related** with
each other, if both are related, but not equal. That is, one is a proper
subgraph of the other.

* `(S strictly-related-to G) := (S related-to G) and (S != G)`

Note that, because the subgraph-of operator is no removal-based operator,
any two separate/distinct graph entities may be related to each other. That
is, (even though it still is) a subgraph does not need to be embedded into
its supergraph.

Two graphs `S` and `G` are said to be **unrelated** with each other, if both
are not related to each other. That is, neither one of them is a subgraph of
the other.

* `(S unrelated-to G) := not (S related-to G)`

Note that there is no definition (possible) for "strictly unrelated".

<!-- ======================================================================= -->
## induced subgraph (V)

An **induced subgraph** `S := (T,U)` is formed from another graph `G := (V,E)`
by removing some of its vertices. In addition to that, the edge-subset `U` is
formed based on the vertex-subset `T` by selecting all those edges `(e in E)`
whose endpoints are both in `T`.

* `S := G[T] := (T,U)` where `U := { (e in E) | (E(e) subset-of T) }`
* i.e. `U` contains all those edges in `E` whose endpoints are both in `T`
* i.e. `S` is a subgraph of `G`, induced by its vertex-subset `T`

Note that, in the context of relations, an induced subgraph represents a
restriction of its super-relation. That is, restricted to the given subset
of vertices.

Note that there is in general no requirement or limitation as to how the subset
of vertices `T` is formed. And because `T` may contain disconnected vertices,
an induced subgraph `S := (T,U)` is in general not necessarily connected.

Note that there is no freedom as to how the edge-subset `U` is formed. That is,
the edge-subset `U` can be understood as a consequence of the vertex-subset `T`.
Because of that, the term "induced" is understood as: The resulting graph is
created "based on a given set of vertices", and "based on a certain rule which
allows to uniquely determine all the edges in the resulting graph".

Note that a non-empty graph `S`, that is a subgraph of `G`, is also a subgraph
of the graph induced by the vertex-set of `G` (i.e. `G[V(G)]`). In general, if
`S` is a subgraph of an induced subgraph `G[X]` (i.e. induced by a subset of
the vertices in `G`), then `S` is also subgraph of `G` itself. The converse is
not in general true because, if `S` is a subgraph of `G`, then `S` is not a
subgraph to all possible induced subgraphs of `G`. However, at least one such
induced induced subgraph always exist.

* `(S subgraph-of G) <- (S subgraph-of G[X])`
* `(S subgraph-of G) <-> (S subgraph-of G[V(G)])`
* `(S subgraph-of G) <-> (S subgraph-of G[V(S)])`

A **strict/proper induced subgraph** `S` is an induced subgraph formed from
a graph `G` by removing at least one vertex - i.e. `(#T < #V)`.

Note that a proper induced subgraph may still have the same edge-subset as
its super-graph - i.e. not necessarily `(#U < #E)`. That is because a proper
induced subgraph may be formed by removing only isolated vertices.

<!-- ======================================================================= -->
## induced-subgraph-of (V)

As before, an induced-subgraph-of operator can be defined as follows:

* for `S := G[T]` where `S := (T,U)` and `G := (V,E)`
* `(S induced-subgraph-of G)` is true, if the following conditions hold:
* (1) `(S subgraph-of G)` is true
* (2) `(U == { (e in E) | (E(e) subset-of T) })` is true

Likewise, a proper/strict-induced-subgraph-of operator can be defined:

* `(S strict-induced-subgraph-of G)` is true, if
* (3) `(S induced-subgraph-of G)` is true
* (4) `(S != G)` is true
* synonymous - proper-induced-subgraph-of

Note that (4) can be simplified as `(#T < #V)`.

<!-- ======================================================================= -->
## induced subgraph (E)

The above definition of an induced subgraph `S` may be referred to as being
**induced by a subset of vertices** (i.e. `S := G[V]`) such that the vertex
set in `S` holds all those vertices in `V` that are also vertices in `V(G)`
(i.e. `V(S) == (V(G) & V)`). Consequently, the "fixed" rule then is to take
all those edges in `G` that have both of their endpoints in `V(S)`.

* `S := G[V] := (T,U)` where `T := (V(G) & V)` and
* `U := { (e in E(G)) | (E(e) subset-of T) }`

Similar to that, an induced subgraph `S` can be defined based upon a subset
of edges `E` (i.e. `S := G[E]`): An induced subgraph, **induced by a subset
of edges** `E`, is a subgraph of `G` such that the edge set in `S` holds all
those edges in `E` that are also edges in `E(G)` (i.e. `E(S) == (E(G) & E)`).
Consequently, the "fixed" rule then is to take all those vertices in `G` that
are endpoints to one or more edges in `E(S)`.

* `S := G[E] := (T,U)` where `U := (E(G) & E)` and
* `T := { (v in V(G)) | (v endpoint-of e) for some (e in U) }`

Note that `G[E]` can not have any disconnected vertices. Hence, `G[E(G)]` may
be used to refer to the maximal subgraph of `G` that has no isolated vertices.
Note however that `G[E]` may itself still be disconnected as it may have more
than one maximal component with two or more vertices.

Note that `V(S)` in `S := G[T]` is not necessarily equal to `T`. Likewise,
`E(S)` is not necessarily equal to `E` in `S := G[E]`. In general both sets
are assumed to be equivalent because the input sets are in general expected
to be reduced to the appropriate elements (i.e. no element not in `G`).
