
<!-- ======================================================================= -->
# A (simple) set of values

* see "set theory" for in-depth discussions on sets

<!-- ======================================================================= -->
## core concept

* values may be grouped into (simple) sets of values
* sets of values are not paired with an order-relation
* hint: "simple" because "not ordered"
* sets of values are complex values

`V := { v1, v2 }`

* each set contains a value no more than once
* i.e. each value must be unique

`V := { e1:v1, e2:v3 }`

* a set of values can be understood to hold one element/slot per value
* the number of elements in a sequence is referred to as its "size"
* the elements within a set have no order - no first/last element/value
* no element is allowed to hold the value of another element
* i.e. a `1:1` relationship between values and elements
* i.e. "values" and "elements" can be used synonymously
* `(vi != vj) <-> (ei !== ej)`

definition

* `V := { vi | vi holds an odd integer }`
* instead of listing each value, sets can be defined by
  specifying a condition that must be satisfied by each value
* alternative notations - `{:}`, `{;}`, `{,}`, etc.

clarification

* adding or removing a value to or from a set results in a different set
* sets are constant/immutable, sets can not be changed, sets are not variable
* mathematical sets of values are constant entities (not obvious to programs)

clarification

* `V1 := { V }`, `V2 := < V, V >`
* simple sets are themselves values
* `V2` is a multiset, not a simple set

<!-- ======================================================================= -->
## is-set

* `(is-set s), isSet(s)` returns `true`, if value `s` is a set of values
* true, if value `s` has the characteristics of a set

<!-- ======================================================================= -->
## set-of

a homogenous set of values

* `V1 := { 1, 2, 3 }`
* `V2 := { 'a', 'b', 'c' }`
* a set may only contain values that have similar characteristics
* `isHomogenous(V)`, `isHom(V)` := true, if `V` is a homogenous set

a heterogenous set of values

* `V3 := { 1, 2.0, 0xab, 'a' }`
* `V4 := { 1, 2.0, 0xab, 'a', "abc", {5} }`
* a set may contain values that have distinct characteristics
* `isHeterogenous(V) := not isHom(V)`

a set of X

* `V := { vi | isX(vi) }`
* all values `(vi in V)` have characteristic `X`
* e.g. a set of numbers, characters, sets, etc.

a set of atomic values

* `V := { vi | isAtomic(vi) }`
* `V` contains primitive values only
* no `vi` is complex - no strings, no sets, etc.
* however, `V` is itself still a complex value
* a set of atomic values is not necessarily homogenous

<!-- ======================================================================= -->
## iteration

```
traceOfValues(setOfValues) begin
  seq = new sequence()
  for v in setOfValues begin
    seq.append(v)
  end
  return seq
end

set = {1, 2}
s1 = traceOfValues(set)
s2 = traceOfValues(set)
```

* any set of values allows to visit each of its values
* an iteration may visit the values in any order
* subsequent iterations may visit the values in different order
* i.e. `s1` is not guaranteed to be identical to `s2`
* synonymous - iterate, visit

<!-- ======================================================================= -->
## size-of, cardinality

* `#V, #(V), sizeOf(V)` := the number of elements in `V`
* `(size-of V), (cardinality-of V) := sizeOf(V)`

<!-- ======================================================================= -->
## is-empty

* `(is-empty V), isEmpty(V) := (#V == 0)`
* `{}` represents the empty set
* `(#{} == 0)` is always true
* `(V == {}) <-> (#V == 0)`

<!-- ======================================================================= -->
## one-element-of

* `oneElementOf(S)` := returns a random element from the given set

clarification

* the element returned remains to be an element of the set
* subsequent calls may result in different elements being returned

<!-- ======================================================================= -->
## (v in V), element-of

* `(v in V), (v element-of V)` := true, if `v` is an element in `V`
* value `v` is in set `V`, if `v` is an element of `V`

clarification

* different sets of values may contain the same value
* `v1 in V1` and `v1 in V2` may be true at the same time
* however, `v2 !in V2` may also be true -
  i.e. the indexes are independent from each other

v belongs-to V

* `(v belongs-to V) := (v in V)`
* value `v` belongs to set `V`, if `v` is an element of `V`

V contains v

* `V(v), (V contains v) := (v in V)`
* set `V` contains value `v`, if `v` is an element of `V`

<!-- ======================================================================= -->
## V in W

* any set is itself a value
* `(V in W), (V element-of W)` := true, if set `V` is an element of set `W`
* `(W contains V) := (V in W)`

clarification

* subset-of <=!=> element-of

<!-- ======================================================================= -->
## union (+, or, union)

* `(V union W) := { x | (x in V) or (x in W) }`
* `(V or W), (V + W) := (V union W)`

likewise

* `(V + w) := (V + {w})`
* `(v + W) := ({v} + W)`
* `(v + w), ({v} + {w}) := {v, w}`

clarification

* `((U + V) + W) <-> (U + (V + W))`
* `((u + v) + w) <-> (u + (v + w))`

<!-- ======================================================================= -->
## intersection (&, and, isect)

* `(A isect B) := { x | (x in A) and (x in B) }`
* `(A & B), (A and B) := (A isect B)`

<!-- ======================================================================= -->
## set difference (\, sub, diff)

* `(A diff B):= { x | (x in A) and (x !in B) }`
* `(A \ B), (A sub B) := (A diff B)`

<!-- ======================================================================= -->
## symmetric difference (^, xor, ex-or)

* `(A ex-or B) := {x | x in (A\B or B\A) }`
* `(A ^ B), (A xor B) := (A ex-or B)`

clarification

* `(A xor B) := (A \ B) or (B \ A)`
* `(A xor B) := (A or B) \ (A & B)`
