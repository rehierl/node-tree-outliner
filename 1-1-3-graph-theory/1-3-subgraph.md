
<!-- ======================================================================= -->
# Subgraphs

Note that the vertex `(v in V)` of a graph `G := (V,E,P)` is **connected**,
if `vPx` and/or `xPv` is true for some `(x in V)`. In addition to that, vertex
`v` is said to be **connected with** vertex `x`.

Note that a vertex `(v in V)` may exist such that neither `vEx` nor `xEv` is
true for any vertex `(x in V)`. That is, a graph may contain vertices that
are no endpoint to any edge `(e in E)`. These kind of vertices may in general
be referred to as being **isolated/disconnected**.

<!-- ======================================================================= -->
## (induced) subgraph

A (simple) **subgraph** `S := (T,U)` is a graph derived from another graph
`G := (V,E)` by removing some of its vertices and/or edges.

* `(T subset-of V)` and `(U subset-of E)`
* `T` must include both endpoints of all the edges in `U`
* i.e. `(E(e) subset-of T)` for all `(e in U)`
* i.e. `U` contains some of the edges in `E`
* i.e. no edge in `U` leads in-to, or out-of `S`
* `S` is not necessarily connected
* i.e. `T` hay have isolated vertices
* `(S sub-graph-of G) <-> (G super-graph-of S)`

Similar to simple sets, a **strict/proper subgraph** is formed by removing
at least one vertex and/or edge - i.e. `(#T < #V)` and/or `(#U < #E)`. That
is, any graph `G` is a (simple) subgraph, but no proper subgraph to itself.

An **induced subgraph** `S := (T,U)` is formed from another graph `G := (V,E)`
by removing some of its vertices. In addition to that, the edge-subset `U` is
formed based on the vertex-subset `T` by selecting all those edges `(e in E)`
whose endpoints are both in `T`.

* `S := G[T] := (T,U)` where `U := { (e in E) | (E(e) subset-of T) }`
* i.e. `U` contains all those edges in `E` whose endpoints are both in `T`
* i.e. `S` is a subgraph of `G`, induced by its vertex-subset `T`

Note that there is no degree of freedom as to how the edge-subset `U` is
formed. That is, the edge-subset `U` is a consequence of the vertex-subset
`T`.

Note that there is in general no requirement or limitation as to how the
vertex-subset `T` is formed. Because of that, an induced subgraph is not
guaranteed to be connected. That is, `S` is a disjoint union of connected
components.

A **strict/proper induced subgraph** `S` is an induced subgraph formed from
another graph `G` by removing at least one vertex - i.e. `(#T < #V)`.

Note that a proper induced subgraph may still have the same edge-subset as
its super-graph - i.e. not necessarily `(#U < #E)`. That is because a proper
induced subgraph may be formed by removing only isolated vertices from its
super-graph.

<!-- ======================================================================= -->
## (connected) components

A **(connected) component** `c` of a graph `G := (V,E)` is an induced
subgraph `c := G[T] := (T,U)` such that each vertex `(x in T)` is connected
with all other vertices `(y in T)` in the graph's underlying undirected graph
`H := (V,F) := H(G)`. That is, a component contains an undirected path `p`
for any pair of vertices `(x,y in T)` - i.e. `(p(x,y) in P[H])`.

The **diameter** of a component `c := (T,U)` is the vertex-length of the
longest path in `c`. That is, `diameter(c) := max({ #p | (p in P[U]) })`.
Note that the diameter of a cyclic component is undefined/infinite.

Note that a component of the form `c := ({v},{})` represents a **trivial
component**. That is, each isolated/disconnected vertex can be understood
to represent a (maximal) trivial component.

A **maximal (connected) component** `c := (T,U)` is a component of a graph
`G := (V,E)` such that no vertex `(v in V\T)` can be added to its set of
vertices `T` while maintaining its connectivity. That is, no other induced
subgraph `G[T + {v}]` is a component of `G`.

Any component `c := (T,U)` is obviously referred to as being **connected**. In
addition to that, a component may be referred to as being **strongly connected**
(i.e. a strongly connected component), if any pair of vertices `(x,y in U)`
is connected in both directions - i.e. `(xUy and yUx)`. (Because of that, any
component of an undirected graph is strongly connected). In contrary to that,
a component is said to be **simply/weakly connected**, if a pair of vertices
exists such that `xUy`, but not `yUx` - i.e. `(xUy ex-or yUx)`.

<!-- ======================================================================= -->
## set of (maximal) components C

A non-empty graph `G := (V,E)` has in general more than one maximal component.
That is because, depending on the graph's set of edges `E`, a maximal component
`c := G[T]` may be restricted to a proper subset of `V`. Because of that,
further maximal components will be induced by subsets of `V\T`.

Note that each vertex in a graph belongs to exactly one maximal component.

Any graph can therefore be understood as a **set of disjoint (maximal)
components** `C`. That is, any graph is the disjoint union of its maximal
components. Hence, and similar to the set of all possible paths `P`,
each graph can be understood to be associated with its set of (maximal)
components `C`.

Note that the term "component" will in general refer to a maximal component.

<!-- ======================================================================= -->
## connected graphs

Depending on the number of components in a graph's set of components `C`,
a non-empty graph `G` may be classified as:

* connected, if `(#C == 1)` - i.e. `(C[G] == {c})`
* strongly connected, if `G` is connected and if `c` is strongly connected
* weakly connected, if `G` is connected and if `c` is weakly connected
* disconnected, if `(#C > 1)` - i.e. `(C[G] == { c1, ..., ck })`
