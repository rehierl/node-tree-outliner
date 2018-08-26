
<!-- ======================================================================= -->
# Paths

* (/see/ "path P over relation R" /)
* paths are understood as sequences of adjacent nodes
* which allows to use sequence-based definitions
* e.g. length-of, subpath-of, prefix-of, ...

<!-- ======================================================================= -->
## multi-directional paths

A path `p` is a sequence of nodes `p := [n1,n2,...,nk] in ×N^k`
such that `(ni covered-by ni+1)` for `i in [1,#p-1]`.

clarifications

* `p := [n1]` is considered to be a degenerated path
* `(p[i] == p[j])` may be true for `(i != j)`
* due to `covered-by`, a path may in general be multi-directional
* e.g. siblings are connected via multi-directional paths
* such paths are said to have no consistent orientation

<!-- ======================================================================= -->
## uni-directional paths

Given a path `p=[n1,...,nk] in ×N^k`
such that `(ni parent-of ni+1)` for any `(i in [1,#p-1])`.

* `p` is an uni-directional, top-down/downward oriented path
* `ni` is an ancestor of `ni+j`, and `ni+j` is a descendant of `ni`
* `TD` - represents the set of all possible top-down paths
* `RD` - any path that begins in a root (`n1 in R`), i.e. any rooted path
* `TL` - any path that ends in a leaf (`nk in L`)
* `RL` or `RTL` - any path that begins in a root and ends in a leaf
* `(RTL subset-of TD)` - read RTL as root-to-leaf

Given a path `p=[n1,...,nk] in ×N^k`
such that `(ni child-of ni+1)` for any `(i in [1,#p-1])`.

* `p` is an uni-directional, bottom-up/upward oriented path
* `ni` is a descendant of `ni+j`, and `ni+j` is an ancestor of `ni`
* `BU` - represents the set of all possible bottom-up paths
* `BR` - any path that ends in a root (`nk in R`)
* `LU` - any path that begins in a leaf (`n1 in L`)
* `LR` or `LTR` - any path that beings in a leaf and ends in a root
* `(LTR subset-of BU)` - read LTR as leaf-to-root

Any such path has one direction/orientation only!

* any such path is said to be uni-directional
* i.e. no `(p in TD)` has a pair of nodes `[ni, ni+1]`
  such that `(ni child-of ni+1)`, or `(ni descendant-of ni+j)`
* i.e. no `(p in BU)` has a pair of nodes `[ni, ni+1]`
  such that `(ni parent-of ni+1)`, or `(ni ancestor-of ni+j)`

**CLARIFICATION**
Any unidirectional path in a tree of nodes (no loops, no cycles)
is an ordered sequence of nodes.

<!-- ======================================================================= -->
## general definitions

* `xPy` is true, if such a path exists over the underlying relation

node-to-node

* `p(a,b), path(a,b) := [a,...,b]`
* the uni-directional path that begins in `a` and ends in `b`
* `path(a,a) := [a]` - note that trees are acyclic
* may be undefined if `a` is unrelated to `b`

node-to-set

* `p(a,B), path(a,B) := { path(a,b) | for all (b in B) }`
* the set of uni-directional paths that begin in `a` and end in `B`
* may be the empty set, if there is no `b` related to `a`

**CLARIFICATION**
The path `rp(n) := [r,...,n] in RD` of a node `n` that begins in a tree's root
will be referred to as **the rooted path of a node**. Every node `n` in a tree
has a unique rooted path `rp(n)`.

* `(rp(n)[1] == r)` - any rooted path begins with the tree's root
* `rp(r) := [r]` - i.e. `rp(r)` is the only rooted path that has length 1

<!-- ======================================================================= -->
## directed/undirected definitions

* the definitions in "path over relation" apply
* i.e. related-to, covered-by, connected-to, ...

away from the root

* any path `(p in TD)` points **downwards**
* `n1` **contains** `nk`, if `p=[n1,...,nk] in TD`
* synonymous - contains, is ancestor of

towards the root

* any path `(p in BU)` points **upwards**
* `n1` is **located inside of** `nk`, if `p=[n1,...,nk] in BU`
* synonymous - located inside of, is descendant of

<!-- ======================================================================= -->
## examples

downwards

* a parent is related to all of its descendants
* a parent is strictly related to its children
* a parent is loosely related to any node `n in (descendants - children)`
* a parent strictly contains its child nodes
* a parent contains its descendant nodes

upwards

* a child is related to all of its ancestors
* a child is strictly related to its parent
* a child is loosely related to any node `n in (ancestors - parent)`
* a child is strictly located inside of its parent node
* a child is located inside of its ancestor nodes

undirected, single root

* the root is related to any other node
* any other node is related to the root
