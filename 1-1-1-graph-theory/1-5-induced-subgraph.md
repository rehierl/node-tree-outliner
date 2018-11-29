
<!-- ======================================================================= -->
# Induced subgraphs

There are two methods that can be used to form an induced subgraph: (V) based
on a given subset of vertices, and (E) based on a given subset of edges.

<!-- ======================================================================= -->
## induced subgraph (V)

By default, an **induced subgraph** `S := G[X] := (T,U)` is formed from another
graph `G := (V,E)` by removing some of its vertices. In addition to that, the
subset of edges `U` is formed by removing all those edges in `E` that have an
endpoint not in `T` (i.e. the implicit removal of incident edges). As such, an
induced subgraph contains all those edges that have both of their endpoints in
`T`.

* `(T subset-of V)` where `T := (V & X)`
* `U := { (e in E) | (E(e) subset-of T) }`
* i.e. `U` contains all the edges in `E` whose endpoints are both in `T`

Note that there is no freedom when forming the subset of edges `U`. That is,
the subset of edges `U` can be understood as a direct consequence of the
subset of vertices `T`. Because of that, the term "induced" is understood as:
The resulting graph is formed "based on a given set of vertices", and "based
on a rule which allows to uniquely determine the edges in the induced graph".

<!-- ======================================================================= -->
## remarks

() Note that, in the context of (binary) relations, an induced subgraph is a
restriction of its super-relation. That is, the corresponding sub-relation
is restricted to the given subset of vertices.

() Note that any induced subgraph `S := (T,U)` of a graph `G := (V,E)` is by
the definition of the "subgraph-of" operator also a subgraph of `G`. However,
an arbitrary subgraph of a graph is not necessarily also an induced subgraph
since an arbitrary subgraph may be formed by also removing one or more edges
that have both of their endpoints in `T`.

* `(S induced-subgraph-of G) -> (S subgraph-of G)`

() Note that a non-empty subgraph graph `S` of graph `G` is a subgraph of the
graph induced by the set of vertices `V` (i.e. `(S subgraph-of G[V]`). That is,
if `S` is a subgraph of an induced subgraph `G[X]`, then `S` is also a subgraph
of `G`. However, if `S` is a subgraph of `G`, then `S` is not necessarily also
a subgraph of any induced subgraph of `G`, even though at least one such
induced subgraph (i.e. `G[V]`) always exists.

* `(S subgraph-of G[X]) -> (S subgraph-of G)`
* `(S subgraph-of G) <-> (S subgraph-of G[V])`
* `(S subgraph-of G) <-> (S subgraph-of G[T])`
* note - `(G[V] == G[T])` may be true

<!-- ======================================================================= -->
## induced subgraph (V+E)

The induced subgraph `S := (T,U)` of graph `G := (V,E)` may be referred to as
being **induced by a subset of vertices** (i.e. `S := G[X]`). As such, the set
of vertices `T` contains all those vertices in `X` that are also vertices in `V`
(i.e. `T := (V & X)`). Because of that, `S` is formed by removing all vertices
in `G` that are not in `X`, including the implicit removal of any incident edge.

* `S := G[X] := (T,U)` where `T := (V & X)` and
* `U := { (e in E) | (E(e) subset-of T) }`
* note - `(G[X] subgraph-of G)` is true

Similar to that, an induced subgraph `S := (T,U)` of graph `G := (V,E)` may
be referred to as being **induced by a subset of edges** (i.e. `S := G[Y]`).
As such the set of edges in `U` contains all those edges in `Y` that are also
edges in `E` (i.e. `U == (E & Y)`). Consequently, the rule used to form such
a subgraph is to remove all those vertices in `G` that are no endpoint to any
edge in `U`.

* `S := G[Y] := (T,U)` where `U := (E & Y)` and
* `T := { (v in V) | (v endpoint-of e) for some (e in U) }`
* note - `(G[Y] subgraph-of G)` is true

An **induced strict/proper subgraph** `S := (T,U)` is an induced subgraph of
graph `G := (V,E)`, if it was formed by removing at least one vertex and/or
edge. (Note that `S` may be referred to as a "strict/proper induced subgraph").

Note that the requirement of having fewer vertices and/or edges is in regards
to the resulting subgraph. That is, the subset of vertices or edges used to
form an induced subgraph is itself not required to have fewer elements than
the corresponding set in the super-graph.

<!-- ======================================================================= -->
## remarks

() Note that an induced subgraph may be clarified as being "induced by a subset
of vertices" (i.e. `G[T]`, `G[V]` or `G[X]`), or as being "induced by a subset
of edges" (i.e. `G[U]`, `G[E]` or `G[Y]`). In addition to that, `G[T]` and
`G[U]` are used to express that the induced subgraph is formed by some subset,
which may or may not be equal to the corresponding set in `G`. In contrary to
that, `G[V]` and `G[E]` are used to express that the induced subgraph is formed
by the corresponding complete set in `G`.

() Note that the set of vertices `X` in `G[X]` is not strictly required to be
equal to `T`. Likewise, the set of edges `Y` in `G[Y]` is not strictly required
to be equal to `U`. However, the input sets (i.e. `X` and `Y`) are in general
expected to be subsets of the corresponding set in `G` and therefore expected
to be equal to the corresponding set in `S`. That is, `(T == (V & X))` and
`(U == (E & Y))` are in general both expected to be true.

() Note that there is in general no requirement or limitation as to how the
input set of vertices or edges is formed. That is, the empty graph `Ø` can be
seen as an induced subgraph of another graph (i.e. `Ø := G[{}]`), induced by
an empty set of vertices, or induced by an empty set of edges.

() Note that a non-empty subgraph `S` of graph `G` is a subgraph of the graph
induced by the set of edges in `G` (i.e. `(S subgraph-of G[E])`). That is, if
`S` is a subgraph of an induced subgraph `G[Y]`, then `S` is also a subgraph of
`G`. However, if `S` is a subgraph of `G`, then `S` is not necessarily also a
subgraph to any induced subgraph of `G`, even though at least one such induced
subgraph (i.e. `G[E]`) always exists.

* `(S subgraph-of G[Y]) -> (S subgraph-of G)`
* `(S subgraph-of G) <-> (S subgraph-of G[E])`
* `(S subgraph-of G) <-> (S subgraph-of G[U])`
* note - `(G[E] == G[U])` may be true

<!-- ======================================================================= -->
## induced-subgraph-of

Given the two graphs `S := (T,U)` and `G := (V,E)`,
an **induced-subgraph-of** operator can be defined:

* `(S induced-subgraph-of G)` is true, if ...
* (1) `(S subgraph-of G)` is true
* (2.1) `(U == { (e in E) | (E(e) subset-of T) })` is true
* (2.2) `(T == { (v in V) | (v endpoint-of e) for some (e in U) })` is true
* synonymous - "i-subgraph-of"

An **induced-proper/strict-subgraph-of** operator can be defined:

* `(S induced-proper-subgraph-of G)` is true, if ...
* (3) `(S induced-subgraph-of G)` is true
* (4) `(S != G)` is true
* synonymous - "ip-subgraph-of"

Note that only condition (2.1) or (2.2) needs to be satisfied. However, if the
vertex set `T` does not contain any disconnected vertices, then both conditions
may be satisfied at the same time. Despite that, `S` may still not be connected.

<!-- ======================================================================= -->
## remarks

() Note that `(G[V] == G)` is true.

() Note that `G[T]` may have disconnected vertices.
Consequently, `G[T]` is not necessarily connected.

() Note that an induced proper subgraph `S := G[T]` (i.e. `(#T < #V)`) may have
the same set of edges as in `G` (i.e. `(U == E)`). That is because an induced
proper subgraph may be formed by removing only disconnected vertices. If in
contrary to that, one or more connected vertices are removed, then `(#U < #E)`
is true since `U` is then, due to the implicit removal of incident edges, a
proper subset of `E`.

* `(S == G[T]) -> (#U <= #E)`, if `(#T < #V)`
* `(S == G[T]) -> (#U == #E)`, if `(#T == #V)`
* i.e. `(G[T] proper-subgraph-of G) -> (#T < #V)`

() Note that `(G[E] == G)` is not necessarily true
since `G` may have disconnected vertices.

() Note that `G[U]` can not have disconnected vertices. Despite that, `G[U]`
is still not necessarily connected since it may consist of components that all
have two or more vertices. Hence, `(G[E] == G)` may be used as a requirement
to only express that `G` must not have disconnected vertices.

() Note that an induced proper subgraph `S := G[U]` (i.e. `(#U < #E)`) may have
the same set of vertices as `G` (i.e. `(T == V)`). That is because all vertices
in `G` may be incident to more than one edge. Likewise, `S` may be a proper
subgraph of `G`, if the entire set of edges `E` is used to induce `S`. That is
because `G` may have disconnected vertices.

* `(S == G[U]) -> (#T <= #V)`, if `(#U < #E)`
* `(S == G[U]) -> (#T <= #V)`, if `(#U == #E)`
* i.e. `(G[U] proper-subgraph-of G) =!> (#U < #E)`
