
<!-- ======================================================================= -->
# (Strict) Subtree

* (/see/ "hierarchy of sets" /)

<!-- ======================================================================= -->
## (induced) subgraph

A **sub-graph** `S := (T,U)` is a graph derived from a `G := (V,E)`
by removing some of its vertices and/or edges.

* `(T subset-of V)` and `(U subset-of E)`
* `T` must include all endpoints of any edge in `U`
* note - not all vertices in `T` need to be connected

An **induced subgraph** `S` is formed from a super-graph `G` by removing some
of its vertices. In addition to that, the edge-subset in `S` is formed based
on the vertex-subset `T` by selecting all edges `(e in E)` that have both
endpoints in `T`.

* `S := G[T] := (T,U)` where `U := { (e in E) | (E(e) subset-of T) }`
* i.e. `S` is a subgraph of `G`, induced by its vertex-subset `T`
* i.e. no edge in `U` leads in-to, or out-of `T`

Note that there is in general no requirement (or limitation) as to how the
vertex-subset `T` is formed from `V`. Because of that, even an induced
subgraph is not necessarily connected. That is, `S` is a disjoint union
of components.

Similar to simple sets, a **strict/proper subgraph** is formed by removing
at least one vertex and/or edge - i.e. `(#T <= #V)` and/or `(#U <= #E)`.
That is, any graph `G` is a (simple) subgraph to itself. In contrary to that,
no proper subgraph is identical to its super-graph.

<!-- ======================================================================= -->
## inner/outer set of a node

The set of inner nodes `IN(n)` of a node `n` may be referred to as **the
inner set of a node** `IS(n)`. In contrary to that, the union of a node with
its inner set will be referred to as **the outer set of a node** `OS(n)`.

* `IS(n) := IN(n) := D(n)`
* `OS(n) := (IS(n) union {n})`
* i.e. `OS(n) <=!=> ON(n)`

Note that `n` will be referred to as **the defining node** of its inner and
its outer set. That is, both sets are defined as: "All the nodes that can be
reached beginning with, and including or excluding the defining node".

`IS(n)` and `OS(n)` only differ in their defining node `n`. Because of that
the inner set of a node is a strict subset to its outer set. In addition to
that, the outer set of a descendant is a strict subset to the outer sets of
its ancestors.

* `(#IS(n) == #OS(n)-1)`
* `(IS(n) strict-subset-of OS(n))`

Note that the outer sets of siblings are disjoint. That is because no descendant
of a node is also a descendant of one of the node's siblings. Because of that,
the inner set of a node is the disjoint union of the outer sets of its child
nodes.

* `S := { OS(n) | (n in N) }`
* for any pair of sets `(s,t in S)` such that `(s != t)` ...
* `(s disjoint-to t) ex-or (s strictly-related-to t)`
* i.e. `(s overlaps t)` is `false` for any such pair

Note that, if a parent has one child only, the parent's inner set is identical
to the outer set of its only child.

<!-- ======================================================================= -->
## (induced) subtree

The term "subtree" may initially be characterized as follows:
A subgraph `S` of a graph `G` such that `S` is a tree.

* `(S subgraph-of G)` must be true
* `(is-tree S) := isTree(S)` must be true

Note that `G` is not required to be a tree. Also, `S` may or may not satisfy
further conditions in addition to the afore mentioned requirements.


<!-- ======================================================================= -->
## sub-graph, sub-tree

* given tree `T:=(N,E,P)`
* induced subtree `T(n):=(N',E',P')` for `(n in N)`
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
