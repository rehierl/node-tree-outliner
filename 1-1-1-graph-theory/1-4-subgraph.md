
<!-- ======================================================================= -->
# Subgraphs

Note that a vertex `(v in V)` in a graph `G := (V,E,P)` is **connected**, if
`vPx` and/or `xPv` is true for some other vertex `(x in V)`. Because of that,
both vertices `v` and `x` are said to be **connected with** each other.

Note that a vertex `(v in V)` may exist such that neither `vPx` nor `xPv` is
true for any other vertex `(x in V)`. That is, a graph may contain vertices
that are no endpoint to any edge `(e in E)`. These kind of vertices are said
to be **isolated** or **disconnected**.

<!-- ======================================================================= -->
## subgraph

A (simple) **subgraph** `S := (T,U)` is a graph formed from another graph
`G := (V,E)` by removing some of the vertices and/or edges in `G`.

* `(T subset-of V) and (U subset-of E)`
* `(S sub-graph-of G) <-> (G super-graph-of S)`

Note that, if vertex `(v in V)` is removed from a super-graph, then all edges
`(e in V)` that have `v` as an endpoint, must also be removed. That is because
a subgraph must still satisfy the definition of a graph in which the endpoints
of its edges are vertices in its set of vertices. Hence, edges may be removed
without further consequence, but the removal of a vertex may trigger the
(implicit) removal of edges.

* `T` must include both endpoints of all the edges in `U`
* i.e. `(E(e) subset-of T)` is true for any edge `(e in U)`
* i.e. no edge in `U` leads in-to, or out-of `S`

Note that the semantics of a subgraph are by definition identical to the
semantics of its super-graph. The same therefore also applies to an empty
subgraph formed from another graph by removing all its vertices and edges.
And because the empty graph can be formed from any non-empty graph, the
semantics of the empty graph needs to be understood to correspond with
the semantics of any non-empty graph.

* `(S subgraph-of G) -> (sem(S) == sem(G))`

Similar to simple sets, a **strict/proper subgraph** is formed by removing
at least one vertex and/or edge - i.e. `(#T < #V)` and/or `(#U < #E)`. Any
graph `G` is therefore a (simple) subgraph, but no proper subgraph to itself.

<!-- ======================================================================= -->
## subgraph-of, strict-subgraph-of

A **subgraph-of** operator can be defined as follows:

* for two graphs `S := (T,U)` and `G := (V,E)`
* `(S subgraph-of G)` is true, if the following holds:
* (1) `(T subset-of V)` and `(U subset-of E)` are both true
* (2) `(E(e) subset-of T)` is true for any edge `(e in U)`
* (3) `(sem(S) == sem(G))` is true

Likewise, a **proper/strict-subgraph-of** operator can be defined:

* `(S strict-subgraph-of G)` is true, if the following holds:
* (4) `(S subgraph-of G)` is true
* (5) `(S != G)` is true
* synonymous - proper-subgraph-of

Note that, if condition (2) is not met, then `S` is not even a graph. Also,
and because (4) still needs to be satisfied, (5) can be simplified as
`(#T != #V) and/or (#U != #E)`. That is, the test for in-equality can be
reduced to a test of in-equality in regards to the numbers of elements in
the corresponding sets. Consequently, the sets of vertices and/or edges in
`S` must have fewer elements (i.e. `<` instead of `!=`) than the corresponding
set in `G`.

Note that the subgraph-of operator is as such still a removal-based operator.
That is, the corresponding test may still proof that one graph can be formed
by removing vertices and/or edges from the other.

<!-- ======================================================================= -->
## related-to, unrelated-to

Two graphs `S := (T,U)` and `G := (V,E)` are said to be **related** with
each other, if one is a subgraph of the other.

* `(S related-to G) := (S subgraph-of G) or (G subgraph-of S)`

Likewise, two graphs `S` and `G` are said to be **strictly related** with
each other, if both are related but not equal to each other. That is, one
is a proper subgraph of the other.

* `(S strictly-related-to G) := (S related-to G) and (S != G)`

Two graphs `S` and `G` are said to be **unrelated** with each other, if both
are not related to each other. That is, neither one of them is a subgraph of
the other.

* `(S unrelated-to G) := not (S related-to G)`

Note that no definition is possible for "strictly unrelated".

<!-- ======================================================================= -->
## induced subgraph (V)

An **induced subgraph** `S := (T,U)` is formed from another graph `G := (V,E)`
by removing some of its vertices. In addition to that, the subset of edges `U`
is formed based on the subset of vertices `T` by selecting all those edges
`(e in E)` whose endpoints are both in `T`.

* `S := G[T] := (T,U)` where `U := { (e in E) | (E(e) subset-of T) }`
* i.e. `U` contains all those edges in `E` whose endpoints are both in `T`
* i.e. `S` is a subgraph of `G`, induced by its vertex-subset `T`

Note that, in the context of relations, an induced subgraph represents a
restriction of its super-relation. That is, the corresponding sub-relation
is restricted to the given subset of vertices.

Note that there is in general no requirement or limitation as to how the subset
of vertices `T` is formed. That is, even the empty graph `Ø` is an induced
subgraph to any graph (i.e. `Ø := G[{}]`). Also, and because `T` may contain
vertices that are disconnected in `G`, an induced subgraph `S := (T,U)` is in
general not guaranteed to be connected.

Note that there is no freedom as to how the subset of edges `U` is formed.
That is, the subset of edges `U` can be understood as a consequence of the
subset of vertices `T`. Because of that, the term "induced" is understood as:
The resulting graph is formed "based on a given set of vertices", and "based
on a rule which allows to uniquely determine the edges in the resulting graph".

Note that a non-empty graph `S`, which is a subgraph of `G`, is also a subgraph
of the graph induced by the vertex-set of `G` (i.e. `G[V(G)]`). In general,
if `S` is a subgraph of an induced subgraph `G[X]` (i.e. induced by a subset
of vertices in `G`), then `S` is also subgraph of `G` itself. The converse
is not in general true because if `S` is a subgraph of `G`, then `S` is not
a subgraph to all possible induced subgraphs of `G`. However, at least one
such induced subgraph (i.e. `G[V(G)]`) always exists.

* `(S subgraph-of G) <- (S subgraph-of G[X])`
* `(S subgraph-of G) <-> (S subgraph-of G[V(G)])`
* `(S subgraph-of G) <-> (S subgraph-of G[V(S)])`

A **induced strict/proper subgraph** `S := (T,U)` is an induced subgraph formed
from another graph `G := (V,E)` by removing at least one vertex and/or edge.
(Note that `S` may also be referred to as a "strict/proper induced subgraph").

Note that the requirement of having fewer vertices and/or edges is in regards
to the resulting subgraph. That is, the subset of vertices used to form the
subgraph is itself (in principle) not required to have fewer elements than the
corresponding vertex set in the super-graph. (Note that this clarification is
in regards to the extension of the term "induced" to also work with subsets of
edges, see below).

Note that an induced proper subgraph may still have the same set of edges as
its super-graph - i.e. not necessarily `(#U < #E)`. That is because an induced
proper subgraph may be formed by removing only isolated vertices.

<!-- ======================================================================= -->
## induced-subgraph-of (V)

As before, an **induced-subgraph-of** operator can be defined as follows:

* for `S := G[T]` where `S := (T,U)` and `G := (V,E)`
* `(S induced-subgraph-of G)` is true, if the following holds:
* (1) `(S subgraph-of G)` is true
* (2) `(U == { (e in E) | (E(e) subset-of T) })` is true

Likewise, an **induced-proper/strict-subgraph-of** operator can be defined:

* `(S induced-proper-subgraph-of G)` is true, if the following holds:
* (3) `(S induced-subgraph-of G)` is true
* (4) `(S != G)` is true
* synonymous - strict/proper-induced-subgraph-of

Note that (4) can be simplified as `(#T < #V)`.

<!-- ======================================================================= -->
## induced subgraph (E)

The above definition of an induced subgraph `S` may be referred to as being
**induced by a subset of vertices** (i.e. `S := G[V]`) such that the vertex
set in `S` holds all those vertices in `V` that are also vertices in `V(G)`
(i.e. `V(S) == (V(G) & V)`). Consequently, the rule of the term "induced"
is to remove all those edges in `G` that have an endpoint not in `V(S)`.

* `S := G[V] := (T,U)` where `T := (V(G) & V)` and
* `U := { (e in E(G)) | (E(e) subset-of T) }`

Similar to that, an induced subgraph `S` can be formed based upon a subset of
edges `E` (i.e. `S := G[E]`): An induced subgraph, **induced by a subset of
edges** `E`, is a subgraph of `G` such that the set of edges in `S` holds all
those edges in `E` that are also edges in `E(G)` (i.e. `E(S) == (E(G) & E)`).
Consequently, the rule that is used to form the subgraph is to remove all
those vertices in `G` that are no endpoint to any edge in `E(S)`.

* `S := G[E] := (T,U)` where `U := (E(G) & E)` and
* `T := { (v in V(G)) | (v endpoint-of e) for some (e in U) }`

Note that `G[E]` can not have any disconnected vertices. Hence, `G[E(G)]`
may be used to refer to the maximal subgraph of `G` that has no disconnected
vertices. Note however that `G[E]` may itself still be disconnected as it may
have more than one maximal component with two or more vertices.

Note that the vertex set `V(S)` in `S := G[T]` is not necessarily equal to `T`.
Likewise, the edge set `E(S)` is not necessarily equal to `E` in `S := G[E]`.
In general both sets are expected to be equivalent because the input sets are
in general assumed to be reduced to the corresponding elements in `G` (i.e.
only elements that exist in `G`).
