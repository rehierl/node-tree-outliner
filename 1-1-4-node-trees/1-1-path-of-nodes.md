
<!-- ======================================================================= -->
# Paths of nodes

* (/see/ "path (p) over relation (R)" /)
* paths are seen as sequences of adjacent nodes
* this allows to use sequence-based definitions
* e.g. length-of, subsequence-of, prefix-of, ...
* i.e. `(s subpath-of t) := (s subsequence-of t)`

Note that, unless specified otherwise, all paths in the current discussion
are considered to be uni-directional paths consistent with the underlying
relation of an arborescence (i.e. top-down oriented paths).

<!-- ======================================================================= -->
## set of paths P over T

Like any other endo-relation relation `R`, a tree `T := (N,E)` can be seen to
have a set of all possible paths `P` associated with it - i.e. `T := (N,E,P)`.

* node-independent - two paths that have no node in common
* edge-independent - two paths that have no edge in common
* aka. node-disjoint, edge-disjoint
* node-disjoint -> edge-disjoint
* distance between nodes - the length of the shortest path
* diameter of a component - the length of the longest path

<!-- ======================================================================= -->
## multi-directional paths

A path `(p in ×N^k)` is a sequence of nodes `p := (n1,n2,...,nk)`
such that `(ni covered-by ni+1)` for `i in [1,#p-1]`.

clarifications

* `p := ()` and `p := (n)` are all considered to be a degenerated paths
* `(p[i] == p[j])` may in general be true for `(i != j)` - i.e. loops, cycles
* due to `covered-by`, a path may in general be multi-directional
* e.g. siblings are connected via multi-directional paths
* such paths are said to have no strict/consistent orientation

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

Note that `(TD == P)`. That is, the set of all possible paths over a tree
is identical to the set of all possible top-down oriented paths.

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
* i.e. no `(p in TD)` has a pair of consecutive nodes
  `(ni,ni+1)` such that `(ni child-of ni+1)`
* i.e. no `(p in BU)` has a pair of consecutive nodes
  `[ni, ni+1]` such that `(ni parent-of ni+1)`

<!-- ======================================================================= -->
## rooted paths

The set of downward oriented paths such that each path begins in a tree's root
will be referred to as **the set of rooted paths**.

* `RP := { p | (p in TD), (p == (r,...)) }`
* `(RP == RD)`, `(RD subset-of TD)` and `(TD == P)`

Likewise, the set of rooted paths that begin in a tree's root `r` and end in a
given node `n` will be referred to as **the set of rooted paths of a node**.

* `RP(r) := { (r) }`
* `RP(n) := { p(r,n) }`
* note - `(RP(n) subset-of RP)`

**CLARIFICATION**
Any path `(p in P)` in an arborescence represents a downward-oriented path
and also an ordered set of nodes.

That is because no such path contains any loops or cycles and therefore also
no repeated nodes. Because of that, the length of a path's sequence of nodes
is equal to the number of nodes in the set of its elements `E(p)` (i.e.
`(#E(p) == #p)`). Consequently, a path can be understood to define a totally
ordered set of nodes.

**CLARIFICATION**
Any node `(n in (N \ RN))` is connected to the root `r` via a unique rooted
path `rp(n)`. Each node therefore has exactly one rooted path `(rp(n) in P)`.

That is because ...

* each rooted tree has a root `r`, and one root only
* each node `(n in (N \ RN))` has a parent, and one parent only
* a tree also has no loops and no cycles
* => a tree consists of a single connected component
* => only one path can be formed that begins in `r` and ends in `n`

Because of that, `rp(n)` will be referred to as **the rooted path of a node**.

* `(#RP == #N)`
* `(#RP(n) == 1)` for all `(n in N)`
* `rPn` holds for all `(n in N)`
* `(#rp(n) <= #N)`
* i.e. all rooted paths have finite length
