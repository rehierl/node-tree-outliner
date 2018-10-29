
<!-- ======================================================================= -->
# Path-based, node-related definitions

* (/see/ "path of nodes" /)
* (/see/ "relationship between sets /)
* definitions based upon uni-directional, downward-oriented paths

<!-- ======================================================================= -->
## level, depth, height

The level/depth of a node can be defined as follows:

* `level(n) := (#rp(n) - 1)` - the node level of a node
* `depth(n) := (#rp(n) - 1)` - the depth of a node
* i.e. the edge-length of the node's rooted path
* i.e. `(level(r) == 0)` and `(depth(r) == 0)`

The height of a node/tree can be defined as follows:

* `height(n) := max({ #p-1 | (p in p(n,L)) })`
* i.e. the edge-length of the longest node-to-leaf path
* `height(tree) := height(r)`
* i.e. the height of a tree is the height of its root
* i.e. `(height(l) == 0)` for `(l in LN)`

Note that the height of a tree is equivalent to its diameter.

<!-- ======================================================================= -->
## ancestor, descendant

Because of the paths in a tree being downward oriented, the following can
be said about the relationship between the nodes of a path:

(x ancestor-of y)

* `(x ancestor-of y)` is true, if `xPy`
* i.e. `x` is said to be an ancestor of `y`
* notational: `xAy := xPy`

(y descendant-of x)

* `(y descendant-of x)` is true, if `xPy`
* i.e. `y` is said to be a descendant of `x`
* i.e. `descendant-of` is antonymous to `ancestor-of`
* notational: `yDx := xPy`

Based on such paths, the following subsets of `N` can be defined:

* `AN := { a | aPn for some (n in N) }`
* i.e. the set of all ancestor nodes
* i.e. each `(a in AN)` is an ancestor
* `DN := { d | nPd for some (n in N) }`
* i.e. the set of all descendant nodes
* i.e. each `(d in DN)` is a descendant

Similar to that, the following functions can be defined:

* `(A: N -> P(N))`, or `P(n) := { a | aPn }`
* i.e. `A(n)` returns the set of all ancestors of `n`
* i.e. `(A(n) subset-of AN)` is true
* `(D: N -> P(N))`, or `D(n) := { d | nPd }`
* i.e. `D(n)` returns the set of all descendants of `n`
* i.e. `(D(n) subset-of DN)` is true

With regards to downward-oriented paths:

* `p := (n1,...,ni,...,nk)` where `(p in P)`
* `(n(i-j) ancestor-of ni)` for `(j in [1,(i-1)])`
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
a given node `n` may be referred to as "the distant ancestors of a node".

The set of nodes `DD(n) := D(n) \ C(n)` that are descendants, but no child to
a given node `n` may be referred to as "the distant descendants of a node".

<!-- ======================================================================= -->
## a recursive definition of rooted paths

In a rooted path, any edge is downward oriented (i.e. from an ancestor
towards its descendants). Because of that, the ancestors `A(n)` of a
node `n` are all presequent to that node in the node's rooted path:

* `(A(n) union {n}) == E(rp(n))`
* `rp(n) := (prefix × n)` where `(E(prefix) == A(n))`

Furthermore, the parent `p` of a node is the least significant ancestor
of a node. That is, `p` is subordinate to any other ancestor in `A(n)`:

* `rp(n) := (prefix × p × n)` where `(E(prefix) == DA(n))`
* `rp(n) := (rp(p) × n)` where `(p parent-of n)` and `rp(r) := (r)`
* i.e. a recursive definition of rooted paths
* `(rp(a) prefix-of rp(n))` where `(a ancestor-of n)`

A tree's root `r` is the most significant ancestor of all other nodes.

* `(r ancestor-of n)` is true for all non-root nodes `(n in N\RN)`

<!-- ======================================================================= -->
# inner/outer node of a node

Due to all rooted paths having a downward (aka. inward) directed orientation,
the nodes in `N` can be classified with regards to a given node `n`:

The set of descendants `D(n)` of a node `n` may be referred to as **the inner
nodes of a node** `IN(n)`. And because each node has an "inside", any node can
be understood to have an "outside". The set of nodes that are not inner nodes
to a given node, excluding the node itself, may therefore be loosely referred
to as **the outer nodes of a node** `ON(N)`.

* `IN(n) := D(n)`
* `ON(n) := (N \ IN(n) \ {n})`
* i.e. `(n !in IN(n))` and `(n !in ON(n))`
* i.e. `{n} == ((N \ IN(n)) \ ON(n))`
* `(A(n) subset-of ON(n))`
* i.e. `(#A(n) <= ON(n))`

Note that ...

* `n` is neither an inner node, nor an outer node to itself
* `(#A(n) <= #ON(n))`, i.e. both sets are not necessarily identical

<!-- ======================================================================= -->
## nodes - contains, inside-of, outside-of

A node `x` is said to **contain** node `y`,
if `(y in IN(x))`. That is, `y` is an inner node of `x`.

* `(x in y) := (y in IN(x))`
* `(x contains y) := (x in y)`
* `xPy` is true, iff `(x contains y)`

A node `x` is said to be **(located) inside of** node `y`,
if `(x in IN(y))`. That is, `x` is an inner node of `y`.

* `(x inside-of y) := (x in IN(y))`
* `(x inside-of y) := (y contains x)`
* `(x inside-of y) := (IN(x) subset-of IN(y))`

A node `x` is said to be **(located) outside of** node `y`,
if `(x in (N \ IN(y) \ {y}))`.
That is, `x` is not inside-of and not equal-to `y`.

* `(x outside-of y) := (x !in y) and (x != y)`
* `(x outside-of y) <=!=> not (x inside-of y)`

Note that both definitions (i.e. inside-of, outside-of) provide a sense of
direction (i.e. inwards, outwards) with regards to a given node.

<!-- ======================================================================= -->
## nodes - coupled, disjoint, overlap

Two distinct nodes `x` and `y` are said to be **coupled** with each other, if
one contains the other. That is, one node is an inner node (aka. a descendant)
of the other.

* `(x coupled-with y) := (xPy or yPx)`
* `(x coupled-with y) := (x in E(rp(y))) or (y in (E(rp(x)))`
* `(x coupled-with y) := (x in IN(y)) or (y in IN(x))`
* `(x coupled-with y) := (IN(x) coupled-with IN(y))`
* i.e. coupled-with has no orientation

Two distinct nodes `x` and `y` are said to be **disjoint** from one another,
if both nodes are not coupled with each other:

* `(x disjoint-from y) := !(x coupled-with y)`
* i.e. disjoint-from has no orientation
* disjoint <=> not coupled

Less accurately, the sets of inner nodes of two disjoint nodes `x` and `y`
(i.e. `IN(x)` and `IN(y)`) are disjoint. That is, both nodes have no descendants
in common.

Furthermore, if `(y in x)`, then any descendant `d` of `y` is also a descendant
of `x`. That is because any rooted path `rp(d)` contains `x` and `y` such that
`(x presequent-to y)`. Therefore, `(d in IN(x))` is true for all `(d in IN(y))`.
Consequently, `(IN(y) strict-subset-of IN(x))` because `y` is also a descendant
of `x`, but no descendant to itself.

Because of that, two sets of inner nodes `IN(x)` and `IN(y)` in a tree are
either strictly related (i.e. one is a strict subset of the other) ex-or both
sets are disjoint. That is, both nodes can not be understood to **overlap**
each other.

Recall that two sets of elements are said to overlap each other, if both sets
have one or more elements in common, but none is a subset of the other.
