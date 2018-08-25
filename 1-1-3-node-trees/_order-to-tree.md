
<!-- ======================================================================= -->
# TODO - (order <-> trees)

post-order traversal

* a topological ordering?
* i.e. aEb -> (a presequent-to b)
* me thinks not

trees

* tree-order, ordered tree
* an order-embedding?

order theory - partial orders

* vertices ordered by reachability
* (strict) partial order => dag

<!-- ======================================================================= -->
## references

wikipedia, tree (set theory)

* https://en.wikipedia.org/wiki/Tree_%28set_theory%29
* tree, a partially ordered set `(T,<)`
* each well-ordered set is a tree
* trees grow downward - root is greatest
* a subtree is downward closed - a subset

wikipedia, topological sorting

* https://en.wikipedia.org/wiki/Topological_sorting
* create a partial order from a DAG
* (1) the order's objects are the vertices
* (2) define (x <= y) if (y) can be reached from (x)
* create a DAG from a partial order
* (1) the DAG's vertices are the objects of the order
* (2) define edge (x,y) if (x <= y)
* (3) use transitive reduction

wikipedia, comparability graph

* https://en.wikipedia.org/wiki/Comparability_graph
* any poset P:=(S,<) can be represented as a family of sets
* i.e. sets such that s(x) corresponds with x in S
* (x < y) iff (s(x) subset-of s(y))
