
<!-- ======================================================================= -->
# A (simple) set of elements

```
(simple) sets (no order)
------------------------
components:  c1 c2 c3
             |  |  |
elements:    v1 v2 v3
```

* (/see/ "set theory" /)

Note that simple sets are specialized multisets such that the multiplicity
of each element can not increase past one/1. Also, a set is a nested set,
if it has elements that are themselves sets.

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
