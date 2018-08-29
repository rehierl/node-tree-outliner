
<!-- ======================================================================= -->
# Path-based, node-related definitions

* (/see/ "path of nodes" /)
* definitions based upon unidirectional, downward-oriented paths

<!-- ======================================================================= -->
## level, depth, height

The level/depth of a node can be defined as follows:

* `level(n) := (#rp(n) - 1)` - the node level of a node
* `depth(n) := (#rp(n) - 1)` - the depth of a node
* i.e. the edge-length of the node's rooted path
* i.e. `(level(r) == 0)` and `(depth(r) == 0)`

The height of a node/tree can be defined as follows:

* `height(n) := max({ #p | (p in p(n,L)) }) - 1`
* i.e. the edge-length of the longest node-to-leaf path
* `height(tree) := height(r)`
* i.e. the height of a tree is the height of its root
* i.e. `(height(l) == 0)` for `(l in LN)`

<!-- ======================================================================= -->
## ancestor, descendant

Because of the paths in a tree being downward oriented, the following can be
said about the relationship between the nodes of a path:

* for `(p in P)` and `p := p(x,y)` - i.e. `xPy`
* `x` is an **ancestor of** `y`
* i.e. `(x ancestor-of y)` is true
* notational: `xAy := xPy`
* `y` is a **descendant of** `x`
* i.e. `(y descendant-of x)` is true
* i.e. `descendant-of` is antonymous to `ancestor-of`
* notational: `yDx := xPy`

Based on such paths, the following subsets of `N` can be defined:

* `AN := { a | aPn for one or more (n in N) }`
* i.e. the set of all ancestor nodes
* i.e. each `(a in AN)` is an ancestor
* `DN := { d | nPd for one or more (n in N) }`
* i.e. the set of all descendant nodes
* i.e. each `(d in DN)` is a descendant

Similar to that, the following functions can be defined:

* `(A: N -> P(N))`, or `P(n) := { a | aPn }`
* i.e. `A(n)` returns the set of all ancestors of `n`
* i.e. `(A(n) subset-of AN)` is true
* `(D: N -> P(N))`, or `D(n) := { d | nPd }`
* i.e. `D(n)` returns the set of all descendants of `n`
* i.e. `(D(n) subset-of DN)` is true

Remarks in general:

* any edge points away from an ancestor towards its descendants
* `(A(n) union {n}) == E(rp(n))`
* i.e. the ancestors of a node are all located on the rooted path of a node
* `(r ancestor-of n)` is true for any `(n in (N \ RN))`
* i.e. a tree's root is an ancestor to any non-root node
* i.e. any non-root node is a descendant to a tree's root
* the parent of a node `P(n)` is the node's least significant ancestor
* i.e. `P(n)` is sub-ordinate to all other nodes in `A(n)`

With regards to downward-oriented paths:

* `p := (n1,...,ni,...,nk)` where `(p in P)`
* `(n(i-j) ancestor-of ni)` for `(j in [1,*])`
* `(n(i+j) descendant-of ni)` for `(j in [1,*])`

With regards to `AN`:

* `AN := (N - LN)`
* i.e. `AN` and `LN` are disjoint
* i.e. `(l !in AN)` - i.e. a leaf is no ancestor
* a parent is an ancestor to its child nodes
* a parent may itself have one or more ancestors

With regards to `DN`:

* `DN := (N - RN)`
* i.e. `DN` and `RN` are disjoint
* i.e. `(r !in DN)` - i.e. a root is no descendant
* a child is a descendant to its parent node
* a child may itself have one or more descendants
* `(node.children[i].parent == node)` is true

<!-- ======================================================================= -->
## distant ancestor/descendant

The set of nodes `DA(n) := A(n) \ P(n)` that are ancestors, but no parent to
a given node `n` will be referred to as **the distant ancestors of a node**.

The set of nodes `DD(n) := D(n) \ C(n)` that are descendants, but no child to
a given node `n` will be referred to as **the distant descendants of a node**.

<!-- ======================================================================= -->
## inner/outer nodes of a node

Due to all rooted paths having a downward (aka. inward) directed orientation,
the nodes in `N` can be classified with regards to a given node `n`:

The set of descendants `D(n)` of a node `n` may be referred to as **the inner
nodes of a node**. And because each node has an "inside", any node can also be
understood to have an "outside". The set of nodes that are not inner nodes to
a given node will be referred to as **the outer nodes of a node**.

* `IN(n) := D(n)`
* `ON(n) := (N \ IN(n) \ {n})`
* `(A(n) subset-of ON(n))`
* i.e. `(#A(n) <= ON(n))`

Note that `A(n)` and `ON(n)` are not identical!

<!-- ======================================================================= -->
## contains, inside-of

A node `x` is said to **contain** node `y`, iff `(y in IN(x))`.
That is, `y` is an inner node of `x`.

* `(x in y) := (y in IN(x))`
* `(x contains y) := (x in y)`
* `xPy` is true, iff `(x contains y)`

A node `x` is said to be **(located) inside of** node `y`, iff `(x in IN(y))`.
That is, `x` is an inner node of `y`.

* `(x inside-of y) := (x in IN(y))`
* `(x inside-of y) := (y contains x)`
* `(x inside-of y) := (IN(x) subset-of IN(y))`

<!-- ======================================================================= -->
## coupled, disjoint, overlap

Two distinct nodes `x` and `y` are said to be **coupled** with each other,
if one contains the other.

* `(x coupled-with y) := (xPy or yPx)`
* i.e. coupled-with has no orientation
* `(x coupled-with y) := (x in E(rp(y))) or (y in (E(rp(x)))`

Two distinct nodes `x` and `y` are said to be **disjoint** from one another,
if both nodes are not coupled with each other:

* `(x disjoint-from y) := !(x coupled-with y)`
* i.e. disjoint-from has no orientation
* disjoint <=> not coupled

Put differently, the sets of nodes `IN(x)` and `IN(y)` of two disjoint nodes
`x` and `y` are disjoint. That is, both nodes have no descendants in common.

Furthermore, if `(y in x)`, then any descendant `d` of `y` is also a descendant
of `x`. That is because any rooted path `rp(d)` contains `x` and `y` such that
`(x presequent-to y)`. Hence, any `(d in IN(x))` for all `(d in IN(y))`.
Consequently, `(IN(y) strict-subset-of IN(x))` because `y` is also a descendant
of `x`, but no descendant to itself.

Because of that, both sets of inner nodes `IN(x)` and `IN(y)` of two distinct
nodes `x` and `y` in a tree are either strictly related (i.e. one is a strict
subset of the other) ex-or both sets are disjoint. That is, both nodes can not
be understood to **overlap** each other.

Note that two sets of elements are said to overlap each other, if both sets
have one or more elements in common, but none is a subset of the other.
