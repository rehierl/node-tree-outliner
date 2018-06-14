
<!-- ======================================================================= -->
# Paths

A path `p` is a sequence of nodes `p := (n1,n2,...,nk) in xN^k`
such that `ni parent-of ni+1` or `ni child-of ni+1`
for `i in [1,k-1]`, `k in [2,*]`.

Any definition based on sequences also apply to paths:

* `#p` := length of a path
* `p(n)` := the n-th node of a path
* `(t == s)`, `(t != s)`, `(t === s)`, `(t !== s)`
* `t subsequence-of s`
* `t prefix-of s`, `u prefix-of s,t`
* `t suffix-of s`, `u suffix-of s,t`
* (strictly|loosely)? pre-, sub-, in-sequent entries

Note that paths `p1` and `p2` are not necessarily identical if they share
a common prefix and a common suffix: `p1=(p1,...,pA,i1,...,iB,s1,...,sC)`, 
`p2=(p1,...,pA,j1,...,jD,s1,...,sC)` for `B and D in [0,+Infinity)`.
They might still differ in an infix (i.e. `(B > 0)` and/or `(D > 0)`).

<!-- ======================================================================= -->
## uni-directional paths

Given a path `p=(n1,...,nk) in xN^k`
such that `ni parent-of ni+1` for `i in [1,#p-1]`.

* `p` is a top-down/downwards oriented path
* `ni` is an ancestor of `ni+j`, and `ni+j` is a descendant of `ni`
* `TD` - represents the set of all possible top-down paths
* `RD` - any such path that begins in a root (`n1 in R`), i.e. any rooted path
* `TL` - any such path that ends in a leaf (`nk in L`)
* `RL` or `RTL` - any such path that begins in a root and ends in a leaf
* `RTL subset-of TD` - read RTL as root-to-leaf

Given a path `p=(n1,...,nk) in xN^k`
such that `ni child-of ni+1` for `i in [1,#p-1]`.

* `p` is a bottom-up/upwards oriented path
* `ni` is a descendant of `ni+j`, and `ni+j` is an ancestor of `ni`
* `BU` - represents the set of all possible bottom-up paths
* `BR` - any such path that ends in a root (`nk in R`)
* `LU` - any such path that begins in a leaf (`n1 in L`)
* `LR` or `LTR` - any such path that beings in a leaf and ends in a root
* `LTR subset-of BU` - read LTR as leaf-to-root

clarification

* `(p,c) in E in TD`, but `E not in BU`
* the edges of a tree are top-down paths
* i.e. `p parent-of c`, not `p child-of c`

Any such path has one direction only!

* any such path is uni-directional
* no `p in TD` has a pair of nodes `(ni, ni+1)` such that
  `ni child-of ni+1`, or `ni descendant-of ni+j`
* no `p in BU` has a pair of nodes `(ni, ni+1)` such that
  `ni parent-of ni+1`, or `ni ancestor-of ni+j`

A path based upon relation x

* any path `p in TD` is said to be a path based upon the `parent-of` relation
* any path `p in BU` is said to be a path based upon the `child-of` relation
* one could also state "a path based upon `E` (or `E'`)"

<!-- ======================================================================= -->
## loops, cycles

* a path `p in TD` has loops, if `(p(i) == p(i+1))`
* a path `p in TD` has cycles, if `(p(i) == p(j))` for some `i,j in [1,#p]`
* i.e. a cyclic path may have loops

clarification

* a tree is defined to not contain any loops or cycles
* therefore, any uni-directional path contains its nodes once, or not at all
* this also applies to any path `p in BU`

<!-- ======================================================================= -->
## undirected definitions

* `n1` is strictly related to `nk`,
  if `p=(n1,nk) in TD or BU`
* `n1` is loosely related to `nk`,
  if `p=(n1,...,nk) in TD or BU` and `#p in [3,*)`
* `n1` is related to `nk`, if `n1` is strictly or loosely related to `nk`
* synonymous - related to, connected with, in relationship with, coupled with

in words:

* strictly -> connected, and there are no nodes in between
* loosely -> connected, but there are some nodes in between
* (none) -> a path exists such that both are nodes connected -
  with or without other nodes in between

<!-- ======================================================================= -->
## directed definitions

away from the root, i.e. downwards

* any path `p in TD` points downwards
* `n1` contains `nk`, if `p=(n1,...,nk) in TD`
* synonymous - contains, is ancestor of

towards the root, i.e. upwards

* any path `p in BU` points upwards
* `n1` is located inside of `nk`, if `p=(n1,...,nk) in BU`
* synonymous - located inside of, is descendant of

<!-- ======================================================================= -->
## examples

downwards

* a parent is related to all of its descendants
* a parent is strictly related to its children
* a parent is loosely related to any node `n in (descendants - children)`
* a parent contains its descendant nodes
* a parent strictly contains its child nodes

upwards

* a child is related to all of its ancestors
* a child is strictly related to its parent
* a child is loosely related to any node `n in (ancestors - parent)`
* a child is located inside of its ancestor nodes
* a child is strictly located inside of its parent node

undirected, single root

* the root is related to any other node
* any other node is related to the root
