
<!-- ======================================================================= -->
# Subset

* subset-of <=!=> element-of

<!-- ======================================================================= -->
## power set

* `A := { 1, 2 }`
* `P(A) := { {}, {1}, {2}, {1,2} }`
* `P(A)` is the set of all subsets in `A`
* note - `{}` and `A` in `P(A)`

clarification

* `P(A)` always contains the empty set `{}`
* `#P(A) = 2^N = 8`, if `#A = N = 3`

<!-- ======================================================================= -->
## V subset-of W

* `(V subset-of W) := (v in W) for any (v in V)`
* set `V` is a subset of set `W`, if `v in W` for any `v in V`

Note that, if `(V subset-of W)` is true,
then `V` may be referred to as the **subset**
and `W` as the **super-set**.

clarification

* The empty set `{}` is a subset to any set.
* Any set, including `{}`, is a subset to itself.

clarification

* `(V subset-of W) <=!=> (W subset-of V)`
* `(V subset-of W) <-> ((V & W) == V)`
* `(V subset-of W) -> (#V <= #W)`

proof that `(V subset-of W) -> (#V <= #W)` is true

* In order for `(V subset-of W)` to be false, `V` needs to contain one or more
  elements that are not in `W`. But, that is "assumed" to not be the case.
* In order for `(#V <= #W)` to not be true, even though `(V subset-of W)` is
  true, `(#V > #W)` would have to be true. But that is not possible as `W` must
  hold all the elements of `V`. Because of that, `(#V > #W)` can not be true.
* If `W` holds all elements in `V`, then `W` may still hold elements that are
  not in `V`. Hence, `(#V < #W)` is not in conflict.
* `subset-of` implies an order (<=)

clarification

Note that the empty set `{}` has no element that could be in conflict with the
requirement of the `subset-of` definition. Because of that, "any element in the
subset is an element of the super-set" is understood to be true if the subset
is empty. That is because the definition of the `subset-of` operator merely
states that, for `(V subset-of W)` to be true, any element that exists in `V`
must also be an element of `W`. Obviously, there is no element in the empty
set which could be in conflict with that requirement.

<!-- ======================================================================= -->
## equal-to

* `(V == W), (V equal-to W) := (V subset-of W) and (W subset-of V)`
* the elements in both sets can not be used to distinguish both sets
* any element `(v in V)` also belongs to `W`, and
  any element `(w in W)` also belongs to `V`
* `V` and `W` are said to be equal

clarification

* `(V == W) <-> (W == V)`
* `(V == W) -> (#V == #W)`
* `(#V == #W) =!> (V == W)`

clarification

* For two sets to be equal, both sets must have the same size and contain the
  same elements. That is, the union of both sets must be identical (in size)
  to the intersection of both sets.
* `(V == W) <-> ( #(V or W) == #(V and W) )`

proof that `(V == W) -> (#V == #W)` is true

* `(V == W) <-> (V subset-of W) and (W subset-of V)`
* For `((V subset-of W) and (W subset-of V))` to be true, each element in
  a set must also be an element of the other set. That is, none of those
  sets can contain an element which the other set does not contain.
* Consequently, `(V == W) -> (#V == #W)` is true.

<!-- ======================================================================= -->
## unequal-to, distinct-to/from

* `(V != W) := not (V == W)`
* `(V != W) <-> (V !subset-of W) or (W !subset-of V)`
* synonymous - distinct-to/from, unequal-to

clarification

* `(V != W) <-> (W != V)`
* `(#V != #W) -> (V != W)`
* `(V != W) =!> (#V != #W)`

clarification

* Two distinct sets are unequal.
* Both sets can be distinguished from one another.
* Two distinct sets differ in size and/or their elements.

clarification

* For two sets to be distinct, one or both sets must be non-empty.
* `(V != W) -> (#V > 0) or (#W > 0)`

<!-- ======================================================================= -->
## V strict-subset-of W

* `(V strict-subset-of W) := (V subset-of W) and (V != W)`
* some `w in W` must exist such that `w !in V` is true
* synonymous - strict-subset, proper-subset, true-subset

Note that, if `(V strict-subset-of W)` is true,
then `V` may be referred to as the **(strict) subset**
and `W` as the **(strict) superset**.

clarification

* The empty set `{}` is a strict subset to any non-empty set.
* No set, including `{}`, is a strict subset to itself.

clarification

* `(V strict-subset-of W) -> (#V < #W)`
* `(V strict-subset-of W) -> !(W strict-subset-of V)`
* `strict-subset-of` implies an order (<)
