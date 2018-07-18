
<!-- ======================================================================= -->
# TODO - node trees

<!-- ======================================================================= -->
## add to core definitions

* (similar to set-of-sets)
* related vs. unrelated nodes
* define "related nodes"
* instead of "one is an ancestor of the other"

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
