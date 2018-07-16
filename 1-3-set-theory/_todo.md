
<!-- ======================================================================= -->
# TODO

* "That is because" => "That is because"
* are length values similar to rank values?

preorder => directed graph -
"To every preorder, there corresponds a directed graph, ..." (wikipedia) -
this is more general than the equivalency between trees and hierarchies -
what kind of "special order" does the equivalency require? -

draw non-crossing borders around subtrees -
in an unordered tree, the subtrees are ordered only if
one subtree is a subtree of the other -
in an ordered tree, the subtrees have an additional order -
i.e. ordered according to the order of their root nodes -

towers of hanoi -
a wood stacking game -
allows to visualize trees -

<!-- ======================================================================= -->
## add to core definitions

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
