
<!-- ======================================================================= -->
# Tree of nodes

* a tree data structure represents a tree structure using nodes and edges
* a tree is a connected graph
* a forest is a disjoint union of trees

undirected tree

* undirected graph
* connected with no cycles
* acyclic and a cycle is formed if any edge is added
* no longer connected, if any edge is removed

rooted tree

* one node is designated as the root
* directed rooted tree - all edges point away from the root - an arboresence
* if arboresence also referred to as branching or out-tree
* if the edges point towards the root - anti-aboresence or in-tree

rooted tree

* except for the root, each node has a single parent node
* each node may have any number of child nodes
* any parent node, that can be reached beginning with an initial node,
  is an ancestor to that node - only when moving upwards on a path only
* any node is a descendant to its ancestor nodes
* any child node is descendant to its parent node -
  i.e. `(node.children[i].parent == node)` is always true
* each node has a level value associated with it -
  i.e. `node.level == (number of ancestors) + 1`.

<!-- ======================================================================= -->
## nodes <-> nodes

* `n in N` is a node, `N` is the set of all nodes
* a node may be a root - `r in R subset-of N`
* a node may be a parent - `p in P subset-of N`
* a node may be a child - `c in C subset-of N`
* a node may be a leaf - `l in L subset-of N`
* edge `e := (p,c) in E subset-of PxC subset-of NxN`

the semantics of an edge `e := (p,c) in E` is such that ...

* node `p` is the parent of node `c` - i.e. `p parent-of c`
* node `c` is a child of node `p` - i.e. `c child-of p`
* `pEc <=> (p parent-of c) <=> (c child-of p)`

<!-- ======================================================================= -->
## root, parent, child, leaf

* `(#R,#P,#C and #L) <= #N`
* a parent always has one or more children
* a child always has a single parent
* a root has no parent, but may itself be one
* a root is no child, but may itself have one or more children
* a node is either a root or a child (i.e. parent-based view)
* `(R == (N - C)) <=> (C == (N - R))`
* a leaf is not a parent, but may itself have one
* a leaf has no child, but may itself be one
* a node is either a parent or a leaf (i.e. child-based view)
* `(L == (N - P)) <=> (P == (N - L))`
* a child is itself either a parent or a leaf
* a root may be a leaf (e.g. `(#N == 1)`)

<!-- ======================================================================= -->
## ordered tree

* an ordered tree in which the child nodes of a node are ordered
* the children of each node are lower than the node itself -
  i.e. with regards to the node's level

put differently

* the edges `e` of a directed, rooted and ordered tree can be thought of as
  being elements of a sequence `s` such that ...
* `(a,b) < (b,cx)` and `(b,cx) < (b,cy)` for `(x < y)`

first/last child

* `cy` first child of `p` := there is no `cx` such that `(p,cx) < (p,cy)`
* `cx` last child of `p` := there is no `cy` such that `(p,cx) < (p,cy)`

sibling

* `x` is a sibling of `y`, if `xEy` and `yEx`
* not right-euclidean - `pEa` and `pEb`, but neither `aEb` nor `bEb`
* `(x sibling-of y) <=> (y sibling-of x)`

clarification

* e.g. `s := [a,...,e,f,g,...,k]`
* all nodes within `s` are direct child nodes of some parent node `p` -
  i.e. `(p,s(i)) in E` for any `i in [1,n]` and `(n == #s)`
* `s1` represents the first child and `sn` the last child of parent `p`

previous/next sibling

* `si` is the previous sibling of `sj` := `si` is sequent to `sj`, and
  there is no sequent sibling `sk` subsequent to `si` and presequent to `sj` -
  i.e. `(si < sk < sj)`
* `(x previous-sibling-of y) <=> (y next-sibling-of x)`

presequent/subsequent sibling

* `sj` is a subsequent sibling of `si` := `si` is sequent to `sj` and `(si < sj)`
* `(si presequent-sibling-of sj) <=> (sj subsequent-sibling-of si)`