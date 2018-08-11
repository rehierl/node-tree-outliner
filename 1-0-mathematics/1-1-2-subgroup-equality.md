
<!-- ======================================================================= -->
# Subgroup, equality

Note that "subgroup-of" is distinct from "element-of".

<!-- ======================================================================= -->
## power-set (of a multiset)

* `A := < 1, 2, 2 >`
* `P(A) := { <>, <1>, <2>, <1,2>, <2,2>, <1,2,2> }`
* note - `#P(A) <= (2^N = 8)` elements
* `P(A)` is the set of all subgroups in `A`
* note - `P(A)` contains `<>` and `A`

<!-- ======================================================================= -->
## subgroup-of

* `#(v,V)` - the cardinality of `(v in V)` - aka. multiplicity
* `(V subgroup-of W) := (#(v,V) <= #(v,W)) for all (v in V)`

Note that, if `(V subgroup-of W)` is true,
then `V` may be referred to as the "sub-group"
and `W` as the "super-group".

clarification

* the empty group `<>` is a subgroup to any group
* any group, including `<>`, is a subgroup to itself
* `subgroup-of` implies an order (<=)

clarification

* `(V subgroup-of W) <=!=> (W subgroup-of V)`
* `(V subgroup-of W) -> (#V <= #W)`

<!-- ======================================================================= -->
## equal-to

* `(V == W), (V equal-to W) := (V subgroup-of W) and (W subgroup-of V)`
* any element `(v in V)` has the same multiplicity in `W`, and
  any element `(w in W)` has the same multiplicity in `V`
* `V` and `W` can not be distinguished from one another
* `V` and `W` are said to be equal

clarification

* `(V == W) <-> (W == V)`
* `(V == W) -> (#V == #W)`
* `(#V == #W) =!> (V == W)`

<!-- ======================================================================= -->
## unequal-to

* `(V != W) := not (V == W)`
* `(V unequal-to W), (V distinct-to W) := (V != W)`
* `V` and `W` can be distinguished from one another
* `V` and `W` are said to be unequal or distinct from one another

clarification

* `(V != W) <-> (W != V)`
* `(#V != #W) -> (V != W)`
* `(V != W) =!> (#V != #W)`

Note that `V` and `W` may have the same cardinality;
they could still differ only in the multiplicities of their elements.

<!-- ======================================================================= -->
## strict-subgroup-of

* `(V strict-subgroup-of W) := (V subgroup-of W) and (V != W)`
* some `(w in W)` must exist such that `(#(w,W) > #(w,V))`
* synonymous - strict-, proper-, true-subgroup

Note that, if `(V strict-subgroup-of W)` is true,
then `V` may be referred to as the "(strict) sub-group"
and `W` as the "(strict) super-group".

clarification

* the empty group `<>` is a strict subgroup to any non-empty group
* no group, including `<>`, is a strict subgroup to itself
* `strict-subgroup-of` implies an order (<)

clarification

* `(V strict-subgroup-of W) -> (#V < #W)`
* `(V strict-subgroup-of W) -> !(W strict-subgroup-of V)`
