
<!-- ======================================================================= -->
# A (simple) set of values

```
(simple) sets
-------------
order:  none

slots:  c1 c2
        |  |
values: v1 v2
```

* see "set theory" for further details

<!-- ======================================================================= -->
## core concept

* values may be grouped into (simple) sets of values
* sets of values are not paired with an order-relation
* hint - "simple" because "not ordered"
* sets of values are complex values

`V := { v1, v2 }`

* each set contains a value no more than once
* i.e. each value must be unique

`V := { c1:v1, c2:v2 }`

* a set of values can be understood to hold one component per element
* the number of components in a set is referred to as "cardinality"
* the components within a set have no order - i.e. no first/last component
* no component is allowed to hold the value of another component
* i.e. the multiplicity of each value within a set is one/1
* i.e. a `1:1` relationship between its elements and components
* i.e. "values", "elements" and "component" may be used synonymously
* `(vi != vj) <-> (ei !== ej)`

definition

* `V := { vi | (vi holds an odd integer) }`
* instead of listing each value, sets can be defined by
  specifying a condition that must be satisfied by each value
* alternative notations - `{:}`, `{;}`, `{,}`, etc.
* this style of notation may be referred to as the "set-builder" notation

clarification

* the number of elements in a set is referred to as its "size"
* in contrary to multisets, `(sizeOf(set) == lengthOf(set))` is always true
* i.e. the "size" of a set is always equal to its cardinality

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
## simple sets are specialized multisets

* "specialized" such that the multiplicity of each element is one/1

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

<!-- ======================================================================= -->
## wikipedia, complement (*)

* all sets are understood to be subsets of a universal set U
* (absolute) complement - A* := (U \ A) - i.e. the default definition
* relative complement - (B \ A)

properties

* (A + B)* = A* & B*
* (A & B)* = A* + B*
* U = (A + A*)
* {} = (A & A*)
* {}* = U
* U* = {}
* A = (A*)* - aka. involution
* (A strict-subset-of B) => (B* strict-subset-of A*)
