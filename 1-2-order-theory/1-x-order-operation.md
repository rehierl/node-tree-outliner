
<!-- ======================================================================= -->
# Order structures - operations

<!-- ======================================================================= -->
## wikipedia, product order

* given two ordered sets A and B
* induce a partial ordering on the Cartesian product (A x B)
* (a1,b1) and (a2,b2) in (A x B)
* (a1,b1) <= (a2,b2) iff (a1 <= a2) and (b1 <= b2)

remarks

* aka. coordinate/component-wise order
* the product order of two totally ordered sets is not total
* e.g. (0,1) and (1,0) are incomparable
* in general, the prod-order is a sub-relation of the lexi-order

<!-- ======================================================================= -->
## wikipedia, linear extension

* short - lin-ext
* the linear extension of a partial order is a total order
* the lexi-order of totally ordered sets is a lin-ext of their prod-order

definition

* given op1 and op2 on set X
* op2 is a lin-ext of op1, if
* 1) op2 is a total order
* 2) if (x op1 y), then (x op2 y) for all (x,y in X)

remarks

* op2 is said to extend op1
* a lin-ext is a order-preserving bijection from a poset to a chain

principle

* known as the order-extension principle
* proven by the use of the "axiom of choice"
* the principle is itself taken as an axiom
* a partial order in which every pair is incomparable can be extended
* i.e. every part-order can be linearly ordered
* known as the ordering principle
