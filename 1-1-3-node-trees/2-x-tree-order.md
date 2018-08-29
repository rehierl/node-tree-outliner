
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

