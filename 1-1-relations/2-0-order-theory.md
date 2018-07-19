
<!-- ======================================================================= -->
# Order Theory

An "order" is by itself a relation that defines the relationship between the
elements of a set. Order theory examines the characteristics of order relations.

This is me trying to wrap my head around the classification of orders. The best
course of action seems to be to (1) pick an order, (2) determine its properties,
and (3) let others do the classification ...

Note that, in the course of this whole discussion, the focus will be on "linear
orders of nodes" which are the result of some tree traversal.

Note that partial/pre-orders are closely related to graph theory.
Meaning that graphs can in general be used to visualize orders.

<!-- ======================================================================= -->
## ordered sets of elements

* there is no single specific type of ordered set

simple set

* a set is a group of elements in which all elements are different
* the elements in a (simple) set have no order whatsoever
* a simple set has no first, no last, and no n-th element
* a set can essentially only answer the "element-of" question
* a set appears as a black box

ordered set

* a (simple) set of elements that is paired with an order relation
* an order relation defines the relationship between the elements
* i.e. a set whose elements are ordered by an order relation

countable sets, total/well order

* sets can be totally ordered in various ways
* well-orders (see ordinal numbers) - natural numbers, least element
* other - integers, not guaranteed to have a least element
* key definition of whether a total order is also a well order

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
* linear order, chain - are total partial orders
* hasse diagrams - used to visualize partial orders

least/greatest elements

* with regards to partially ordered sets P
* m is least, if (m <= a) for all elements in P
* greatest element - dual to least
* least/greatest elements do not necessarily exit
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

* maintain/inherit the order
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
* product order - for (A X B) define (a1,b1)<=(a2,b2) iff (a1<=a2) & (b1<=b2)
* note the 3 distinct orders of (<=) in (A X B), A, B
* every partial order (<=) gives rise to a strict order (<)
* e.g. (a < b) if (a <= b) and !(b <= a)
* e.g. (a <= b) if (a < b) or (a = b)

functions between orders

* monotone functions - an order-preserving mapping of order onto another
* order-preserving: (a <= b) -> (f(a) <= f(b))
* the "converse" of this implication leads to order-reflecting
* order-reflecting: (f(a) <= f(b)) -> (a <= b)
* order-reversing, antitone: (a <= b) -> (f(b) <= f(a))
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
