
<!-- ======================================================================= -->
# Binary operations on graphs

* removal-based binary operations
* i.e. graph difference, symmetric difference

<!-- ======================================================================= -->
## options to define the graph difference (\)

The definition of the graph-difference operation `T := (G \ S)` needs to define
which elements in `S` to remove from `G`. That is because, in contrary to simple
sets of elements, graphs contain elements/vertices and their relationships/edges
rather than a single type of elements.

Note that the definition of the set-difference `C := (A \ B)` is based upon
the removal of elements. That is, `C` is formed by removing all the elements
in `B` from `A`. Because of that, `(A \ B)` is a subset of `A`.

### option-0, Remove nothing at all

Removing no vertices and no edges at all has obviously no effect on `G`. That
is because the operation will then have to return `G` as `T` (i.e. without any
modification). Obviously, that option does not cover the intention behind this
operation.

### option-1, Remove all the edges in S

This option is intended to remove all the edges in `S` from the edges in `G`,
while maintaining the vertices in `G`.

Recall that the endpoints of an edge in a graph must both be vertices in the
graph's set of vertices. Because of that, an edge in `S` can only be removed
from `G`, if `G` contains the corresponding edge and both of its endpoints.

Example 1: The graph difference `T := (G \ S)` of `G := ({1,2},{(1,2),(2,1)})`
and `S := ({1,2},{(1,2)})` under that option is `T := ({1,2},{(2,1)})`.

Example 2: The graph difference `T := (G \ S)` of `G := ({1,2},{(1,2)})` and
`S := ({1,2},{(1,2)})` under that option is `T := ({1,2},{})`. That is, the
resulting graph is a graph of disconnected vertices.

Note that the complement graph `G*` is defined based upon the removal of edges:
`G* := (K(G) \ G)`. That is, all edges in `G` need to be removed from its
induced complete graph `K(G)`. The disadvantage of this option is that the
complement graph of a complete graph is, in contrary to the empty complement of
the universal set of elements, an edgeless graph of vertices.

### option-2, Remove all the vertices in S

This option is intended to remove all the vertices in `S` from the set of
vertices in `G`, while maintaining the set of edges in `G`.

Recall that the endpoints of any edge `e` in a graph `G := (V,E)` must both
be elements in `V` (i.e. `(E(e) subset-of V)`). Because of that, and if a
vertex `(v in V)` would have to be removed, then any edge `(e in E)` incident
to `v`, must also be implicitly removed. That is, because the result of such
an operation would otherwise not be a graph. Consequently, the removal of all
vertices in `S` also results in the implicit removal of any edge that are
incident to a removed vertex.

Example: The graph difference `T := (G \ S)` of `G := ({1,2,3},{(1,2),(2,3)})`
and `S := ({1},{})` under that option is `T := ({2,3},{(2,3)})`.

Note that even edges, which are no edges in `S`, may have to be removed.

### option-3, Remove all the vertices and all the edges in S

Because once all the vertices in `S` have been removed from `G` (including the
implicit removal of any incident edge), no edge in `G` remains that could still
be an edge in `S`. Because of that, the subsequent removal of all the edges in
`S` from `G` will no longer have any effect. The removal of all the vertices in
`S` will therefore also implicitly remove all the edges in `S`. This option is
consequently equivalent to option-2.

Example: The graph difference `T := (G \ S)` of `G := ({1,2,3},{(1,2),(2,3)})`
and `S := ({1,2},{(1,2)})` under that option is `T := ({3},{})`.

<!-- ======================================================================= -->
## difference (\, sub, diff)

Due to the above, there are only two options available that allow to define
the difference between two graphs. Because of that, option-1 will be referred
to as the **edge-based**, and option-2 as the **vertex-based** definition.

The difference graph of the difference graph `(G \ G)` under the edge-based
definition is an edgeless graph of vertices (i.e. one component per vertex).
In contrary to that, the difference graph `(G \ G)` under the vertex-based
definition is the empty graph `Ø`. Because of that, the vertex-based definition
is more suited for the definition of the relationship between a graph and its
subgraphs as it is more consistent compared with the difference between simple
sets of elements.

* `(G diff S) := (V,E)` where
* `V := (V(G) \ V(S))` and `E := { (x,y) in E(G) | (x,y !in V(S)) }`
* `(G \ S), (G - S), (G sub S) := (G diff S)`
* i.e. **the vertex-based definition**

Note that ...

* `((G \ Ø) == G)` and `((G \ G) == Ø)`
* `((G \ S) disjoint-to S)`
* `((G \ S) subgraph-of G)`

Note that `(G \ S)` can be also defined as an induced subgraph of `G`:

* `(G diff S) := G[V(G) \ V(S)]`

In `T := (G \ S)`, `S` is not required to be a subgraph of `G`. Likewise, `S`
may not overlap `G`, or both graphs may even be disjoint from one another.
However, in the context of this discussion, the intersection between `S` and
`G` is assumed to be non-empty. Furthermore, `S` is assumed to be reduced to
that intersection, which is why `S` is assumed to have no elements (vertices
and/or edges) outside of `G`. That is, `S` is in general expected to be a
non-empty subgraph of `G`.

* `S` is stripped of any elements not in `G`
* i.e. `S := (G & S)`, i.e. `(S subgraph-of G)`

<!-- ======================================================================= -->
## symmetric difference (^, xor, ex-or)

With the above vertex-based definition, the symmetric difference between two
graphs can be defined "similar" to the symmetric difference between two simple
sets of elements.

* `(G ex-or S) := (G \ S) + (S \ G)`
* `(G ^ S), (G xor S) := (G ex-or S)`

**TODO** - any application/use?
