
<!-- ======================================================================= -->
# Subtrees

A (simple) **subtree** `S := (T,U)` is a subgraph of a graph `G := (V,E)`
such that `S` is a tree.

* `(S subgraph-of G)` must be true
* `isTree(S)` must be true

Note that `G` is not required to be a tree. Hence, the focus of this definition
is on the characteristic of the subtree itself. In addition to that, `S` may or
may not satisfy further restrictions.

Note that a subtree is commonly defined as: "A connected subgraph of a tree".
That is, this definition requires `G` to be a tree. Consequently, and because
`S` is a connected subgraph of `G`, `S` is itself a tree. Because of that,
the common definition is more specific and the above definition more general.

A **strict/proper subtree** is formed by removing at least one node and/or
edge - i.e. `(#T < #V)` and/or `(#U < #E)`. That is, any tree `G` is a (simple)
subtree, but no proper subtree to itself.

An **induced subtree** `S := (T,U)` is an induced subgraph of a graph
`G := (V,E)` such that `S` is a tree.

A **strict/proper induced subtree** `S` is an induced subtree formed from
another graph `G` by removing at least one vertex - i.e. `(#T < #V)`.

Note that not even the super-graph of a proper induced subtree is itself
necessarily a tree (e.g. a subtree in a forest of trees). 

Note that a proper induced subtree, formed from another tree, will always have
fewer edges than its super-tree - i.e. `(#U < #E)`. That is because any tree
is a connected graph.

<!-- ======================================================================= -->
## inner/outer set of a node

The set of inner nodes `IN(n)` of node `n` in a tree `T` may be referred to as
**the inner set of a node** `IS(n)`. In contrary to that, the union of a node
with its inner set will be referred to as **the outer set of a node** `OS(n)`.

* `IS(n) := IN(n) := D(n)`
* `OS(n) := (IS(n) union {n})`
* i.e. `OS(n) <=!=> ON(n)`

Note that `n` will be referred to as **the defining node** of its inner and its
outer set. That is, both sets are defined as: "All the nodes that can be reached
beginning with, and including (or excluding) the defining node".

`IS(n)` and `OS(n)` only differ in the defining node `n`. Because of that, the
inner set of a node is a strict subset to the node's outer set. In addition
to that, the outer set of a descendant is a strict subset to the outer sets of
its ancestors.

* `(#IS(n) == #OS(n)-1)`
* `(IS(n) strict-subset-of OS(n))`

Note that, if a parent has one child only, then the parent's inner set is equal
to the outer set of its only child. **TODO** (there was some thought ...)

Note that the outer sets of siblings are disjoint. That is because no descendant
of a node is also a descendant of the node's siblings. For that to be false, a
node would need to have more than one parent. Because of that, the inner set of
a node is the disjoint union of the outer sets of its child nodes.

* `S := { OS(n) | (n in N) }`, i.e. `(#S == #N)`
* i.e. `S` is the set of outer sets in a tree, one for each node

For any pair of sets `(s,t in S)` the following applies:

* if `(s != t)`, then `(s disjoint-to t) ex-or (s strictly-related-to t)`
* i.e. `(s overlaps t)` is `false` for any pair in `S`

<!-- ======================================================================= -->
## subtree of a tree

There are obviously several ways to form a subtree `S` from a given tree `T`.
However, and independently of how exactly a subtree is formed, a subtree will
always have a root `r`. (Note that `r` may or may not be identical to the root
of the super-tree).

Like any other tree, each node in `S` has a unique rooted path in `T`. In
addition to that, a subtree is not required to contain all the descendants
of `r` in `T`. Consequently, `S` may have leaf nodes that are no leafs in `T`.

That is, a subtree is in general defined by its root and its leaf nodes.

Note that, in the context of this discussion, the super-graph of a sub-tree
is in general assumed to be an arborescence and any sub-tree is assumed to
be a non-empty induced subtree of such a super-tree.

once the first node of a subtree is selected, all other nodes must
be reachable from that node.

<!-- ======================================================================= -->
## TODO

* define `R(T)` as the root of a tree
* an induced subtree is induced by the subtree's root
* only one edge that leads into the subtree
* no edge that leads out of the subtree

--

* can an induced subtree be formed from a non-tree graph?
* yes, if isolated vertices are excluded

however, since an induced subtree is based on a connected component, the
super-graph must contain the subtree as is. that is, an induced subtree
is formed by cutting away the exterior - i.e. what is outside of it.
