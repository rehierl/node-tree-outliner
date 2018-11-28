
<!-- ======================================================================= -->
# Induced subgraphs

There are two methods to form an induced subgraph:
(V) based on a given subset of vertices,
or (E) based on a given subset of edges.

<!-- ======================================================================= -->
## induced subgraph (V)

By default, an **induced subgraph** `S := G[X] := (T,U)` is formed from another
graph `G := (V,E)` by removing some of its vertices. In addition to that, the
subset of edges `U` is formed by removing all those edges in `E` that have an
endpoint not in `T` (i.e. the implicit removal of incident edges).

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
the definition of the "subgraph-of" operator also a subgraph of `G`. In contrary
to that, an arbitrary subgraph of a graph is not necessarily also an induced
subgraph. That is because an arbitrary subgraph may be formed by removing one
or more edges that have both of their endpoints in `T`.

() Note that a non-empty graph `S`, which is a subgraph of `G`, is a subgraph
of the graph induced by the set of vertices in `G` (i.e. `(S subgraph-of G[V]`).
That is, if `S` is a subgraph of an induced subgraph `G[X]`, then `S` is also
a subgraph of `G` itself. The converse is in general not true because if `S` is
a subgraph of `G`, then `S` is not necessarily also a subgraph to any induced
subgraph of `G`. However, at least one such induced subgraph (i.e. `G[V]`)
always exists.

* `(S subgraph-of G[X]) -> (S subgraph-of G)`
* `(S subgraph-of G) <-> (S subgraph-of G[V])`
* `(S subgraph-of G) <-> (S subgraph-of G[T])`
* note - `(G[V] == G[T])` may be true

<!-- ======================================================================= -->
## induced subgraph (V+E)

The induced subgraph `S := (T,U)` of a graph `G := (V,E)` may be referred to as
being **induced by a subset of vertices** (i.e. `S := G[X]`). As such, the set
of vertices `T` contains all those vertices in `X` that are also vertices in `V`
(i.e. `T := (V & X)`). Because of that, `S` is formed by removing all vertices
in `G` that are not in `X`, including the implicit removal of any incident edge.

* `S := G[X] := (T,U)` where `T := (V & X)` and
* `U := { (e in E) | (E(e) subset-of T) }`
* note - `(G[X] subgraph-of G)` is true

Similar to that, an induced subgraph `S := (T,U)` of a graph `G := (V,E)` may
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
edge. (`S` may also be referred to as a "strict/proper induced subgraph").

Note that the requirement of having fewer vertices and/or edges is in regards
to the resulting subgraph. That is, the subset of vertices or edges used to
form an induced subgraph is itself not required to have fewer elements than
the corresponding set in the super-graph.

<!-- ======================================================================= -->
## remarks

() Note that an induced subgraph may be clarified as being "induced by a
subset of vertices" (i.e. `G[V]` or `G[X]`), or as being "induced by a subset
of edges" (i.e. `G[E]` or `G[Y]`).

() Note that the set of vertices `X` in `G[X]` is not strictly required to be
equal to `T`. Likewise, the set of edges `Y` in `G[Y]` is not strictly required
to be equal to `U`. However, the input set (i.e. `X` or `Y`) is in general
expected to be a subset of the corresponding set in `G` and therefore expected
to be equal to the corresponding set in `S`. That is, `(T == (V & X))` and/or
`(U == (E & Y))` are in general expected to be true.

() Note that there is in general no requirement or limitation as to how the
input set of vertices or edges is formed. That is, the empty graph `Ø` can be
seen as an induced subgraph of another graph (i.e. `Ø := G[{}]`), induced by
an empty set of vertices, or induced by an empty set of edges.

() Note that a non-empty graph `S`, which is a subgraph of `G`, is a subgraph
of the graph induced by the set of edges in `G` (i.e. `(S subgraph-of G[E])`).
That is, if `S` is a subgraph of an induced subgraph `G[Y]`, then `S` is also
a subgraph of `G` itself. The converse is in general not true because if `S` is
a subgraph of `G`, then `S` is not necessarily also a subgraph to any induced
subgraph of `G`. However, at least one such induced subgraph (i.e. `G[E]`)
always exists.

* `(S subgraph-of G[Y]) -> (S subgraph-of G)`
* `(S subgraph-of G) <-> (S subgraph-of G[E])`
* `(S subgraph-of G) <-> (S subgraph-of G[U])`
* note - `(G[E] == G[U])` may be true

<!-- ======================================================================= -->
## induced-subgraph-of

An **induced-subgraph-of** operator can be defined:

* `(S induced-subgraph-of G)` is true, if ...
* for `S := (T,U)` and `G := (V,E)`
* (1) `(S subgraph-of G)` is true
* (2.1) `(U == { (e in E) | (E(e) subset-of T) })` is true
* (2.2) `(T == { (v in V) | (v endpoint-of e) for some (e in U) })` is true
* synonymous - "i-subgraph-of"

An **induced-proper/strict-subgraph-of** operator can be defined:

* `(S induced-proper-subgraph-of G)` is true, if ...
* (3) `(S induced-subgraph-of G)` is true
* (4) `(S != G)` is true
* synonymous - "ip-subgraph-of"

Note that only of the conditions (i.e. (2.1) or (2.2)) needs to be satisfied.

<!-- ======================================================================= -->
## remarks (V)

() Note that `G[T]` may have disconnected vertices since `T` may contain
vertices that are disconnected in `G`. Because of that, `G[T]` itself is
not necessarily connected.

() Note that `(G[V] == G)` is always true.

<!-- ======================================================================= -->
## remarks (E)

() Note that `G[E]` can not have disconnected vertices. (Hence, `G[E]` may be
used to refer to the maximal subgraph of `G` that has no disconnected vertices).
Note however that `G[E]` itself is still not necessarily connected since it may
consist only of maximal components that have two or more vertices.

() Note that `G[E]` is not necessarily equal to `G` (i.e. `G[E] <=!=> G`).
That is because `G` may have disconnected vertices. That is, `(G[E] == G)`
is true if (and only if) `G` has no disconnected vertices.

<!-- ======================================================================= -->
## remarks

() Note that an induced proper subgraph `S := G[X]` may still have the same set
of edges as `G` (i.e. `(U == E)`). That is because an induced proper subgraph
may be formed by removing only disconnected vertices. If in contrary to that,
one or more connected vertices are removed, then `(#U < #E)` is true since `U`
is then a proper subset of `E`.

* `(S == G[X]) -> (#U <= #E)`

**TODO** - explain this -
Note that (4) can be simplified as `(#T < #V)`.

* `(S i-subgraph-of G) -> (S subgraph-of G)`
* `(S i-subgraph-of G) -> (#T <= #V) and (#U <= #E)`

* `(S proper-subgraph-of G) := (S subgraph-of G) and (S != G)`
* `(S proper-subgraph-of G) -> (#T < #V) and/or (#U < #E)`

Note that ...

* `(S i-subgraph-of G) -> (T subset-of V) and (U subset-of E)`
* `(S i-subgraph-of G) -> (#T <= #V) and (#U <= #E)`
