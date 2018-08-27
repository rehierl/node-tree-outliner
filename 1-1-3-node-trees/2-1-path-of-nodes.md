
<!-- ======================================================================= -->
# Paths of nodes

* (/see/ "path (p) over relation (R)" /)
* paths are understood as sequences of adjacent nodes
* which allows to use sequence-based definitions
* e.g. length-of, subpath-of, prefix-of, ...

Note that, unless specified otherwise, all paths in the current discussion
are considered to be uni-directional paths consistent with the relation of
an arborescence (i.e. top-down oriented paths).

<!-- ======================================================================= -->
## multi-directional paths

A path `p` is a sequence of nodes `p := [n1,n2,...,nk] in ×N^k`
such that `(ni covered-by ni+1)` for `i in [1,#p-1]`.

clarifications

* `p := [n1]` is considered to be a degenerated path
* `(p[i] == p[j])` may be true for `(i != j)` - i.e. loops, cycles
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
* `RD` - any path that begins in a root (`n1 in RN`), i.e. any rooted path
* `TL` - any path that ends in a leaf (`nk in LN`)
* `RL` or `RTL` - any path that begins in a root and ends in a leaf
* `(RTL subset-of TD)` - read RTL as root-to-leaf

Given a path `p=[n1,...,nk] in ×N^k`
such that `(ni child-of ni+1)` for any `(i in [1,#p-1])`.

* `p` is an uni-directional, bottom-up/upward oriented path
* `ni` is a descendant of `ni+j`, and `ni+j` is an ancestor of `ni`
* `BU` - represents the set of all possible bottom-up paths
* `BR` - any path that ends in a root (`nk in RN`)
* `LU` - any path that begins in a leaf (`n1 in LN`)
* `LR` or `LTR` - any path that beings in a leaf and ends in a root
* `(LTR subset-of BU)` - read LTR as leaf-to-root

Any such path has one direction/orientation only:

* any such path is said to be uni-directional
* i.e. no `(p in TD)` has a pair of nodes `[ni, ni+1]`
  such that `(ni child-of ni+1)`, or `(ni descendant-of ni+j)`
* i.e. no `(p in BU)` has a pair of nodes `[ni, ni+1]`
  such that `(ni parent-of ni+1)`, or `(ni ancestor-of ni+j)`

**CLARIFICATION**
The path `rp(n) := [r,...,n] in RD` that begins in a tree's root `r` and ends
in a given node `n` will be referred to as **the rooted path of a node**.

* `(rp(n)[1] == r)` - any rooted path begins with the tree's root
* `rp(r) := [r]` - i.e. `rp(r)` is the only rooted path that has length 1
* each node `n` in a tree has a unique rooted path `rp(n)`

**CLARIFICATION**
Any unidirectional path in an arborescence represents an ordered set of nodes.

That is because no such path contains any loops or cycles and therefore also no
repeated nodes. Because of that, the length of a path's node sequence is equal
to the number of nodes in the set of its elements `E(p)` (i.e. `(#p == #E(p))`).
Consequently, a path can be understood to define a totally ordered set of nodes.

<!-- ======================================================================= -->
## general definitions

* `xPy` is true, if a path can be formed over the underlying relation `R`
* i.e. the relation has edges that allow to connect node `x` with node `y`
* `P` can be seen to represent the set of all possible paths over `R`

node-to-node

* `p(a,b), path(a,b) := [a,...,b]`
* the uni-directional path that begins in `a` and ends in `b`
* `path(a,a) := [a]` - note that trees are acyclic
* may be undefined if `a` is unrelated to `b`

node-to-set

* `p(a,B), path(a,B) := { path(a,b) | for all (b in B) }`
* the set of uni-directional paths that begin in `a` and end in `B`
* may be the empty set, if there is no `b` related to `a`

loops and cycles

* loop - a path such that `p := [a,a]` (i.e. `aEa`)
* cycle - a path such that `p := [a,...,a]` (i.e. `aPa`)
* 1-cycle - a cycle of length one - `p := [a,a]`
* 2-cycle - a cycle of length two - `p := [a,b,a]`

sets of paths

* vertex-independent - two paths that have no vertex in common
* edge-independent - two paths that have no edge in common
* aka. vertex-disjoint, edge-disjoint
* vertex-disjoint -> edge-disjoint
* distance between vertices - the length of the shortest path
* diameter of a component - the length of the longest path

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
