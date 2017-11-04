
# Tree (data structure)

A tree data structure is an abstract data type that represents a tree structure
using nodes and edges.

* Except for a tree's root node, each node has a single parent node.
* Each node may have any number of child nodes.
* Any parent node, that can be reached beginning with some initial node,
  is an ancestor to that node (i.e. moving upwards only).
* Any node is a descendant to all of its ancestor nodes.
* Any child node is a descendant to its parent node
  (i.e. `(node.children[i].parent = node)` is always true).
* Each node has a level value associated with it:
  `node.level = (number of ancestors) + 1`.
* A tree has no cycles.

<!-- ======================================================================= -->
## Nodes <-> Nodes

* Think in terms of tuples.

The DOM tree is a tree data structure defined in terms of nodes and edges,
i.e. we are bound by the rules of discrete mathematics (graph theory)!

* `n in N` is a node, `N` is the set of all nodes.
* A node may be a root - `r in R subset-of N`
* A node may be a parent - `p in P subset-of N`
* A node may be a child - `c in C subset-of N`
* A node may be a leaf - `l in L subset-of N`
* Edge `e := (p,c) in E subset-of PxC subset-of NxN`
* `E` only contains edges, if the corresponding nodes are connected.

The semantics of an edge `e := (p,c) in E` is such that ...

* Node `p` is the parent of node `c` - i.e. `p parent-of c`
* Node `c` is a child of node `p` - i.e. `c child-of p`
* `((p,c) in E) <=> (p parent-of c) <=> (c child-of p)`

<!-- ======================================================================= -->
## root, parent, child, leaf

* `#X = #(X) := number of entities in set X`
* `(#R,#P,#C and #L) <= #N`
* A parent always has one or more children.
* A child always has a single parent.
* A root has no parent, but may itself be one.
* A root is no child, but may itself have one or more children.
* A node is either a root or a child (i.e. parent-based view).
* `(R = (N - C)) <=> (C = (N - R))`
* A leaf is not a parent, but may itself have one.
* A leaf has no child, but may itself be one.
* A node is either a parent or a leaf (i.e. child-based view).
* `(L = (N - P)) <=> (P = (N - L))`
* A child is itself either a parent or a leaf.
* A root may be a leaf (e.g. `(#N == 1)`).

<!-- ======================================================================= -->
## a rooted, ordered tree

The DOM tree is a rooted, ordered tree data structure.

* Rooted tree - There must and can only be a single root -
  `r in (R = {r}) subset-of P`
* Ordered tree - The child nodes of a node are ordered -
  left-to-right, first-to-last
