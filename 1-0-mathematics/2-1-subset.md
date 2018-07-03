
<!-- ======================================================================= -->
# Subset

<!-- ======================================================================= -->
## V subset-of W

* `(V subset-of W) := (v in W) for any (v in V)`
* set `V` is a subset of set `W`, if `v in W` for any `v in V`

Note that, if `(V subset-of W)` is true,
then `V` may be referred to as "subset"
and `W` as "super-set".

clarification

* `(V subset-of W) -> (#V <= #W)`
* In order for `(V subset-of W)` to be false, `V` needs to contain one or more
  elements that are not in `W`. But, that is "assumed" to not be the case.
* In order for `(#V <= #W)` to not be true, even though `(V subset-of W)` is
  true, `(#V > #W)` would need to be true. But that is not possible as `V`
  would need to have all the elements in `W` plus one additional element.
  Because of that, `(V subset-of W)` could no longer be true. That would be a
  conflict as `(V subset-of W)` can not be true and false at the same time.
* `subset-of` implies an order (<=)

clarification

* The empty set `{}` is a subset to any set.
* Any set, including `{}`, is a subset to itself.

clarification

* `(V subset-of W) <=!=> (W subset-of V)`
* `(V subset-of W) <-> ((V & W) == V)`

<!-- ======================================================================= -->
## equal-to

* `(V == W), (V equal-to W) := (V subset-of W) and (W subset-of V)`
* the values in both sets can not be used to distinguish both sets
* any value `v in V` also belongs to `W`, and
  any value `w in W` also belongs to `V`
* `V` and `W` are said to be equal

(V == W) -> (#V == #W)

* (V == W) <-> (V subset-of W) and (W subset-of V)
* For ((V subset-of W) and (W subset-of V)) to be true, each element in
  a set must also be an element of the other set. That is, none of those
  sets can contain an element which the other set does not contain.
* For (#V == #W) to not be true, one set would need to have more elements
  than the other. This however would be in conflict with the left side.
* `(V == W) -> (#V == #W)` is true

(V != W)

* `(V != W) := not (V == W)`
* (V != W) <-> (V !subset-of W) or (W !subset-of V)
* both are different in size and/or values

clarification

* `(V == W) <-> (W == V)`, and `(V != W) <-> (W != V)`
* `(V == W) -> (#V == #W)`, but `(#V == #W) =!> (V == W)`
* `(#V != #W) -> (V != W)`, but `(V != W) =!> (#V != #W)`

<!-- ======================================================================= -->
## V strict-subset-of W

* `(V strict-subset-of W) := (V subset-of W) and (V != W)`
* some `w in W` must exist such that `w !in V` is true
* synonymous - strict-subset, proper-subset, true-subset

Note that, if `(V strict-subset-of W)` is true,
then `V` may be referred to as "(strict) subset"
and `W` as "(strict) super-set".

clarification

* `(V strict-subset-of W) -> (#V < #W)`
* `strict-subset-of` implies an order (<)

clarification

* The empty set `{}` is a strict subset to any non-empty set.
* No set, including `{}`, is a strict subset to itself.
