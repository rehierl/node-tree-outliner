
<!-- ======================================================================= -->
# A (simple) set of elements

```
(simple) sets
-------------
order:       none

components:  c1 c2
             |  |
elements:    v1 v2
```

* see "set theory" for further details

<!-- ======================================================================= -->
## core concept

* elements may be grouped into (simple) sets of elements
* (simple) sets of elements are not paired with an order-relation
* hint - "simple" because "not ordered"
* sets of elements are complex values

`V := { v1, v2 }`

* each set contains an element no more than once
* i.e. each element must be unique within its set

`V := { c1:v1, c2:v2 }`

* a set of elements holds one component per element
* the components within a set have no order - i.e. no first/last component
* no component is allowed to hold the element of another component
* i.e. the multiplicity of each element within a set is one/1
* i.e. `(#(v,V) == 1)` for all `(v in V)`
* i.e. a `1:1` relationship between its elements and components
* i.e. "values", "elements" and "component" may be used synonymously
* `(vi != vj) <-> (ei !== ej)`

"set-builder" notation

* `V := { vi | (vi holds an odd integer) }`
* instead of listing each element, sets can be defined by
  specifying a condition that must be satisfied by each element
* alternative notations - `{:}`, `{;}`, `{,}`, etc.

clarification

* the number of elements in a set is referred to as its "size"
* i.e. the "size" of a set is always equal to its cardinality
* in contrary to multisets, `(sizeOf(set) == lengthOf(set))` is always true

<!-- ======================================================================= -->
## is-set

* `isSet(s)` returns `true`, if value `s` is a set of elements
* i.e. `true`, if value `s` has the characteristics of a set
* `(is-set s) := isSet(s)`

Note that `isMultiSet(s)` is understood to be true for sets.

<!-- ======================================================================= -->
## sets are specialized multisets

* "specialized" such that the multiplicity of each element is one/1

a set adopts the following definitions:

* a set of X, a set of atomic elements, etc.
* a homogenous/heterogenous set of elements
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

* `(A union B) := { x | (x in A) or (x in B) }`
* `(A or B), (A + B) := (A union B)`

likewise

* `(A + b) := (A + {b})`
* `(a + B) := ({a} + B)`
* `(a + b), ({a} + {b}) := {a, b}`

clarification

* `((A + B) + C) <-> (A + (B + C))`
* `((a + b) + c) <-> (a + (b + c))`

<!-- ======================================================================= -->
## intersection (&, and, isect)

* `(A isect B) := { x | (x in A) and (x in B) }`
* `(A & B), (A and B) := (A isect B)`

<!-- ======================================================================= -->
## set difference (\, sub, diff)

* `(A diff B) := { x | (x in A) and (x !in B) }`
* `(A \ B), (A sub B) := (A diff B)`

<!-- ======================================================================= -->
## symmetric difference (^, xor, ex-or)

* `(A ex-or B) := { x | x in (A\B or B\A) }`
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
