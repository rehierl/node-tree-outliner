
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
* `T` must include both endpoints of all the edges in `U`
* i.e. `(E(e) subset-of T)` is true for all edges `(e in U)`
* i.e. no edge in `U` leads in-to, or out-of `S`
* `(S sub-graph-of G) <-> (G super-graph-of S)`

Note that the semantics of a subgraph is, by the construction of a subgraph,
identical to the semantics of its supergraph. Consequently, the same needs
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
## induced subgraph

An **induced subgraph** `S := (T,U)` is formed from another graph `G := (V,E)`
by removing some of its vertices. In addition to that, the edge-subset `U` is
formed based on the vertex-subset `T` by selecting all those edges `(e in E)`
whose endpoints are both in `T`.

* `S := G[T] := (T,U)` where `U := { (e in E) | (E(e) subset-of T) }`
* i.e. `U` contains all those edges in `E` whose endpoints are both in `T`
* i.e. `S` is a subgraph of `G`, induced by its vertex-subset `T`

Note that, in the context of relations, an induced subgraph represents the
restricted relation of its super-graph. That is, restricted to the given
subset of vertices.

Note that there is in general no requirement or limitation as to how the subset
of vertices `T` is formed. And because `T` may contain disconnected vertices,
an induced subgraph `S := (T,U)` is in general not necessarily connected.

Note that there is no freedom as to how the edge-subset `U` is formed. That is,
the edge-subset `U` can be understood as a consequence of the vertex-subset `T`.

A **strict/proper induced subgraph** `S` is an induced subgraph formed from a
graph `G` by removing at least one vertex - i.e. `(#T < #V)`.

Note that a proper induced subgraph may still have the same edge-subset as
its super-graph - i.e. not necessarily `(#U < #E)`. That is because a proper
induced subgraph may be formed by removing only isolated vertices.

<!-- ======================================================================= -->
## induced-subgraph-of

As before, an induced-subgraph-of operator can be defined as follows:

* where `S := (T,U)` and `G := (V,E)`
* `(S induced-subgraph-of G)` is true, if the following conditions hold:
* (1) `(S subgraph-of G)` is true
* (2) `(U == { (e in E) | (E(e) subset-of T) })` is true

Likewise, a proper/strict-induced-subgraph-of operator can be defined:

* `(S strict-induced-subgraph-of G)` is true, if
* (3) `(S induced-subgraph-of G)` is true
* (4) `(S != G)` is true
* synonymous - proper-induced-subgraph-of

Note that (4) can be simplified as `(#T < #V)`.
