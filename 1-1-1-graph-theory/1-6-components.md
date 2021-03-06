
<!-- ======================================================================= -->
# (connected) components

A **(connected) component** `c := G[T] := (T,U)` of a graph `G := (V,E)`
is an induced subgraph such that each vertex `(x in T)` is connected with
every other vertex `(y in T)` in the graph's underlying undirected graph
`UG := UG(G) := (V,A)`. That is, `UG` contains an undirected path `p` for
all pairs of vertices `(x,y in T)` - i.e. `(p(x,y) in P[UG])`.

The **diameter** of a component `c := (T,U)` is the edge-length of the
longest path in it. That is, `diameter(c) := max({ #p | (p in P[c]) })`.
Note that the diameter of a cyclic component is undefined/infinite.

A **maximal (connected) component** `c := (T,U)` is a component of a graph
`G := (V,E)` such that no vertex `(y in V\T)` can be added to its set of
vertices `T` while maintaining its connectivity. That is, no vertex
`(y in V\T)` exists that is connected to some `(y in T)`. Consequently,
the induced subgraphs `G[T + {y}]` are no components in `G`.

A maximal component of the form `c := ({v},{})` will be referred to as a
(maximal) **trivial component**. Because of that, each disconnected vertex
represents its own maximal component.

Any component `c := (T,U)` in `G := (V,E)` is said to be **connected**. In
addition to that, a component in `G` is said to be **strongly connected** (i.e.
a strongly connected component), if all pairs of vertices `(x,y in U)` in it
are connected in both directions - i.e. `(xPy and yPx)`. (Because of that, any
component in an undirected graph is strongly connected). In contrary to that,
a component is said to be **simply/weakly connected**, if a pair of vertices
`(x,y in U)` exists such that `xPy`, but not `yPx` - i.e. `(xPy ex-or yPx)`
is true for some vertices. Because of that, each connected component is also
weakly connected, but not necessarily strongly connected.

Note that ...

* The term "component" will in general refer to a maximal component.
* Each vertex in a graph belongs to exactly one maximal component.
* i.e. the (maximal) components in a graph are **disjoint**
* Components in an oriented, acyclic graph are weakly connected.
* Components in an oriented, cyclic graph may be strongly connected.
* e.g. a cycle graph is strongly connected

<!-- ======================================================================= -->
## the set of (maximal) components

A non-empty graph `G := (V,E)` has in general more than one maximal component.
That is because, depending on the graph's set of edges `E`, a maximal component
`c := G[T]` may be limited to a proper subset of `V`. Hence, further maximal
components will be induced by subsets of `V\T`.

Any graph can therefore be understood as a **union of disjoint (maximal)
components**. That is, as a set of (maximal) components `C`. Similar to
the set of all possible paths `P`, each graph can therefore be understood
to have a set of components `C` associated with it.

Note that, similar to `P(G)`, the set of components `C` of a given graph
`G` can be clarified as `C(G)`.

<!-- ======================================================================= -->
## connected graphs

Depending on the number of components in a graph's set of components `C`,
a non-empty graph `G` may be classified as being ...

* **connected**, if `(#C == 1)` - i.e. `(C(G) == {c})`
* i.e. a connected graph has one and only one maximal component
* **strongly connected**, if `G` is connected and `c` is strongly connected
* **weakly connected**, if `G` is connected and `c` is weakly connected
* **disconnected**, if `(#C > 1)` - i.e. `(C[G] == { c1, ..., ck })`
* i.e. a disconnected graph has more than one maximal component

Note that a null-graph may be referred to as being connected. That is because
it has no maximal component and therefore also no other maximal component
that could "disconnect" the graph - i.e. a null-graph is understood to have
no characteristic that could be in conflict with its connectivity.
