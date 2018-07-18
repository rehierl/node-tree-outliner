
<!-- ======================================================================= -->
# Order structures - overview

This is me trying to wrap my head around the classification of orders. The best
course of action seems to be to (1) pick an order, (2) determine its properties,
and (3) let others do the classification ...

Note that, in the course of this whole discussion, the focus will be on "linear
orders of nodes" which are the result of some tree traversal.

<!-- ======================================================================= -->
## relation properties

```
(total) pre-order    - reflexive, transitive
partial-order        - anti-symmetric pre-order
total-order          - connex partial-order
strict-total-order   - 
```

* comparable - if (a op b) or (b op a)
* incomparable - if neither (a <= b) nor (b <= a)
* covered - no 3rd element in between
* total - no in-comparable pairs
* strict - irreflexive, no loops

```
strict partial order - x, a-symmetric
strict weak order    - x, a-symmetric
partial equivalence  - x, symmetric
equivalence relation - symmetric pre-order
```

* A "total preorder" or "weak order" is a preorder that is total!

clarification

* a "strict weak order" is a "strict partial order" plus properties (total?)
* none of those two are pre-orders (irreflexive)

<!-- ======================================================================= -->
## structure overview

* partial order - may hold in-comparable elements
* antichain - a subset of a poset such that all pairs are in-comparable
* total/linear/chain order - a poset such that all pairs are comparable

transform

* product order - induce a partial ordering on the cart-product
* linear extension - make all pairs comparable - partial-to-total

<!-- ======================================================================= -->
## directed acyclic graphs (DAG)

* preorder <=> dag

partial orders

* vertices ordered by reachability
* partial order => dag
* strict partial order => dag
