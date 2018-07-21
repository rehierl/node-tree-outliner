
<!-- ======================================================================= -->
# order - characteristics

* issue - no strict/consistent naming convention
* i.e. probably due to a "naturally" grown system of names
* i.e. semantics of partial/strict/total seems mixed

```
preorder             - reflexive, transitive
equivalence relation - symmetric preorder
partial-order        - anti-symmetric preorder
total-order          - connex partial-order
```

* partial - some in-comparable pairs
* total - no in-comparable pairs
* comparable - if (a op b) or (b op a)
* incomparable - if neither (a <= b) nor (b <= a)
* note - equal items are incomparable under (<)
* note - transitivity of incomparability
* covered - no 3rd element in between
* precedes - there may be elements in between

```
partial equivalence relation - symmetric, transitive
strict weak order            - strict partial order
strict weak order            - asymmetric preorder
strict partial order         - asymmetric preorder
```

* strict - irreflexive, no loops
* not including reflexivity - i.e. may still be reflexive
* strict vs. non-strict - often ignored because easily interconvertible

<!-- ======================================================================= -->
## order - overview

structures - 1

* pre-order - almost an order, but not quite
* partial order - may hold in-comparable elements
* total/linear/chain order - a poset such that all pairs are comparable

structures - 2

* equivalence relation - a partition of a set
* weak order - may contain ties/equals
* well order - total, and each subset has a least element
* lattices - each pair has a greatest-lower and a least-upper bound
* antichain - a subset of a poset such that all pairs are in-comparable

classification by

* comparability - all/some/none incomparable
* reflexivity/strictness - all/some/none related to themselves
* directed/weakness/symmetry - all/some/none relationships directed

transform

* product order - induce a partial ordering on the cart-product
* linear extension - make all pairs comparable - partial-to-total
* order type - same type if isomorphic
* order isomorphism - an isomorphic mapping exists
* order embedding - one order embedded into another
