
<!-- ======================================================================= -->
# TODO - node trees

what are sections?

* the union of sets of nodes
* i.e. no crossing borders
* the union of subtrees

mixed

* (strict) subtree as "induced subtrees"
* i.e. induced by its root node
* prefix/suffix-order of a rooted path
* prefix/suffix-order of a tree
* disjoint tree

thoughts

* sequences are not required, if ...
* a topological sorting can be defined
* based on the relationships of sets

<!-- ======================================================================= -->
## core definitions

align them with those in hierarchy-of-sets

* including `T := (N,E)`
* related vs. unrelated nodes
* define "related nodes"
* instead of "one is an ancestor of the other"
* properly define "sub-graph", "sub-tree"

**CLARIFICATION**
Node `n1` is said to be **disjoint** from `n2`,
if the outer sets of both nodes are disjoint.

* The subtrees of both nodes have no nodes in common.
* `n1` does not contain `n2`, and `n2` does not contain `n1`.
* `n1` is not an ancestor of `n2`, and `n2` not an ancestor of `n1`.

Note that two nodes in a tree are either disjoint,
ex-or one node is an ancestor of the other.

**CLARIFICATION**
Node `n1` is said to be **coupled** with `n2`,
if the outer sets of both nodes are not disjoint.

* coupled <=> not disjoint
