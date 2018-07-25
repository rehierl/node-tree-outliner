
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
* the number of elements in a set is referred to as "cardinality"
* the elements within a set have no order - i.e. no first/last element
* no element is allowed to hold the value of another element
* i.e. the multiplicity of each value within a set is one/1
* i.e. a `1:1` relationship between values and elements
* i.e. "values" and "elements" may be used synonymously
* `(vi != vj) <-> (ei !== ej)`

definition

* `V := { vi | (vi holds an odd integer) }`
* instead of listing each value, sets can be defined by
  specifying a condition that must be satisfied by each value
* alternative notations - `{:}`, `{;}`, `{,}`, etc.

clarification

* the number of elements in a set is referred to as its "size"
* in contrary to multisets, `(sizeOf(set) == lengthOf(set))` always holds
* i.e. the "size" of a set is equal to its cardinality

clarification

* adding or removing a value to or from a set results in a new set
* sets are constant/immutable - sets can not be changed - sets are not variable
* mathematical sets of values are constant entities - not obvious to programs

<!-- ======================================================================= -->
## is-set

* `isSet(s)` returns `true`, if value `s` is a set of values
* i.e. `true`, if value `s` has the characteristics of a set
* `(is-set s) := isSet(s)`

Note that `isMultiSet(s)` is understood to be true for sets.

<!-- ======================================================================= -->
## a set is a specialized multiset

* "specialized" such that the multiplicity of each value it holds is one/1

a set adopts the following definitions:

* a set of X, a set of atomic values
* a homogenous/heterogenous set of values
* (random) iteration
* multiplcitiyOf()
* sizeOf() := cardinalityOf()
* isEmpty(), `{}` represents an empty set
* (v in V), oneElementOf()

<!-- ======================================================================= -->
## add, remove

* the `add(x,V)` operation must be adjusted such that the
  multiplicity of `x` does not increase beyond `1`
* `(V == add(x,V)` will be true iff `(x in V)`
* the `remove(x,V)` operation does not need to be changed

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
