
<!-- ======================================================================= -->
# (Strict) Subtree

* (/see/ "hierarchy of sets" /)

<!-- ======================================================================= -->
## (induced) subgraph

A **subgraph** `S := (T,U)` is a graph derived from another graph `G := (V,E)`
by removing some of its vertices and/or edges.

* `(T subset-of V)` and `(U subset-of E)`
* `T` must include all endpoints of any edge in `U`
* i.e. `(E(e) subset-of T)` for all `(e in U)`
* `S` is not necessarily connected
* i.e. `T` hay have isolated vertices
* `(S subgraph-of G) <-> (G supergraph-of S)`

Note that there is in general no requirement (or limitation) as to how the
vertex-subset `T` is formed from `V`. Because of that, an induced subgraph
is not necessarily connected. That is, `S` is a disjoint union  of components.

Similar to simple sets, a **strict/proper subgraph** is formed by removing at
least one vertex and/or edge - i.e. `(#T < #V)` and/or `(#U < #E)`. That is,
any graph `G` is a (simple) subgraph, but no proper subgraph to itself.

An **induced subgraph** `S` is formed from another graph `G` by removing some
of its vertices. In addition to that, the edge-subset in `S` is formed based on
the vertex-subset `T` by selecting all those edges `(e in E)` whose endpoints
are both in `T`.

* `S := G[T] := (T,U)` where `U := { (e in E) | (E(e) subset-of T) }`
* i.e. `S` is a subgraph of `G`, induced by its vertex-subset `T`
* i.e. all those edges in `E` whose endpoints are in `T`
* i.e. no edge in `U` leads in-to, or out-of `T`

A **strict/proper induced subgraph** `S` is formed from another graph `G` by
removing at least one vertex - i.e. `(#T < #V)`. As such, a proper induced
subgraph is always a proper subgraph.

Note that a proper induced subgraph may still have the same edge subset as its
supergraph - i.e. `(U == E)`, i.e. not necessarily `(#U < #E)`. That is because
a proper induced subgraph may be formed by removing only isolated vertices.

<!-- ======================================================================= -->
## inner/outer set of a node

The set of inner nodes `IN(n)` of node `n` may be referred to as **the inner
set of a node** `IS(n)`. In contrary to that, the union of a node with its
inner set will be referred to as **the outer set of a node** `OS(n)`.

* `IS(n) := IN(n) := D(n)`
* `OS(n) := (IS(n) union {n})`
* i.e. `OS(n) <=!=> ON(n)`

Note that `n` will be referred to as **the defining node** of its inner and
its outer set. That is, both sets are defined as: "All the nodes that can be
reached beginning with, and including (or excluding) the defining node".

`IS(n)` and `OS(n)` only differ in the defining node `n`. Because of that the
inner set of a node is a strict subset to its outer set. In addition to that,
the outer set of a descendant is a strict subset to the outer sets of its
ancestors.

* `(#IS(n)+1 == #OS(n))`
* `(IS(n) strict-subset-of OS(n))`

Note that the outer sets of siblings are disjoint. That is because no descendant
of a node is also a descendant of one of the node's siblings. Because of that,
the inner set of a node is the disjoint union of the outer sets of its child
nodes.

* `S := { OS(n) | (n in N) }`, `(#S == #N)`
* i.e. the set of outer sets in a tree, one for each node
* for any pair of sets `(s,t in S)` the following applies:
* if `(s != t)`, then `(s disjoint-to t) ex-or (s strictly-related-to t)`
* i.e. `(s overlaps t)` is `false` for any such pair

Note that, if a parent has one child only, then the parent's inner set is
identical to the outer set of its only child.

<!-- ======================================================================= -->
## (induced) subtree

The term **subtree** may be defined as follows: A subtree `S := (T,U)` is the
subgraph of a graph `G := (V,E)` such that `S` is a tree.

* `(S subgraph-of G)` must be true
* `(is-tree S) := isTree(S)` must be true

Note that `G` is not required to be a tree. Hence, the focus of this definition
is on the characteristic of the subgraph. Note also that `S` may or may not
satisfy further restrictions in addition to the afore mentioned requirements.

Note that a subtree is commonly defined as: "A connected subgraph of a tree".
That is, `G` is required to be a tree. As a result, `S` is a tree. That is
because any connected subgraph of a tree is by consequence automatically a
tree. Because of that, the above definition is more general than the common
definition. However, in the context of this discussion, `G` is in general
always assumed to be a tree.

As above, a **strict/proper subtree** is formed by removing at least one node
and/or edge - i.e. `(#T < #V)` and/or `(#U < #E)`. That is, any subtree `G`
is a (simple) subtree, but no proper subtree to itself.

An **induced subtree** `S` is an induced subgraph such that `S` is a tree.

* `S := G[T] := (T,U)` where `U := { (e in E) | (E(e) subset-of T) }`
* i.e. `S` is a subtree of `G`, induced by its node-subset `T`
* i.e. all those edges in `E` whose endpoints are in `T`
* i.e. no edge in `U` leads in-to, or out-of `T`

A **strict/proper induced subtree** `S` is formed from another graph `G` by
removing at least one vertex - i.e. `(#T < #V)`. As such, a proper induced
subtree is always a proper subtree.

Note that a proper induced subgraph may still have the same edge subset as its
supergraph - i.e. `(U == E)`, i.e. not necessarily `(#U < #E)`. That is because
a proper induced subgraph may be formed by removing only isolated vertices.

<!-- ======================================================================= -->

Note that, if `G` is a tree, then a strict induced subtree

Note that `G` will always have one, and only one edge which
leads into a strict induced subtree.

**TODO** - only one edge that leads into the subtree
- no edge that leads out of the subtree

**TODO** - can an induced subtree be formed from a non-tree graph?
- i.e. `S` is an induced subtree -> `G` must consequently also be a tree

<!-- ======================================================================= -->
## sub-graph, sub-tree

* induced subtree -> induced (sub)path

--

* the union of subtrees
* (strict) subtree as "induced subtrees"
* i.e. induced by its root node
* properly define "sub-graph", "sub-tree"
* vertex/edge disjoint tree
* intersection of a tree

<!-- ======================================================================= -->
## (induced) paths

Note the similarities with the removal-based definition of "subsequence". That
is the removal of vertices and edges from transitive closure of a sequence -
i.e. not just from its cover relation. Because of that, any subsequence can be
considered an "induced subsequence".
