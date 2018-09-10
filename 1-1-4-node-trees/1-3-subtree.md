
<!-- ======================================================================= -->
# (strict/proper) Subtree

* (/see/ "hierarchy of sets" /)

<!-- ======================================================================= -->
## (induced) subgraph

A **subgraph** `S := (T,U)` is a graph derived from another graph `G := (V,E)`
by removing some of its vertices and/or edges.

* `(T subset-of V)` and `(U subset-of E)`
* `T` must include both endpoints of all the edges in `U`
* i.e. `(E(e) subset-of T)` for all `(e in U)`
* i.e. `U` contains some of the edges in `E`
* i.e. no edge in `U` leads in-to, or out-of `S`
* `S` is not necessarily connected
* i.e. `T` hay have isolated vertices
* `(S sub-graph-of G) <-> (G super-graph-of S)`

Similar to simple sets, a **strict/proper subgraph** is formed by removing at
least one vertex and/or edge - i.e. `(#T < #V)` and/or `(#U < #E)`. That is,
any graph `G` is a (simple) subgraph, but no proper subgraph to itself.

An **induced subgraph** `S := (T,U)` is formed from another graph `G := (V,E)`
by removing some of its vertices. In addition to that, the edge-subset `U` is
formed based on the vertex-subset `T` by selecting all those edges `(e in E)`
whose endpoints are both in `T`.

* `S := G[T] := (T,U)` where `U := { (e in E) | (E(e) subset-of T) }`
* i.e. `U` contains all those edges in `E` whose endpoints are both in `T`
* i.e. `S` is a subgraph of `G`, induced by its vertex-subset `T`

Note that there is no degree of freedom as to how the edge-subset `U` is
formed. That is, the edge-subset is always a direct consequence of the
vertex-subset `T`.

Note that there is in general no requirement or limitation as to how the
vertex-subset `T` is formed. Because of that, an induced subgraph is not
guaranteed to be connected. That is, `S` is a disjoint union of connected
components.

A **strict/proper induced subgraph** `S` is an induced subgraph formed from
another graph `G` by removing at least one vertex - i.e. `(#T < #V)`.

Note that a proper induced subgraph may still have the same edge subset as its
super-graph - i.e. not necessarily `(#U < #E)`. That is because a proper induced
subgraph may be formed by removing only isolated vertices from its super-graph.

<!-- ======================================================================= -->
## (induced) subtree

A **subtree** `S := (T,U)` is a subgraph of a graph `G := (V,E)`
such that `S` is a tree.

* `(S subgraph-of G)` must be true
* `isTree(S)` must be true

Note that `G` is not required to be a tree. Hence, the focus of this definition
is on the characteristic of the subgraph. In addition to that, `S` may or may
not satisfy further restrictions.

Note that a subtree is commonly defined as: "A connected subgraph of a tree".
That is, this definition requires `G` to be a tree. As a consequence of that
requirement, `S` is guaranteed to be a tree. That is because any connected
subgraph of a tree is by consequence automatically a tree. Because of that,
the common definition is more specific and the above definition more general.

As above, a **strict/proper subtree** is formed by removing at least one node
and/or edge - i.e. `(#T < #V)` and/or `(#U < #E)`. That is, any tree `G` is a
(simple) subtree, but no proper subtree to itself.

An **induced subtree** `S := (T,U)` is an induced subgraph of a graph
`G := (V,E)` such that `S` is a tree.

* `S := G[T] := (T,U)` such that `isTree(S)` is true

A **strict/proper induced subtree** `S` is an induced subtree formed from
another graph `G` by removing at least one vertex - i.e. `(#T < #V)`.

Note that the super-graph of a proper induced subtree is not necessarily
a tree (e.g. a subtree in a forest of trees). 

Note that a proper induced subtree, formed from another tree, will always have
fewer edges than its super-tree - i.e. `(#U < #E)`. That is because any tree
consists of a single connected component.

<!-- ======================================================================= -->
## inner/outer set of a node

The set of inner nodes `IN(n)` of node `n` in a tree `T` may be referred to as
**the inner set of a node** `IS(n)`. In contrary to that, the union of a node
with its inner set will be referred to as **the outer set of a node** `OS(n)`.

* `IS(n) := IN(n) := D(n)`
* `OS(n) := (IS(n) union {n})`
* i.e. `OS(n) <=!=> ON(n)`

Note that `n` will be referred to as **the defining node** of its inner and
its outer set. That is, both sets are defined as: "All the nodes that can be
reached beginning with, and including (or excluding) the defining node".

`IS(n)` and `OS(n)` only differ in the defining node `n`. Because of that, the
inner set of a node is a strict subset to its outer set. In addition to that,
the outer set of a descendant is a strict subset to the outer sets of its
ancestors.

* `(#IS(n)+1 == #OS(n))`
* `(IS(n) strict-subset-of OS(n))`

Note that the outer sets of siblings are disjoint. That is because no descendant
of a node is also a descendant of one of the node's siblings. Because of that,
the inner set of a node is the disjoint union of the outer sets of its child
nodes.

* `S := { OS(n) | (n in N) }`, i.e. `(#S == #N)`
* i.e. the set of outer sets in a tree, one for each node
* for any pair of sets `(s,t in S)` the following applies:
* if `(s != t)`, then `(s disjoint-to t) ex-or (s strictly-related-to t)`
* i.e. `(s overlaps t)` is `false` for any pair in `S`

Note that, if a parent has one child only, then the parent's inner set is
identical to the outer set of its only child.

<!-- ======================================================================= -->
## subtree of a tree

Obviously, there are several ways to form a subtree `S` from a given tree `T`.
However, any non-empty subtree will effectively always have a root node `r`.
That is, any node in `S` will have a unique rooted path that begins in the
subtree's root. Other than that, a subtree is not required to contain all
the descendants of `r` in `T`. That is, `S` may have different leaf nodes.

That is, a subtree is in general defined by its root and its leaf nodes.

Note that, in the context of this discussion, the super-graph of a sub-tree
is in general assumed to be an arborescence and any sub-tree is assumed to
be a non-empty induced subtree of such a super-tree.

once the first node of a subtree is selected, all other nodes must
be reachable from that node.

<!-- ======================================================================= -->
## TODO

* an induced subtree is induced by the subtree's root
* only one edge that leads into the subtree
* no edge that leads out of the subtree

--

* can an induced subtree be formed from a non-tree graph?
* yes, if isolated vertices are excluded

however, since an induced subtree is based on a connected component, the
super-graph must contain the subtree as is. that is, an induced subtree
is formed by cutting away the exterior - i.e. what is outside of it.
