
<!-- ======================================================================= -->
# Node tree definitions

* a summary of standard and non-standard definitions
* i.e. definitions used throughout this discussion
* the focus is on directed rooted trees of nodes
* aka. arborescence, out-tree

Note that forests, i.e. possibly empty unions of disjoint trees,
are not in the focus of this discussion.

<!-- ======================================================================= -->
## downward-oriented edges

An arborescence is a directed tree `T` defined as a tuple of sets:

* `T := (N,E)`
* `N` is the non-empty set of nodes
* `(E subset-of N×N)` is the possibly empty set of edges

Each node `(n in N)` can be understood to represent some unique object:

* `(o: N -> O)` - is a bijective function
* `o(n)` returns the object that node `n` represents
* i.e. `(o(x) !== o(y))` where `(x,y in N)`
* i.e. distinct nodes represent distinct objects
* `(n: O -> N)` - is inverse to `o()`
* `n(o)` returns the id/reference/node of object `o`
* i.e. `(o(n(o)) === o)` and `(n(o(n)) === n)`

Due to each edge `(e in E)` being an ordered pair of nodes `((x,y) in N×N)`,
the following can be said about the relationship between the nodes `x` and `y`
of `e`:

* `x` is the parent node of `y`
* i.e. `(x parent-of y)` is true
* `y` is a child node of `x`
* i.e. `(y child-of x)` is true
* i.e. `child-of` is antonymous to `parent-of`
* `x` is super-ordinate to `y`
* `y` is sub-ordinate to `x`
* `x` is more significant than `y`
* `y` is less significant than `x`

The following can be said about an edge `e` and the relationship it has with
its nodes `x` and `y`:

* `e := (x,y)` or `(x -> y)`
* `e` begins in `x` and ends in `y`
* `e` is an outgoing edge of `x`
* `e` is an incoming edge of `y`
* `e` is downward-directed/oriented
* `e` points away from a super-ordinate towards a sub-ordinate node

Because no node is considered to be super- or sub-ordinate to itself,
no edge is allowed to begin and end in the same node.

* `((x,x) in E)` is not allowed
* i.e. a tree of nodes has no loops
* i.e. each edge is an ordered pair of distinct nodes
* i.e. `((x,y) in E)` iff `(x != y)`

Each tree can be understood to have an indicator function `E()` such that:

* `(E: N×N -> Bool)` or `E(x,y) := ((x,y) in E)`
* notational: `xEy := E(x,y)`

<!-- ======================================================================= -->
## root, parent, child, inner, leaf

Based on `E`, the following subsets of `N` can be defined:

* `RN := { r | ((x,r) !in E) for all (x in N) }`
* i.e. the set of nodes that have no parent
* i.e. each `(r in RN)` is a root node
* `PN := { p | pEy for some (y in N) }`
* i.e. the set of nodes that are parent to some child
* i.e. each `(p in PN)` is a parent node
* `CN := { c | xEc for some (x in N) }`
* i.e. the set of nodes that are child to some parent
* i.e. each `(c in CN)` is a child node
* `IN := { i | (i in PN) and (i in CN) }`
* i.e. the set of nodes that have a parent and a child
* i.e. each `(i in IN)` is an inner node of the tree
* `LN := { l | ((l,y) !in E) for all (y in N) }`
* i.e. the set of nodes that have no child
* i.e. each `(l in LN)` is a leaf node

Similar to that, the following functions can be defined:

* `(P: N -> P(N))`, or `P(n) := { p | pEn }`
* i.e. `P(n)` returns the set of parent nodes of `n`
* i.e. `n` is a child, if `(P(n) != {})`
* notational: `xPy := (x in P(y))`
* `(C: N -> P(N))`, or `C(n) := { c | nEc }`
* i.e. `C(n)` returns the set of child nodes of `n`
* i.e. `n` is a parent, if `(C(n) != {})`
* notational: `xCy := (x in C(y))`

The following conditions hold for all trees:

* `(#RN == 1)` - each tree always has exactly one root `r`
* `(#P(c) == 1)` - each child has exactly one parent
* `(#N >= 1)` - a tree has at least its root as node
* i.e. the tree's set of nodes is never empty

Because of that, `P()` can be re-defined as follows:

* `(P: N -> N)` or `P(n) := p such that pEn`
* i.e. `P(n)` returns the parent of node `n`
* i.e. `P(r)` returns a `null` reference for `r`
* notational: `xPy := (x == P(y))`

Some further characteristics of a tree are:

* any parent has a child node
* any child has a parent (and one parent only)
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
* i.e. `(x sibling-of y)`, if `(P(x) == P(y))` is true
* i.e. siblings have the same parent node
* notational: `xSy := (x sibling-of y)`
* `(x sibling-of y) <-> (y sibling-of x)`
* i.e. unlike `parent-of`, `sibling-of` has no orientation
* i.e. siblings are considered to be equal

The following function can be defined:

* `(S: N -> P(N))` or `S(n) := { s | pEs where pEn and (s != n) }`
* `S(n)` returns the set of siblings of node `n`
* i.e. `S(n) := C(p)\{n}` where `pEn`
* notational: `xSy := (x in S(y))`

Remarks

* a tree has no edge `xEy` or `yEx`, if `xSy`
* **TODO** - not right-euclidean - `pEa` and `pEb`, but neither `aEb` nor `bEb`

<!-- ======================================================================= -->
## parent-of semantics

The semantics of an edge `e := (p,c) in E` is such that:

* `(e in E)`, `(E subset-of PN×CN)` and `(PN×CN subset-of N×N)`
* `(p parent-of c)` - i.e. `p` is the parent of `c`
* i.e. each edge is downward-oriented
* `(c child-of p)` - i.e. `c` is a child of `p`
* `pEc <-> (p parent-of c) <-> (c child-of p)`
* i.e. `sem(E)` := "parent-of", not "child-of"

Note that, if all edges are inverted (i.e. child-of semantics), the resulting
directed graph would no longer be tree. That is, because the structure would
then have one or more root nodes (i.e. the former leaf nodes) and never more
than one leaf node (i.e. the former root). Consequently, and if non-linear,
that structure would not correspond with the definition of an arborescence.
