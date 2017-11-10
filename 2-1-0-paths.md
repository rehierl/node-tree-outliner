
# Paths

A path `p` is a sequence of nodes such that `p=(n1,n2,...,nk) in Nx...xN`,
and `ni parent-of ni+1` or `ni child-of ni+1`
for `i in [1,k-1]`, `k in [2,+Infinity)`.

Any definition based on sequences also apply to paths:

* `#p` := length of a path
* `p(n)` := the n-th node of a path
* `(t = s)`, `(t != s)`, `(t === s)`, `(t !== s)`
* `t subsequence-of s`
* `t prefix-of s`, `u prefix-of s,t`
* `t suffix-of s`, `u suffix-of s,t`
* (|strictly|loosely) pre-, sub-, in-sequent entries
* see [sequences]()

<!-- ======================================================================= -->
## miscellaneous

In general, paths `p1` and `p2` are not necessarily identical if they share a
common prefix and a common suffix: `p1=(p1,...,pA,i1,...,iB,s1,...,sC)`, 
`p2=(p1,...,pA,j1,...,jD,s1,...,sC)` for `B and D in [0,+Infinity)`. They might
still contain different subsequences (i.e. `(B > 0)` and/or `(D > 0)`).

<!-- ======================================================================= -->
## uni-directional paths

For any path `p=(n1,n2,...,nk) in Nx...xN` such that
`ni parent-of ni+1` (i.e. top-down) for `i in [1,k-1]`, `k in [2,+Infinity)`,
`ni` is an ancestor of `ni+j` and `ni+j` a descendant of `ni` for `j in [i+1,k]`.

* `TD` represents the set of all top-down paths (= downwards)
* `RD` - any such path that begins in a root (`ni in R`)
* `TL` - any such path that ends in a leaf (`nk in L`)
* `RL` or `RTL` - any such path that begins in a root and ends in a leaf
* `RTL subset-of TD` - read RTL as root-to-leaf

For any path `p=(n1,n2,...,nk) in Nx...xN` such that
`ni child-of ni+1` (i.e. bottom-up) for `i in [1,k-1]` and `k in [2,+Infinity)`,
`ni` is a descendant of `ni+j` and `ni+j` an ancestor of `ni` for `j in [i+1,k]`.

* `BU` represents the set of all bottom-up paths (= upwards)
* `BR` - any such path that ends in a root (`nk in R`)
* `LU` - any such path that begins in a leaf (`ni in L`)
* `LR` or `LTR` - any such path that beings in a leaf and ends in a root
* `LTR subset-of BU` - read LTR as leaf-to-root

Any such path has one direction only (i.e. any such path is uni-directional)!

* No `p in TD` has a pair of nodes `(ni, ni+1)` such that
  `ni child-of ni+1`, or `ni descendant-of ni+j`
* No `p in BU` has a pair of nodes `(ni, ni+1)` such that
  `ni parent-of ni+1`, or `ni ancestor-of ni+j`

Also

* `E in TD`, but `not in BU`.
* `p in RD` <=> `p` is a **rooted path**
* A tree has **no cycles**, if `p(i) != p(j)`
  for `i,j in [1,k]`, `i != j` and any `p in TD or BU`.

<!-- ======================================================================= -->
## undirected definitions

* `n1` is strictly related to `nk`, if `p=(n1,nk) in TD or BU`
* `n1` is loosely related to `nk`, if `p=(n1,n2,n3,...,nk) in TD or BU`
  and `k in [3,+Infinity)`
* `n1` is related to `nk`, if `n1` is strictly or loosely related to `nk`
* synonymous - related to, connected with, in relationship with, coupled with

in simple words:

* strictly => connected, and there are no nodes in between
* loosely => connected, but there are some nodes in between
* (none) => a path exists such that both are nodes connected -
  with or without other nodes in between

<!-- ======================================================================= -->
## directed definitions

* any path `p in TD` points downwards
* `n1` contains `nk`, if `p=(n1,...,nk) in TD`
* synonymous - contains, is ancestor of
* any path `p in BU` points upwards
* `n1` is located inside `nk`, if `p=(n1,...,nk) in BU`
* synonymous - located inside of, is descendant of

<!-- ======================================================================= -->
## examples

downwards

* A parent is related to all of its descendants.
* A parent is strictly related to its children.
* A parent is loosely related to any node `n in (descendants - children)`.
* A parent contains its descendant nodes.
* A parent strictly contains its child nodes.

upwards

* A child is related to all of its ancestors.
* A child is strictly related to its parent.
* A child is loosely related to any node `n in (ancestors - parent)`.
* A child is located inside of its ancestor nodes.
* A child is strictly located inside of its parent node.

undirected, single root

* The root is related to any other node.
* Any other node is related to the root.

