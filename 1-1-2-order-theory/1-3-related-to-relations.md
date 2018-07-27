
<!-- ======================================================================= -->
# Related to relations

<!-- ======================================================================= -->
## wikipedia, covering relation

* the covering relation of a poset is the
* bin-rel which holds between comparable elements
* that are immediate neighbors

definition

* poset (X,<=)
* (x < y) iff (x <= y) and (x != y)
* (x covers y), if (x < y) and there is no (z) such that (x < z < y)
* alternative - (x covers y), if `([x,y] = {x,y})`

examples

* e.g. given the natural numbers, (i+1) covers all i
* e.g. given the real numbers, no number covers another under (<=)
* e.g. the transitive reduction of a poset is a cover relation

<!-- ======================================================================= -->
## wikipedia, setoid

* aka. e-set, bishop set, extensional set
* a setoid is a set euipped with an ER
* used in proof theory, type theory

<!-- ======================================================================= -->
## wikipedia, equivalence relation (ER,~)

* there is no "equivalence order" because
* there is no direction (i.e. "before" or "after")
* i.e. there is consequently no "order"
* all elements are either equal or unequal
* i.e. disjoint equivalence classes of equal elements

remarks

* must be - reflexive, transitive, symmetric
* i.e. a symmetric preorder
* e.g. "is-equal-to" is the canonical example
* any ER represents a partition of the underlying set

construction

* (~) is an equiv. relation on set X
* P(x) is a property of elements of X
* P(x) is well-defined, if whenever (x ~ y) => P(x) is true if P(y) is true

<!-- ======================================================================= -->
## wikipedia, partition of a set

* aka. a family of sets
* group the elements of set X into a set of non-empty disjoint subsets P
* equivalence relation <= defines => partition
* subsets in P - blocks, parts, cells
* rank of P - (#X - #P) - (#elements >= #blocks)
* e.g. "equal to", "similar to"

<!-- ======================================================================= -->
## wikipedia, partial equivalence relation (PER)

* aka. restricted equivalence relation
* must be - symmetric, transitive
* "partial" here - "almost, but not quite"
