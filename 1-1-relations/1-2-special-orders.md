
<!-- ======================================================================= -->
# Special types of orders

* total/simple/linear/chain order - a total partial order

overview

* note - all are transitive (=x) + y
* (total) pre-order - x + reflexive
* equivalence relation - symmetric pre-order
* partial order - antisymmetric pre-order
* strict partial order - x + irreflexive, antisymmetric
* strict weak order - x + irreflexive, antisymmetric
* partial equivalence - x + symmetric

clarification

* a "strict weak order" is a "strict partial order" plus properties
* none of those two are pre-orders (irreflexive)

<!-- ======================================================================= -->
## Preorder, quasiorder

* preorder - reflexive, transitive
* note - a preorder is not restricted to these properties
* equivalence relation - symmetric preorder
* partial order - antisymmetric preorder
* "pre-order" - almost a (partial) order, but not quite
* note - the (<=) operator/symbol does not always apply

directed graph

* preorder - directed graph (with possibly disconnected components)
* however, most directed graphs are neither reflexive, nor transitive
* partial order - directed acyclic graph - loops, but no cycles
* e.g. reachability in a directed graph => preorder

<!-- ======================================================================= -->
## Equivalence relation (~)

well-defined (unambiguous) properties

* (~) is an equiv. relation on set X
* P(x) is a property of elements of X
* P(x) is well-defined, if whenever (x ~ y) => P(x) is true if P(y) is true

partition of set

* aka. a family of sets
* group the elements of set X into a set of non-empty disjoint subsets P
* equivalence relation <- defines -> partition
* subsets in P - blocks, parts, cells
* rank of P - (#X - #P) - (#elements >= #blocks)
* e.g. "equal to", "similar to"

<!-- ======================================================================= -->
## Weak ordering

* formalization of ranking of a set
* a generalization of totally ordered sets
* axiomatized as strict weak order, total preorder, 

set-related ranking

* for any two items (a and b) within a set, (a < b) or (a = b) or (a > b)
* known as "weak order" or "total preorder"
