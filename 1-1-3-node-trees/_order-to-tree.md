
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

wikipedia, comparability graph

* https://en.wikipedia.org/wiki/Comparability_graph
* any poset P:=(S,<) can be represented as a family of sets
* i.e. sets such that s(x) corresponds with x in S
* (x < y) iff (s(x) subset-of s(y))
