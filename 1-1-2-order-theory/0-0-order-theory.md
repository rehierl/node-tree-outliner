
<!-- ======================================================================= -->
# Order Theory

An "order" is by itself a relation that defines the relationship between the
elements of a set. Order theory examines the characteristics of order relations.

This is me trying to wrap my head around the classification of orders. The best
course of action seems to be to (1) pick an order, (2) determine its properties,
and (3) let others do the classification ...

Note that partial/pre-orders are closely related to graph theory,
meaning that graphs can in general be used to visualize orders.

Note that there is no single specific type of "ordered set". That is because an
ordered set is a set of elements paired with some order relation.

<!-- ======================================================================= -->
## wikipedia, order theory

* examine the notion of order by the use of binary relations
* i.e. provide a formal framework to describe statements as "precedes that"
* subset-of - captures a notion of containment/specialization
* "partial orders" - pairs of elements exist that are in-comparable
* e.g. subset-of - does not allow to compare any two elements
* e.g. subset-of, factor-of (n|m), identical-to
* "total orders" - all pairs of elements are comparable 
* e.g. (<=,>=) - allows to compare each element to any other element
* functions between orders - e.g. monotone functions

(partially) ordered set

* poset - a set with a partial order on it
* partial order - transitive, reflexive, antisymmetric
* linear order, chain - total partial orders
* hasse diagrams - used to visualize partial orders

least/greatest elements

* with regards to partially ordered sets P
* m is least, if (m <= a) for all elements in P
* greatest element - dual to least
* least/greatest elements do not necessarily exist
* both are unique if they do exist
* e.g. "1" in Nat - "1" is the least element under "<"
* e.g. "{}" in P(s) - "{}" is the least set under "subset-of"
* e.g. "0" in Int - can be divided by any number - greatest element

min/max elements

* m is minimal, if (a <= m) then (a = m)
* maximal element - dual to minimal
* more than one min/max element may exist
* some elements may be both - i.e. min and max
* if m is the least element, then m is the only min element
* e.g. 2-to-5 under divisibility - 2, 3 and 5 are minimal
* i.e. least/greatest is more strict

subsets of partially ordered sets

* subsets of posets maintain/inherit the order
* allows to define bounds, upper/lower, least upper
* infimum, meet - greatest lower bound
* e.g. (-1) is a lower bound of the natural numbers
* e.g. the union of sets is an upper bound to its subsets

duality

* a given order can be inverted by exchanging its direction
* the same can be done with definitions - e.g. minimal/maximal
* i.e. dual, inverse, opposite order
* i.e. every definition has its dual

construction of new orders

* e.g. construction by duality
* e.g. cartesian product under the product order
* product order - for (A × B) define (a1,b1) <= (a2,b2) iff (a1<=a2) & (b1<=b2)
* note the 3 distinct orders (<=) in (A × B), A, B
* every poset (<=) gives rise to a strict order (<)
* e.g. (a < b) if (a <= b) and !(b <= a)
* every strict order (<) gives rise to a poset (<=)
* e.g. (a <= b) if (a < b) or (a = b)

functions between orders

* monotone functions - an order-preserving mapping between orders
* order-preserving, isotone: (a <= b) -> (f(a) <= f(b))
* the "converse" of this implication leads to order-reflecting
* order-reflecting: (a <= b) <- (f(a) <= f(b))
* order-reversing, antitone: (a <= b) -> (f(a) >= f(b))
* (order-preserving vs. order-reflecting), but (order-reversing vs. ???)
* e.g. powerset, set-complement
* order-embedding - order-preserving and order-reflecting
* e.g. map natural numbers to real numbers
* order isomorphism - orders are essentially the same, "rename" elements

special order types

* preorder - transitive, reflexive - i.e. not a partial order
* each preorder includes an equivalence relation between elements
* preorders are relations that can be turned into orders (hence: pre-order)
  by identifying all equivalent elements with respect to this relation
* total order - attach distinct numbers (aka. scores) to items
* strict weak ordering - distinct items may have equal scores
* semiorder - scores need to be separated by a fixed threshold
* interval order - threshold may vary on an per-item basis
* well-order - all non-empty subsets have a min element
* lattices - every non-empty finite set has a supremum and infimum
* and many more ...

subsets of ordered sets

* such subsets may have special properties
* upper set - a set of elements that all are above a given element
* upper closure of S in P - { x in P | (y <= x) for some (y in S) }
* upper/lower set - equal to its upper/lower closure
