
<!-- ======================================================================= -->
# Set of values V

* different values may be grouped into sets of values -
  e.g. `V := {v1, v2}`
* each set can contain a value no more than once
* the same values may be grouped into different sets of values -
  e.g. `V := {v1, v2}`, `W := {v1, v3, v4}`
* sets of values may be identified by number ids -
  e.g. `V1 := V`, `V2 := W`
* similar to values, number ids may be generalized into letter ids -
  e.g. `Vi := V2` for `i = 2`

clarification

* adding or removing a value to or from a set results in a different set
* sets are constant/immutable, sets can not be changed, sets are not variable
* i.e. mathematical sets of values are constant (not too obvious to programs)
* any set of values is itself a value - e.g. `V3 := { V1, V2 }`, `v1 := V3`

<!-- ======================================================================= -->
## ordered sets of values

simple sets of values

* a simple set of values is a group of values in which all values are different
* the values of a (simple) set of values have no order
* a (simple) set has no first, no last, and no n-th value
* due to having "no order" and the `in` operator, a set appears as a black box
* the only question that can be answered is whether a set "contains" a value

ordered sets of values

* an ordered set of values is a simple set of values
* the values in an ordered set of values have an order
* an ordered set has a first, a last, and an n-th value
* every value `v(n)` has a previous `v(n-1)` and a next `v(n+1)` sibling
* an ordered set of values can respond with the index of a given value -
  e.g. `-1` if does not contain a value, `1` if it's the first value, etc.

examples

* `V1 := { +, 1, a }`
* the elements in `V1` have no order, they are mere symbols
* the elements need to be understood to represent mere symbols/images
* any implicit ordinal number must be ignored (e.g. ascii)
* `V2 := { a, b, c }`
* the elements in `V2` have an order, `a` comes before `b` and `b` before `c`
* the elements need to be understood to represent more than mere symbols
* each element has an implicit ordinal number associated with them
* `V3 := { a, a, b, c }`
* this group neither is an ordered set, nor a simple set of values
* not all elements within that group are unique

<!-- ======================================================================= -->
## is-set

* `(is-set s), isSet(s)` returns `true`, if value `s` is a set of values
* i.e. `s` has the characteristics of a set
* signature - (anything) -> boolean

<!-- ======================================================================= -->
## set of X

* in general, a set only contains values that have similar characteristics -
  e.g. `V5 := { 1, 2, 3 }`, `V6 := { 'a', 'b', 'c' }`
* however, a set may also consist of arbitrary selected values -
  e.g. `V7 := { 1, 2.0, 0xab, 'a', "abc", {5} }`
* "a set of values" := `vi in V` is a primitive value - no string, no set
* "a set of sets" := any `si in S` is itself a set - this does not state what
  kind of set `si` is - `S` may contain sets that differ in characteristics

<!-- ======================================================================= -->
## iteration

```
for v in V begin
  //- do something
end
```

* any set of values allows to visit each of its values
* however, any iteration may visit the values in any order!
* synonymous - iterate, visit

<!-- ======================================================================= -->
## size-of V, cardinality

* `sizeOf(V)` returns the number of elements in `V`
* `#V, #(V), (size-of V), (cardinality-of V) := sizeOf(V)`
* signature - (set) -> number `n in [0,*]`

<!-- ======================================================================= -->
## n size-of V

* `(n size-of V) := (n == sizeOf(V))`
* `(n cardinality-of V) := (n size-of V)`
* signature - (number,set) -> boolean

<!-- ======================================================================= -->
## is-empty V

* `(is-empty V), isEmpty(V) := (#V == 0)`
* `{}` represents an empty set, i.e. `(#({}) == 0)`
* `isEmpty({})` is always true

<!-- ======================================================================= -->
## V contains v

* `contains(V,v)` is true, if `v` is an element of `V`
* `(V contains v) := (contains(V, v) == true)`
* set `V` contains value `v`, if `v` is an element of `V`
* signature - (set, value) -> boolean

<!-- ======================================================================= -->
## (v in V), (v belongs-to V)

* `(v in V) := (V contains v)`
* `(v element-of V), (v belongs-to V) := (v in V)`
* value `v` is in set `V`, if `v` is an element of `V`
* signature - (value, set) -> boolean

clarification

* different sets of values may contain the same value
* `v1 in V1` and `v1 in V2` may be true at the same time
* however, `v2 !in V2` may also be true -
  i.e. the indexes are independent from each other
* `(v in V) <=> (V contains v)`

<!-- ======================================================================= -->
## V equal-to W

* `(V == W) := (v in W, for any v in V) and (w in V, for any w in W)`
* `(V equal-to W) := (V == W)`
* signature - (set,set) -> boolean

(V == W)

* any value `v in V` also belongs to `W`, and
  any value `w in W` also belongs to `V`
* `V` and `W` are said to be equal
* `V` and `W` have same size and values

(V != W)

* both are different in size and/or values

clarification

* `(V == W) <=> (W == V)`, and `(V != W) <=> (W != V)`
* `(V == W) => (#V == #W)`, but `(#V == #W) !> (V == W)`

<!-- ======================================================================= -->
## V subset-of W

* `(V subset-of W) := ((v in W) for any (v in V))`
* `subsetOf(V,W) := (V subset-of W)`
* set `V` is a subset of set `W`, if `v in W` for any `v in V`
* signature - (set,set) -> boolean

clarification

* `subset-of` implies an order (`<=`)
* `(V subset-of W) => (#V <= #W)`
* `(V == W) := (subsetOf(V,W) and subsetOf(W,V))`
* `(V subset-of W) <!> (W subset-of V)`

<!-- ======================================================================= -->
## V strict-subset-of W

* `(V strict-subset-of W) := (V subset-of W), but (V != W)`
* some `w in W` exists such that `w !in V`
* synonymous - strict-subset, proper-subset, true-subset
* signature - (set,set) -> boolean

clarification

* `strict-subset-of` implies an order (`<`)
* `(V subset-of W) => (#V <= #W)`
* `(V strict-subset-of W) => (#V < #W)`

<!-- ======================================================================= -->
## operations on sets

* in this context, the addition of values is of no interest
* this allows to use the (+) operator as the union operator for sets

### union (+, or)

* `(V union W), (V + W), (V or W) := { x : (x in V) or (x in W) }`

likewise

* `(V + w) := (V + {w})`
* `(v + W) := ({v} + W)`
* `(v + w), ({v} + {w}) := {v, w}`

clarification

* `((U + V) + W) <=> (U + (V + W))`
* `((u + v) + w) <=> (u + (v + w))`

### set difference (\, -, sub)

* `(A \ B), (A - B), (A sub B) := { x : (x in A) and (x !in B) }`

### intersection (&, and)

* `(A & B), (A and B) := { x : (x in A) and (x in B) }`

### symmetric difference (xor)

* `(A xor B) := {x : (x in (A\B or B\A)) }`

<!-- ======================================================================= -->
## power set

* `A := {1,2}`
* `P(A) := { {}, {1}, {2}, {1,2} }`
* `P(A)` is the set of all subsets of `A`

<!-- ======================================================================= -->
## V contains W

* any set is itself a value
* `(W in V)` is true, if set `W` is an element of set `V`
* set `W` is in set `V`, if `W` is an element of `V`
* `(V contains W), contains(V,W) := (W in V)`
* `(W element-of V), elementOf(W,V) := (W in V)`
* signature - (set,set) -> boolean

clarification

* `subset-of <!> element-of`
