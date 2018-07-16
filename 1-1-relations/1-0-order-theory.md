
<!-- ======================================================================= -->
# Order Theory

What exactly is "order"?

An "order" is by its own a relation that defines the relationship the elements
of a set have with each other. Order theory examines the common characteristics
of different order relations.

<!-- ======================================================================= -->
## wikipedia, order theory

* examine the notion of order using binary relations
* subset-of - captures a notion of containment/specialization
* (<=,==,>=) - on numbers allow to compare any two elements
* "partial orders" - pairs of elements may exist that are in-comparable
* e.g. subset-of, factor-of (n|m), identical-to - are partial orders
* "total orders" - all pairs of elements are comparable - (a <= b) or (b <= a)

(partially) ordered set - aka. poset

* poset - a set with a partial order on it
* partial order - transitive, reflexive, antisymmetric
* linear order, chain - are total partial orders
* hasse diagrams - used to visualize partial orders

partial orders may contain "special elements"

* e.g. "1" in Nat - "1" is the least element under "<"
* e.g. "{}" in P(s) - "{}" is the least set under "subset-of"
* e.g. "0" in Int - can be divided by any number - greatest element
* such elements are called minimal/maximal - there may be more than one
* e.g. 2-to-5 under divisibility - 2, 3 and 5 are minimal
* minimal/maximal - there is no other element that is smaller/greater
* note - elements may be both min and max

subsets of partially ordered sets

* maintain/inherit the order
* allows to define upper/lower bounds
* e.g. (-1) is a lower bound of the natural numbers
* e.g. the union of sets is an upper bound to its subsets

duality

* a given order can be inverted by exchanging its direction
* the same can be done with definitions - e.g. minimal/maximal
* i.e. dual, inverse, opposite order
* this is a general truth

construction of new orders

* e.g. by duality
* e.g. cartesian product under the product order
* product order - for (A X B) define (a1,b1)<=(a2,b2) iff (a1<=a2) & (b1<=b2)
* note the 3 distinct orders in (A X B), A, B

functions between orders

* monotone functions map one order onto another - order-preserving
* order-preserving if: (a <= b) -> (f(a) <= f(b))
* the "converse" of this implication leads to
* order-reflecting if: (f(a) <= f(b)) -> (a <= b)
* order-reversing if: (a <= b) -> (f(b) <= f(a)) - aka. antitone
* order-embedding - map natural numbers to real numbers
* order isomorphism - orders are the same, "rename" elements

types of orders

* preorder - transitive, reflexive
* each preorder includes an equivalence relation between elements
* preorders are relations that can be turned into orders (hence: pre-order)
  by identifying all equivalent elements with respect to this relation
* total order - attach distinct real numbers to items
* strict weak ordering - distinct items may have equal scores
* and many more ...

subsets of ordered sets

* such subsets may have special properties
* e.g. upper closure of S in P - { x in P | (y <= x) for some (y in S) }
* upper/lower set - equal to its upper/lower closure

<!-- ======================================================================= -->
## wikipedia, order isomorphism

order isomorphism

* a monotone function
* an isomorphism for partially ordered sets

ordinal number

* ordinal number - generalization of "natural number"
* any finite set can be put in order by counting its elements
* i.e. label its elements with distinct natural numbers
* an ordinal number is used to describe the order type of a well ordered set

order type

* order isomorphic - ordered sets X and Y have the same order type
* requires a bijection (1:1, e.g. `n -> 2*n`)
* must be order-preserving
* every well-ordered set is order-equivalent to exactly one ordinal number
