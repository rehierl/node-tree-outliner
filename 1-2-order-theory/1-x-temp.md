
<!-- ======================================================================= -->
# Temporary

* cyclic
* lattices
* preorders
* semiorders
* weak orders
* well-orders
* well-quasi-orders

<!-- ======================================================================= -->
## wikipedia, interval order

* a collection of intervals on the real numbers
* a partial order that corresponds to the left-to-right precedence relation
* i.e. (l1 < l2) => l1 is completely left of l2

formally

* a poset P := (X,<=)
* a bijection (f: X -> (l,r)) exists
* (xi < xj) in P when (ri < lj)

remarks

* unit-length intervals - i.e. (i,i+1)
* semiorders - subclass of intervall orders if unit-length intervals
* interval graph - the complement of the interval-order's comparability graph

<!-- ======================================================================= -->
## wikipedia, semiorder

* a type of ordering
* determined for a set of items with numerical scores
* two items are incomparable if their scores are too close
* i.e. within a margin of error to each other
* generalize strict-weak-orderings
* from a special case of partial-orders and interval-orders

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
* a generalization of totally ordered sets (no ties)
* total orders generalized by partial orders and preorders
* weak orders axiomatized/formalized as - strict weak order,
  total preorder, ordered partitions, preferential arrangement

ranking of a set

* known as "weak order" or "total preorder"
* for any two items (a and b) within a set, (a < b) or (a = b) or (a > b)
* not necessarily a "total order" (e.g. elements might have equal rank)
* i.e. an incomparable pair may exist under the given relation - a tie

axiomatized/formalized

* A "total preorder" or "weak order" is a preorder that is total!
* partition + total order => an ordered partition (aka. list of sets)

<!-- ======================================================================= -->
## Lattice order

* a partially ordered set, in which every two elements
  have a unique supremum and a unique infimum
* supremum - least upper bound, join
* infimum - greatest lower bound, meet

<!-- ======================================================================= -->
## Well-order

* a well-ordered set
* => a set paired with such an order

definition

* well-order, well-ordering, well-order relation
* a well-order on a set S is a total order on S in which
* every non-empty subset of S has a least element
* least element - smaller than every other element
