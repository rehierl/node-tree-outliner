
<!-- ======================================================================= -->
# Related nodes

A tree of nodes is most commonly defined by a set of nodes and by a parent-child
relationship between those nodes (i.e. `G := (N,E)`).

Because a rooted tree can only have a single root node, the 1st node of each
edge refers to the parent node and the 2nd node to a child node to which the 1st
node is a parent (i.e. `e := (p,c)`). In other words, all edges point from a
parent node towards a child node.

This top-down orientation is necessary because the inverted set of edges `E'`
defines a graph that contains multiple root nodes, but only a single leaf.

Strictly, the parent-child relationship of a tree defines which nodes are in
direct/strict relationship with another node. Consequently, there is no strict
relationship between nodes `a` and `c` (i.e. `!aRc`), even if `aRb` and `bRc`.
That is, the parent-child relationship defined by the set of edges `E` is itself
not transitive (i.e. `aRb and bRc => aRc`).

* `a strictly-related-to b`, if `aEb` or `bEa`
* `a` and `b` are strictly related to each other

Even if grandchildren are not strictly related to their grandparents, nodes `a`
and `c` are nonetheless related with each other because `E` allows to define a
path that connects both nodes (i.e. `p=(a,b,c)`).

* `p loosely-related-to d`, if a path exists
  such that `path=(p,...,d)` where `(pi,pi+1) in E or E'`
* `a` and `d` are loosely related to each other

antonymous semantics

* `parent-of` <=> `child-of`
* `contains` <=> `element-of`

notes
