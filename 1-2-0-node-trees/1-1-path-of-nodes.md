
<!-- ======================================================================= -->
# Paths of nodes

* (/see/ "path of vertices" /)
* a path in a tree is a path of vertices

Note that, unless specified otherwise, all paths are assumed to be oriented
according to the corresponding arborescence (i.e. uni-directional, top-down
oriented paths).

<!-- ======================================================================= -->
## set of paths P over G

Like any other endo-relation relation `R`, a tree `T := (N,E)` can be seen
to include a set of all possible paths `P` over `E` - i.e. `T := (N,E,P)`.
That is, `P` contains one or more paths for all pairs of connected nodes.

<!-- ======================================================================= -->
## uni-directional paths

Given a path `p=(n1,...,nk) in ×N^k`
such that `(ni parent-of ni+1)` for all `(i in [1,#p-1])`.

* `p` is an uni-directional, top-down/downward oriented path
* `TD` - the set of all possible top-down oriented paths
* `RD` - the set of all possible paths that begin in a root
* `TL` - the set of all possible paths that end in a leaf
* `RL` or `RTL` - the set of paths that begin in a root and end in a leaf
* `(RTL subset-of TD)` - read RTL as root-to-leaf

Note that `(P == TD)`. That is, the set of all possible paths over a tree is
identical to the set of all possible top-down oriented paths. Furthermore,
any path in `TD` is consistent with the underlying tree.

Given a path `p=(n1,...,nk) in ×N^k`
such that `(ni child-of ni+1)` for all `(i in [1,#p-1])`.

* `p` is an uni-directional, bottom-up/upward oriented path
* `BU` - the set of all possible bottom-up oriented paths
* `BR` - the set of all possible paths that end in a root
* `LU` - the set of all possible paths that begin in a leaf
* `LR` or `LTR` - the set of paths that being in a leaf and end in a root
* `(LTR subset-of BU)` - read LTR as leaf-to-root

Any such path has one direction/orientation only:

* any such path is said to be uni-directional
* i.e. all edges in an uni-directional path have the same orientation
* i.e. no `(p in TD)` has a pair of consecutive nodes
  `(ni,ni+1)` such that `(ni child-of ni+1)`
* i.e. no `(p in BU)` has a pair of consecutive nodes
  `[ni, ni+1]` such that `(ni parent-of ni+1)`

<!-- ======================================================================= -->
## rooted paths

The set of downward oriented paths, such that each path begins in a tree's root,
will be referred to as **the set of rooted paths**.

* `RP := { p | (p in TD), (p == (r,...)) }`
* `(RP == RD)`, `(RD subset-of TD)` and `(TD == P)`

Likewise, the set of rooted paths that begin in a tree's root `r` and end in a
given node `n` will be referred to as **the set of rooted paths of a node**.

* `RP(r) := { (r) }`
* `RP(n) := { p(r,n) }`
* `(RP(n) subset-of RP)`

<!-- ======================================================================= -->
## remarks

**CLARIFICATION**
Any path `(p in P)` in an arborescence represents a downward-oriented path.
In addition to that, any such path represents an ordered set of nodes.

That is because no such path contains any loops or cycles and therefore also
no repeated nodes. Because of that, the length of a path's sequence of nodes
in `P` is equal to the number of nodes in the set of its elements `E(p)` (i.e.
`(#E(p) == #p)`). Consequently, and if the index order of such a path is taken
into account, a path can be understood to define a totally ordered set of nodes.

**CLARIFICATION**
Any node `(n in N\RN)` is connected to the root `r` via a unique rooted path
`rp(n)`. Each node therefore has exactly one rooted path `rp(n)` in `P`.

That is because ...

* each rooted tree has a root `r`, and one root only
* each node `(n in N\RN)` has a parent, and one parent only
* each edge `(e in E)` is strictly downward oriented
* i.e. a tree has no loops and no cycles
* => a tree consists of a single connected component
* => only one path can be formed that begins in `r` and ends in `n`

Because of that, `rp(n)` will be referred to as **the rooted path of a node**.

* for all `(n in N)` ...
* `RP(n) := { rp(n) }`
* `(#RP == #N)`
* `(#RP(n) == 1)`
* `rPn` is true

Note that all rooted paths have finite length (i.e. `(#rp(n) <= #N)`).

**CLARIFICATION**
Any tree consists of a single connected, non-empty component.
That is because each node in a tree is connected to the root.
