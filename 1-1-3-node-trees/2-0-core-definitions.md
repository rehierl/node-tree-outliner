
<!-- ======================================================================= -->
# Node tree definitions

* core definitions used throughout this discussion
* a summary of standard and non-standard definitions
* the focus is on directed node trees

<!-- ======================================================================= -->
## subsets of nodes

* `N` is the set of all nodes
* the following sets are all subsets of `N`
* `r in RN` - the set of all root nodes
* `p in PN` - the set of all parent nodes
* `c in CN` - the set of all child nodes
* `l in LN` - the set of all leaf nodes
* `a in AN` - the set of all ancestor nodes
* `d in DN` - the set of all descendant nodes

<!-- ======================================================================= -->
## tree, forest

* the definition of parent/leaf is child-based -
  i.e. a parent is a node that has one or more child nodes
* a tree has no loops and no cycles (i.e. acyclic)
* a tree always has exactly one root node -
  i.e. `(#RN == 1)`, `(#N >= 1)`
* a tree always has one or more nodes - i.e. never empty
* a forest is the union of disjoint trees

<!-- ======================================================================= -->
## semantics of E

* edge `e := [p,c] in E subset-of P×C subset-of N×N`
* the direction of any edge is top-down

the semantics of an edge `e := [p,c] in E` is such that ...

* node `p` is the parent of node `c` - i.e. `(p parent-of c)`
* node `c` is a child of node `p` - i.e. `(c child-of p)`
* `pEc <-> (p parent-of c) <-> (c child-of p)`
* `sem(E)` := "parent-of", not "child-of"

clarification

* turn the edges of a directed tree upside-down
* and you will have the "child-of" semantics
* that directed graph, if non-empty, always has
  one or more roots and no more than one leaf
* i.e. that directed graph, if non-linear, is not a tree

<!-- ======================================================================= -->
## root, parent, child, leaf

* `(#RN, #PN, #CN and #LN) <= #N`
* a parent always has one or more child nodes
* a child has one parent only
* a root has no parent, but may itself be one
* a root is no child, but may itself have multiple child nodes
* a root may be a leaf (e.g. `(#N == 1)`)

a child-based view - i.e. with regards to a node's children

* `PN := (N - LN)`
* i.e. `PN` and `LN` are disjoint
* a node is either a parent ex-or a leaf
* a parent has child nodes, a leaf does not

a parent-based view - i.e. with regards to a node's parent

* `RN := (N - CN)`
* i.e. `RN` and `CN` are disjoint
* a node is either a root ex-or a child
* a leaf is not a parent, but may itself have one
* a leaf has no child, but may itself be one

<!-- ======================================================================= -->
## ancestors, descendants

* `(#AN and #DN) <= #N`

the set of all ancestors

* `AN := (N - LN)`
* i.e. `AN` and `LN` are disjoint
* a parent is an ancestor to its child nodes
* a parent may itself have one or more ancestors
* an ancestor is no leaf

ancestors of a node

* `A(n)` := the set of all ancestors of node `n`
* `(A(n) subset-of A)` is always true

the set of all descendants

* `DN := (N - RN)`
* i.e. `DN` and `RN` are disjoint
* a child is a descendant to its parent node
* a child may itself have one or more descendants
* `(node.children[i].parent == node)` is always true
* a descendant is no root

descendants of a node

* `D(n)` := the set of all descendants of node `n`
* `(D(n) subset-of D)` is always true

<!-- ======================================================================= -->
## children, siblings

* `parentOf(c)` := the parent node `p` of child node `c`
* `(x sibling-of y) := (parentOf(x) == parentOf(y))`
* i.e. siblings have the same parent node

siblings

* `x` is a sibling to `y`, if `pEx` and `pEy`, where `p` is parent of `x` and `y`
* not right-euclidean - `pEa` and `pEb`, but neither `aEb` nor `bEb` (???)
* `(x sibling-of y) <-> (y sibling-of x)`

<!-- ======================================================================= -->
## tree-order, ordered tree

tree-order (graph theory)

* a partial ordering on the vertices, such that ...
  `(v < w)` if there is a rooted path `rp := [r..v..w]`

ordered tree (graph theory)

* an ordered tree is a rooted tree, such that ...
  each parent node has a first and a last child

Note that the set of child nodes of a parent node can be sequentialized into
the parent's linear sequence of child nodes `cs := cs(p)`. The first node in
`cs[1]` is the parent's first child, the last node `cs[#cs]` the parent's last
child and the n-th node `cs[n]` the parent's n-th child node.

* `(c first-child-of p) := (c == cs(p)[1])`
* `(c last-child-of p) := (c == cs(p)[#cs(p)])`
* `(x < y) := (idx(cs(p),x) < idx(cs(p),y))`
* `(x < y) ex-or (y < x)` for two distinct nodes `x,y in cs(p)`

<!-- ======================================================================= -->
## next/previous sibling

* given an ordered tree ...

first/last child

* `(c first-child-of p)` := `p` has no other child `d` such that `(d < c)`
* `(c last-child-of p)` := `p` has no other child `d` such that `(c < d)`

previous/next sibling

* `(x previous-sibling-of y)` := `x` is the previous sibling of `y`, if
  `(x < y)`, and if there is no other sibling `z` such that `(x < z < y)`
* `(x next-sibling-of y)` := `x` is the next sibling of `y`, if
  `(y < x)`, and if there is no other sibling `z` such that `(y < z < x)`
* `(x previous-sibling-of y) <-> (y next-sibling-of x)`

presequent/subsequent sibling

* `(x presequent-sibling-of y) := (x < y)`
* `(x subsequent-sibling-of y) := (y < x)`
* `(x presequent-sibling-of y) <-> (y subsequent-sibling-of x)`

<!-- ======================================================================= -->
## document-/enter-order

* an ordering on the vertices of a tree, such that ...
* req-1: `(p < n)` - any node `n` is subsequent to its parent
* req-2: `(s < n)` - any node `n` is subsequent to its presequent siblings

Note that the document-order has the same characteristics as the tree-order,
if the tree is an unordered tree of nodes.

Note that the document-order is a combination of the tree-order and the child
order in an ordered tree. That is, the document-order preserves the tree-order.

Note that the pre-order DFS traversal of a tree will enter the nodes in
document-order. Because of that, the document-order may also be referred
to as the enter-order.

<!-- ======================================================================= -->
## level, depth, height

* `level(n) := (#rp(n) - 1)` - the node level of a node
* `depth(n) := (#rp(n) - 1)` - the depth of a node
* i.e. `(level/depth(root) == 0)`

height of a node/tree

* `height(n) := maxIn({ #p | (p in path(n,L)) }) - 1`
* i.e. the length of the longest node-to-leaf path, minus one
* `height(tree) := height(r)` - the height of a tree is the height of its root
* i.e. `(height(leaf) == 0)`
