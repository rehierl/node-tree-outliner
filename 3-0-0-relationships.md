
<!-- ======================================================================= -->
# Related nodes

A tree of nodes can be defined by a set of nodes `N` and by a set of edges `E`.
The edges as a whole define a parent-child relationship, a `parent-of` relation
on all the nodes.

* `Relation := (A,B,G)` => `Graph := (V,V,E)` => `Tree := (N,E)`

<!-- ======================================================================= -->
## (p parent-of c) relation

The 1st node of each edge refers to the parent node and the 2nd node to a child
node for which the 1st node is a parent (i.e. `e := (p,c)`). In other words, all
edges point from a parent node towards a child node.

* `sem(Tree) := p parent-of c` for any `(p,c) in E`
* `sem(Tree)` refers to the semantics of `Tree`

<!-- ======================================================================= -->
## (a related-to b)

The parent-child relationship of a tree defines which nodes are in direct/strict
relationship with another node. Consequently, there is no strict relationship
between two nodes `a` and `c` (i.e. `!aRc`) if `aEb` and `bEc` (if that were the
case, `c` would have two parent nodes `b` and `a`). As a result, the parent-child
relationship defined by the set of edges `E` is itself not transitive (defined
as "if `aRb and bRc`, then also `aRc`").

* `a strictly-related-to b`, if `aEb` or `bEa`
* `a` and `b` are strictly related with each other

Even if grandparents are not strictly related to their grandchildren, nodes `a`
and `c` are nonetheless related with each other. That is because `E` allows to
define a path that connects both nodes (e.g. `p=(a,b,c)` if `aEb` and `bEc`).

* `a loosely-related-to b`, if a path `p=(a,..,b)` or `p=(b,..,a)` exists
  such that `(#p > 2)` and all pairs `(pi,pi+1)` of that path are in `E`
* i.e. an uni-directional path can be defined that connects both nodes
* `a` and `b` are loosely related with each other

The strict and loose relationship can be generalized into:

* `a related-to b`, if `(a strictly-related-to b)` or `(a loosely-related-to b)`
* `a` and `b` are related with each other

<!-- ======================================================================= -->
## (c child-of p) relation

The directed strict top-down orientation (i.e. away from the root towards the
leafs of a tree) of the parent-child relation is necessary because the inverted
set of edges `E'` defines a graph that contains multiple root nodes, but only a
single leaf node.

* `ant(Tree) := c child-of p` for any `(c,p) in E'`
* `ant(Tree)` refers to the antonymous relation of `Tree`
* i.e. `p parent-of c` is antonymous to `c child-of p`

<!-- ======================================================================= -->
## (a ancestor-of n)

Without any relationship between a node and its grandparents and grandchildren,
there would be no reason to define the terms "grand-parent" and "grand-child".
Similarly, there would be no reason to generalize those two terms into
"ancestor" and "descendant":

* `a ancestor-of n`, if a path `p=(a,...,n)` exists
  such that `(#p > 1)` and all `(pi,pi+1) in E`
* `d descendant-of n`, if a path `p=(n,...,d)` exists
  such that `(#p > 1)` and all `(pi,pi+1) in E`

<!-- ======================================================================= -->
## (p contains c) relation

In HTML, the strict `a parent-of b` relation is semantically equivalent to a
strict `a contains b` relation (i.e. node `a` contains node `b` as a direct
element node).

* `a strictly-contains b`, if `aEb`
* `a loosely-contains c`, if `aEb` and `bEc`
* `a contains b`, if `(a strictly-contains b)` or `(a loosely-contains b)`
* `b located-inside a` and `b element-of a` are antonymous to `a contains b`

Example pattern: `<A><B>C</B></A>`

In this pattern, node `A` is said to strictly contain node `B` and to loosely
contain node `C`. Therefore, node `A` contains and is related to both nodes.
Even though `C` is also related to `A` and `B`, node `C` does itself not contain
any of those two nodes, but can still be said to be located inside of these.

As a result, the `related-to` relationship is undirectional, whereas the
`contains`, `located-inside` and `element-of` relationships are directional.
With that in mind, a tree can also be seen to be defined by such a `p contains c`
relation:

* `sem(Tree) := p contains c` for any `(p,c) in E`
* `(p contains c) <=> (p parent-of c)`
