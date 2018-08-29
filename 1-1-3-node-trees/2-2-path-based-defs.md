
<!-- ======================================================================= -->
# Path-based definitions

* (/see/ "path of nodes" /)
* definitions based upon unidirectional, downward-oriented paths

**TODO** - distant descendants `(D(n) \ C(n))`
**TODO** - ancestors located on the rooted path
**TODO** - define inner/outer nodes of a node
**TODO** - outer ?= ancestors

<!-- ======================================================================= -->
## paths of nodes

**TODO** - move to 2.1.

The set of edges `E` allows to define sequences (aka. paths) of nodes:

* `p := (n1,n2,...,nk)` where `(ni parent-of ni+1)`
* i.e. these are uni-directional, downward-oriented paths
* i.e. paths as defined above are consistent with the tree's relation
* `#p` is the length of a path (in number of nodes)
* i.e. `(#p == k)` for `p := (n1,n2,...,nk)`
* `p1 := (n)` and `p2 := ()` are both seen as degenerated paths
* i.e. these paths do not contain any edge `(e in E)`
* `p(x,y) := (x,...,y)` is a path between `x` and `y`
* `xPy` := "a path `p(x,y)` an be formed/constructed"

A tree can be understood to have an associated set of paths `P`:

* `P := { xPy | (x,y in N) and (x != y) }`
* i.e. `P` is the set of all possible paths
* `xPy` is true if `(p(x,y) in P)`

(x connected-with y)

* a path `p` is said to connect a node with all the other nodes in it
* i.e. `p(x,y)` connects `x` with `y` and any other node in between
* `(x connected-with y) <-> (y connected-with x)`
* i.e. `connected-with` is understood to have no orientation
* i.e. `p(x,y)` also connects `y` with `x` and any other node in `p`

The rooted path `rp(n)` of a node `n` can be defined as follows:

* `rp(n) := p(r,n) := (r,...,n)`
* i.e. a path that begins in the root `r` and ends in the node `n`

<!-- ======================================================================= -->
## no loops, acyclic, connected

Each edge `(e in E)` is considered to be a path in `P`:

* `xEy <-> xPy`
* `((x,x) !in E) <-> ((x,x) !in P)`

A path `p` is said to have loops, if ...

* `(p in P)` and `p := (...,x,x,...)`
* i.e. `(p[i] == p[i+1])` for some `(i in [1,#p-1])`
* note - a tree is not allowed to have any loops

A path `p` is said to have cycles, if ...

* `(p in P)` and `p := (...,x,...,x,...)`
* i.e. `(p[i] == p[j])` for `(i != j)`
* i.e. a cycle is a path that begins and ends in the same node
* 1-cycle - a cycle of edge-length one - `p := (a,a)` - aka. loop
* 2-cycle - a cycle of edge-length two - `p := (a,b,a)`
* note - a tree is not allowed to have cycles
* i.e. each tree is required to be acyclic

Each node in a tree has a unique rooted path:

* `(#RP(n) == 1)` where `RP(n) := { rp(n) }`
* i.e. exactly one rooted path `rp(n)` can be formed for any node
* i.e. each node `n` is connected with the root `r`
* i.e. `rPn` is true for any `(n in N)`
* i.e. any tree is a directed connected graph

**TODO** - any downward-directed path in a finite tree has finite length

<!-- ======================================================================= -->
## level, depth, height

The level/depth of a node can be defined as follows:

* `level(n) := (#rp(n) - 1)` - the node level of a node
* `depth(n) := (#rp(n) - 1)` - the depth of a node
* i.e. the edge-length of the node's rooted path
* i.e. `(level(r) == 0)` and `(depth(r) == 0)`

The height of a node/tree can be defined as follows:

* `height(n) := max({ #p | (p in p(n,L)) }) - 1`
* i.e. the length of the longest node-to-leaf path, minus one
* i.e. the edge-length of the longest node-to-leaf path
* `height(tree) := height(r)`
* i.e. the height of a tree is the height of its root
* i.e. `(height(leaf) == 0)`

<!-- ======================================================================= -->
## ancestor, descendant

Because of paths being downward oriented, the following can be said
about the relationship between the nodes of a path:

* for `(p in P)` and `p := (x,...,y)` - i.e. `xPy`
* `x` is an ancestor of `y`
* i.e. `(x ancestor-of y)` is true
* synonymous to that, `xAy := xPy`
* `y` is a descendant of `x`
* i.e. `(y descendant-of x)` is true
* i.e. `descendant-of` is antonymous to `ancestor-of`
* synonymous to that, `yDx := xPy`

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

Remarks in general:

* `(#AN and #DN) <= #N`
* `(r !in DN)` - i.e. a root is no descendant
* `(l !in AN)` - i.e. a leaf is no ancestor
* a parent is an ancestor to its child nodes
* a child is a descendant to its parent node
* i.e. any edge points from an ancestor towards a descendant

With regards to `AN`:

* `AN := (N - LN)`
* i.e. `AN` and `LN` are disjoint
* a parent is an ancestor to its child nodes
* a parent may itself have one or more ancestors

With regards to `DN`:

* `DN := (N - RN)`
* i.e. `DN` and `RN` are disjoint
* a child is a descendant to its parent node
* a child may itself have one or more descendants
* `(node.children[i].parent == node)` is true

With regards to downward-oriented paths:

* `p := (n1,...,ni,...,nk)` where `(p in P)`
* `(n(i-j) ancestor-of ni)` for `(j in [1,*])`
* `(n(i+j) descendant-of ni)` for `(j in [1,*])`
