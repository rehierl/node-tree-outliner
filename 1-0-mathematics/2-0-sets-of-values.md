
<!-- ======================================================================= -->
# (Simple-) set (ss)

* `V := {v1, v2}`
* different values may be grouped into sets of values
* each set contains a value no more than once - each value is unique
* `V := {v1, v2}`, `W := {v1, v3, v4}`
* the same values may be grouped into different sets of values
* `V1 := V`, `V2 := W`
* sets of values may be identified by number ids
* `Vi := V2` for `i = 2`
* similar to values, number ids may be generalized into letter ids

definition

* `V := { vi | vi holds an odd integer }`
* instead of listing each value/element,
  a set can be defined by a condition
  which must be satisfied by each value/element
* alternate notations - `{:}`, `{;}`, `{,}`, etc.

clarification

* adding or removing a value to or from a set results in a different set
* sets are constant/immutable, sets can not be changed, sets are not variable
* mathematical sets of values are constant entities (not obvious to programs)

clarification

* `V3 := {V1, V2}`, `V4 := <V2, V2>`
* any set of values is itself a value
* V4 is a multiset, not a set
* `V := {e1, e2}`, `(e1 == e2)`
* sets may contain different elements that hold the same value
* what matters in such a case are the entities, not their values

<!-- ======================================================================= -->
## is-set

* `(is-set s), isSet(s)` returns `true`, if value `s` is a set of values
* true, if value `s` has the characteristics of a set

<!-- ======================================================================= -->
## set-of

* `V5 := { 1, 2, 3 }`, `V6 := { 'a', 'b', 'c' }`
* a set may contain values that have similar characteristics
* `V7 := { 1, 2.0, 0xab, 'a', "abc", {5} }`
* a set may however also contain arbitrary values

a set of values

* `V := { vi | vi in S }`
* `S` contains primitive/atomic values only
* no value is complex - no strings, no sets, etc.
* i.e. "a set of atomic values"

a set of sets

* `V := { vi | isSet(vi), vi in S }`
* `S` may contain sets that differ in characteristics
* `S` may contain `V5`, `V6` and `V7`

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
* any iteration may visit the values in any order
* subsequent iterations may visit the values in different order
* that is, `s1` is not guaranteed to be identical to `s2`
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
## (v in V), element-of

* `(v in V), (v element-of V)` := true, if `v` is an element of `V`
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

* `(V contains v) := (v in V)`
* set `V` contains value `v`, if `v` is an element of `V`

<!-- ======================================================================= -->
## V in W

* any set is itself a value
* `(V in W), (V element-of W)` := true, if set `V` is an element of set `W`
* `(W contains V) := (V in W)`

clarification

* subset-of <=!=> element-of

<!-- ======================================================================= -->
## operations on sets

* in this context, the addition of values is of no interest
* the (+) operator is therefore used as the union operator for sets

### union (|, or, +)

* `(V union W) := { x | (x in V) or (x in W) }`
* `(V | W), (V or W), (V + W) := (V union W)`

likewise

* `(V + w) := (V + {w})`
* `(v + W) := ({v} + W)`
* `(v + w), ({v} + {w}) := {v, w}`

clarification

* `((U + V) + W) <-> (U + (V + W))`
* `((u + v) + w) <-> (u + (v + w))`

### intersection (&, and)

* `(A isect B) := { x | (x in A) and (x in B) }`
* `(A & B), (A and B) := (A isect B)`

### set difference (\, -, sub)

* `(A diff B):= { x | (x in A) and (x !in B) }`
* `(A \ B), (A ! B), (A - B), (A sub B) := (A diff B)`

### symmetric difference (^, xor, ex-or)

* `(A ex-or B) := {x | x in (A\B or B\A) }`
* `(A ^ B), (A xor B) := (A ex-or B)`

clarification

* `(A xor B) := (A \ B) or (B \ A)`
* `(A xor B) := (A or B) \ (A & B)`

<!-- ======================================================================= -->
## power set

* `A := {1,2}`
* `P(A) := { {}, {1}, {2}, {1,2} }`
* `P(A)` is the set of all subsets in `A`

clarification

* `P(A)` always contains the empty set `{}`
* `#P(A) = 2^N = 8`, if `#A = N = 3`
