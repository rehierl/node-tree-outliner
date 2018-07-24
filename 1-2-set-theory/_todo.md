
<!-- ======================================================================= -->
# TODO - set theory

* "That is because" => "That is because"
* are length values similar to rank values?

towers of hanoi -
a wood stacking game -
allows to visualize trees -

preorder => directed graph -
"To every preorder, there corresponds a directed graph, ..." (wikipedia) -
this is more general than the equivalency between trees and hierarchies -
what kind of "special order" does the equivalency require? -

draw non-crossing borders around subtrees -
in an unordered tree, the subtrees are ordered only if
one subtree is a subtree of the other -
i.e. ordered according to the order of their root nodes -
in an ordered tree, the subtrees have an additional order -
i.e. tree-order + child-order -

hierarchy of sets -> unordered tree -
start with non-disjoint sets -
end with pairwise disjoint sets -
see partition refinement in computer science

<!-- ======================================================================= -->
## a set of sets

a set of sets

* `V := { vi | isSet(vi) }`
* all values in `(vi in V)` are sets of values

a heterogenous set of sets

* `V := { vi | isSet(vi) }`
* `V` contains sets that differ in characteristics
* i.e. `vi` is a set of `X`, `vj` is a set of `Y`, etc.
* e.g. `V` may contain `V5`, `V6` and `V7`

a homogenous set of sets

* `V := { vi | isSet(vi) and isX(vi) }`
* all `(vi in V)` are sets that share the same characteristic
