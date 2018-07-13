
<!-- ======================================================================= -->
# The NxN relation

A tree of nodes is defined by a set of nodes `N` and by a set of edges `E`. The
edges as a whole define a parent-child relationship on top of all the nodes:

* `R := (A,B,G)` => `G := (V,V,E)` => `T := (N,E)`
* binary relation `R`, graph `G`, tree `T`
* sets of elements `A,B`, set of vertices `V`, set of nodes `N`
* where `(A == B == V == N)`

Note that a binary relation `R` may in general have different sets of elements
`A` and `B` (i.e. `(A != B)`).

<!-- ======================================================================= -->
## (p parent-of c)

The 1st node of each edge (i.e. `e := (p,c) in E`) refers to a parent node and
the 2nd node to a child node. Obviously, the parent node `p` is said to be the
parent of child `c`. Therefore, all edges have an orientation (aka. direction)
from a parent node towards a child node.

* `T := (N,E)` where `N` is the set of all nodes
* `E := { (p,c) : (p in N), (c in N), (p parent-of c) }`
* `sem(T) := (p parent-of c)`

This `parent-of` relation will be referred to as the `NxN` relation of the tree.

* `sem(T)` refers to the semantics of the tree's relation
* `pEc` is true, if `(p,c) in E`
* `!pEc` is true, if `(p,c) not in E`

Note that a parent is said to be superordinate to its subordinate child.
Because of that, the `parent-of` relation has a top-down/downward direction.

<!-- ======================================================================= -->
## (c child-of p)

The directed and strict top-down orientation (i.e. away from the root node
towards a leaf node) of the `parent-of` relation is necessary because the
inverted set of edges `E'` defines a graph that contains multiple root nodes
(the former leaf nodes), but only a single leaf node (the former root node).

formal definition

* `R' := (N,N,E')` where `N` is the set of all nodes
* `E' := { (c,p) : (c in N), (p in N), (p parent-of c) }`
* `sem(R') := (c child-of p)`

simple definition

* `(c child-of p)`, if `pEc`
* in words: "node `c` is a child of node `p`"

As such, this `child-of` relation is said to be antonymous to the above
`parent-of` relation, i.e. `(R == ant(tree))`.

* antonymous <=> inverted edges/tuples/sequences *and* inverted semantics

Note that the `child-of` relation has a bottom-up/upward direction.

<!-- ======================================================================= -->
## (a related-to b)

The above `parent-of` relation defines which nodes are in direct/strict
relationship with another node.

* `(a strictly-related-to b)`, if `aEb` or `bEa`
* `a` is directly/strictly related to `b`
* `(a strictly-related-to b) <=> (b strictly-related-to a)`

However, there is no such strict relationship between two nodes `a` and `c`
(i.e. `!aEc`) if `aEb` and `bEc` (if that were the case, then `c` would have
two parent nodes `a` and `b`). Consequently, the `parent-of` relation of a
tree is not transitive.

Even if grandparents are not strictly related to their grandchildren, nodes `a`
and `c` are nonetheless considered to be related with each other. That is
because `E` allows to define a path that connects both nodes (e.g. `p=(a,b,c)`
if `aEb` and `bEc`).

* `(a loosely-related-to b)`, if a path `p=(a,..,b)` or `p=(b,..,a)`
  exists such that `(#p > 2)` and all pairs `(pi,pi+1) in E`
* `a` and `b` are loosely related with each other
* i.e. an uni-directional path can be defined that connects both nodes
* `(a loosely-related-to b) <=> (b loosely-related-to a)`

Note that a path of nodes is said to be uni-directional, if (and only if) the
same set of edges `E` was used to construct the whole path. A path is said to
be multi-directional, if it is based upon two or more sets of edges that differ
in orientation (e.g. `E` and `E'`).

To be more accurate, whether a path is uni- or multi-directional depends on the
orientation of the sets of edges involved. If all sets involved have the same
orientation, then a path is said to be uni-directional. Otherwise, a path is
multi-directional.

The strict and loose relationship can be generalized into:

* `(a related-to b)`, if `(a strictly-related-to b)`
  or `(a loosely-related-to b)`
* `a` and `b` are related with each other
* `(a related-to b) <=> (b related-to a)`
* synonymous - `related-to`, `associated-with`

Note that the `related-to` relation has no orientation.
As such, it is understood to be un-directional.

<!-- ======================================================================= -->
## (a ancestor-of n)

Without any relationship between a node and its grandparents and grandchildren,
there would be no reason to have the dedicated terms "grand-parent" and
"grand-child". Similarly, there would be no reason to generalize these terms
into "ancestor" and "descendant":

* `(a ancestor-of n)`, if a path `p=(a,...,n)` exists
  such that `(#p > 1)` and all pairs `(pi,pi+1) in E`
* `(d descendant-of n)`, if a path `p=(n,...,d)` exists
  such that `(#p > 1)` and all pairs `(pi,pi+1) in E`

<!-- ======================================================================= -->
## (s sibling-of n)

Similar to ancestor and descendant nodes, a relationship does exist between
two siblings `s` and `n`, even though there is no such edge in `E` (i.e. `!sEn`
and `!nEs`). In addition to that, no uni-directional path can be defined that
connects both nodes. That is because the path would have to go up to the
common parent node and then down to the corresponding sibling.

* `(s sibling-of n)`, if `pEs` and `pEn`
* i.e. `(p parent-of s)` and `(p parent-of n)`
* `(s sibling-of n) <=> (n sibling-of s)`
* Note that `(n sibling-of n)` is always true under that definition.

In addition to that, an ordered tree requires that there is an order of
sorts on the set of child nodes (i.e. `((s < n) or (n < s))` is always
true if `(s != n)` and `(s sibling-of n)`).

A node has a first and a last child, if it is a parent node.

* `(c first-child-of p)`, if `c` has no sibling `s` such that `(s < c)`
* `(c last-child-of p)`, if `c` has no sibling `s` such that `(c < s)`

A node may have presequent and subsequent siblings:

* `(x presequent-sibling-of y)`, if `(x sibling-of y)` and `(x < y)`
* `(y subsequent-sibling-of x) <=> (x presequent-sibling-of y)`

A node may have a previous and a next sibling:

* `(x previous-sibling-of y)`, if `(x sibling-of y)`, `(x < y)` and
  there is no other sibling `z` such that `(x < z < y)` -
  i.e. `z` is subsequent to `x` and presequent to `y`
* `(y next-sibling-of x) <=> (x previous-sibling-of y)`

Note that it is assumed that the overall order of nodes also defines the order
of parent nodes with regards to their child nodes:

* `(p < c)`, if `(p parent-of c)`

and consequently

* `(p < d)`, if `(p descendant-of d)`

Note also, that all nodes are ordered according to the same order, regardless
of which entities these nodes represent. That is, the nodes of a tree are not
split into one or more groups which are then ordered independent of each other
(e.g. the display of a file-system: first the folders, then the files).

<!-- ======================================================================= -->
## (p contains c)

Based on the above `parent-of` relation of a tree, the tree's `contains`
relation can be defined as follows:

* `R := (N,N,G)`
* `G := { (p,c) : pEc }`
* `sem(R) := (p contains c)`

As such, the `contains` relation is equivalent to the `parent-of` relation.
That is, the `contains` relation also has a top-down orientation.

* `(a strictly-contains b)`, if `aEb`
* `(a loosely-contains b)`, if a path `p=(a,..,b)`
  exists such that `(#p > 2)` and all pairs `(pi,pi+1) in E`
* `(a contains b)`, if `(a strictly-contains b)` or `(a loosely-contains b)`

In addition to that:

* `(b belongs-to a)`, if `aEb`
* `(b belongs-to a)` is antonymous to `(a contains b)`
* synonymous - `belongs-to`, `element-of`, `located-inside`

Example pattern: `A  B  C  /B  /A`

In this pattern, node `A` is said to strictly contain node `B` and to loosely
contain node `C`. Therefore, node `A` contains and is related to both nodes.
Even though `C` is also related to `A` and `B`, node `C` does itself not contain
any nodes. In addition to that, `C` can be understood to be located inside of
both nodes.
