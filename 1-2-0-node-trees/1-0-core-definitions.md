
<!-- ======================================================================= -->
# Definitions related to node trees

* standard and non-standard, tree-related definitions
* the focus is on directed rooted node trees
* aka. arborescence, out-tree

<!-- ======================================================================= -->
## basic definitions

An arborescence/tree is an oriented graph `T` defined as a tuple of sets:

* `T := (N,E)` is a graph of nodes
* `N` is the non-empty set of nodes
* `(E subset-of N×N)` is the possibly empty set of edges
* such that `(E(e) subset-of N)` for all `(e in E)`
* i.e. both endpoints of each edge are nodes in `N`

As trees are directed graphs, each node represents a unique object:

* `o(n)` returns the object that node `n` represents
* `n(o) := v(o)` returns the id/reference/node of object `o`

The following can be said about the nodes of an edge:

* `e := (x,y)` or `(x -> y)`
* `x` is the parent of `y`, and `y` is a child of `x`
* i.e. `(x parent-of y)` is true, iff `x` is the parent of `y`
* i.e. `(y child-of x)` is true, iff `y` is a child of `x`
* i.e. `child-of` is antonymous to `parent-of`
* `x` is super-ordinate to `y`, and `y` is sub-ordinate to `x`
* `x` is more significant than `y`, and `y` is less significant than `x`

The following can be said about an edge `e` and the relationship it has
with both of its nodes `x` and `y`:

* `e` is downward-directed/oriented
* i.e. from a super-ordinate towards a sub-ordinate node

Like any (directed) graph, each tree can be understood to have an indicator
function `E()` associated with it:

* `(E: N×N -> Bool)` or `E(x,y) := ((x,y) in E)`
* notational: `xEy := E(x,y)`

Because no node is considered to be super- or sub-ordinate to itself,
no edge begins and ends in the same node.

* `xEx` is not allowed to be true for any `(x in N)`
* i.e. a tree of nodes has no loops
* i.e. each edge is an ordered pair of distinct nodes
* i.e. `xEy` may be true iff `(x != y)`

<!-- ======================================================================= -->
## root, parent, child, inner, leaf

Based on `E`, the following subsets of `N` can be defined:

* `RN := { (r in N) | ((x,r) !in E) for all (x in N) }`
* i.e. the set of nodes that have no parent
* i.e. each `(r in RN)` is a root node
* i.e. each root is a source vertex: `(RN == SRC)`
* `PN := { (p in N) | pEy for some (y in N) }`
* i.e. the set of nodes that are parent to some child
* i.e. each `(p in PN)` is a parent node
* `CN := { (c in N) | xEc for some (x in N) }`
* i.e. the set of nodes that are child to some parent
* i.e. each `(c in CN)` is a child node
* `IN := { (i in N) | (i in PN) and (i in CN) }`
* i.e. the set of nodes that have a parent and a child
* i.e. each `(i in IN)` is an inner node to the tree
* i.e. each inner node is an internal vertex: `(IN == INT)`
* `LN := { (l in N) | ((l,y) !in E) for all (y in N) }`
* i.e. the set of nodes that have no child
* i.e. each `(l in LN)` is a leaf node
* i.e. each leaf is a sink vertex: `(LN == SNK)`

Similar to that, the following functions can be defined:

* `(p: N -> p(N))`, or `p(n) := { p | pEn }`
* i.e. `p(n)` returns the set of parent nodes of `n`
* i.e. `n` is a child, if `(p(n) != {})`
* i.e. `p()` is equivalent to `src()`
* notational: `xPy := (x in p(y))`
* `(c: N -> P(N))`, or `c(n) := { c | nEc }`
* i.e. `c(n)` returns the set of child nodes of `n`
* i.e. `n` is a parent, if `(c(n) != {})`
* i.e. `c()` is equivalent to `snk()`
* notational: `xCy := (x in c(y))`

The following conditions hold for all trees:

* `(#RN == 1)` - each tree always has exactly one root `r`
* `(#N >= 1)` - a tree has at least its root as node
* i.e. the tree's set of nodes is never empty
* `(#p(c) == 1)` - each child has exactly one parent

Because of that, `p()` can be re-defined:

* `(p: N -> N)` or `p(n) := p such that pEn`
* i.e. `p(n)` returns the parent of node `n`
* i.e. `p(r)` returns a `null` reference for `r`
* note - `p()` is still considered to be identical to `src()`
* i.e. even though `p()` returns a node and `src()` a set of nodes
* notational: `xPy := (x == p(y))`

Note that, because of `(#p(c) == 1)`, each non-root node `(n in N\RN)` is
a sink to one, and only one, edge. That is, each child node has exactly
one incoming edge. In contrary to that, each non-leaf node `(n in N\LN)`
is a source to one or more edges. That is, each parent node has one or
more outgoing edges. Put differently, each node may be the sink of an edge
no more than once. In contrary to that, any node may act as a source to any
number of edges.

<!-- ======================================================================= -->
## remarks

Further characteristics are:

* each parent has a child
* each child has a parent, and one parent only
* a root has no parent, but may itself be one
* a root is no child, but may itself have one
* `(#N == 1)` => `(RN,LN == {r})` and `(PN,CN,IN == {})`
* i.e. a root may even be a leaf
* `(#N >= 2)` => `(RN,PN,CN,LN != {})` but `(IN ?= {})`
* i.e. any tree always has one or more leaf nodes
* i.e. trees may or may not have inner nodes

With regards to a node's parent (i.e. a parent-based view):

* `RN := (N - CN)`
* i.e. `RN` and `CN` are disjoint
* i.e. any node is either a root ex-or a child
* i.e. all nodes, except for the root, are child nodes
* a leaf is no parent, but may itself have one

With regards to a node's child nodes (i.e. a child-based view):

* `PN := (N - LN)`
* i.e. `PN` and `LN` are disjoint
* i.e. any node is either a parent ex-or a leaf
* i.e. any node, except for a leaf, is a parent
* a leaf has no child, but may itself be one

<!-- ======================================================================= -->
## siblings

* `x` is a child of `p`, if `pEx` is true
* `x` is a sibling of `y`, if `(pEx and pEy)` is true
* i.e. `(x sibling-of y)`, if `(p(x) == p(y))` is true
* i.e. siblings have the same parent node
* notational: `xSy := (x sibling-of y)`
* `(x sibling-of y) <-> (y sibling-of x)`
* i.e. unlike `parent-of`, `sibling-of` has no orientation
* i.e. siblings are considered to be equal

The following function can be defined:

* `(s: N -> P(N))` or `s(n) := { s | pEs where pEn and (s != n) }`
* `s(n)` returns the set of siblings of node `n`
* i.e. `s(n) := c(p)\{n}` where `pEn`
* notational: `xSy := (x in s(y))`

Note that there is no edge `xEy` or `yEx`, if `xSy`.

**TODO**
- not right-euclidean - `pEa` and `pEb`, but neither `aEb` nor `bEb`
- recheck the exact properties of "right-euclidean"

<!-- ======================================================================= -->
## semantics of a tree

The semantics of a tree `T := (N,E)` is such that:

* `sem(T) := (p parent-of c)` - i.e. `p` is the parent of `c`
* `((p,c) in E)`, `(E subset-of PN×CN)` and `(PN×CN subset-of N×N)`
* i.e. each edge is downward-oriented

In contrary to that:

* `sem(G) := (c child-of p)` - i.e. `c` is a child of `p`
* i.e. `pEc <-> (p parent-of c) <-> (c child-of p)`
* i.e. each edge is upward-oriented

Note that, in both cases, the semantics of each edge is oriented in the
direction of the corresponding edge. That is, the edges have consistently
oriented semantics.

Note that, if all edges are inverted (i.e. `child-of` semantics), the resulting
oriented graph would in general no longer be a tree. That is, because the
structure would then have one or more root nodes (i.e. the former leaf nodes)
and always one, and only one leaf node (i.e. the former root). Consequently,
and if non-linear, that structure would not correspond with the definition of
an arborescence. Hence, such a tree must have the `parent-of` semantics.

<!-- ======================================================================= -->
## remarks

Note that the `parent-of` relation can not be seen as a function: not right
unique (i.e. a parent may have several child nodes, i.e. not functional).
In contrary to that, the antonymous `child-of` relation is functional: right
unique (i.e. each child has one parent only, i.e. functional), not left-unique
(i.e. a parent may have several child nodes, i.e. not injective), not left
total (i.e. the root has no parent), not right total (i.e. leaf nodes have
no child, i.e. not surjective).
