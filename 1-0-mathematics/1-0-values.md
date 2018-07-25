
<!-- ======================================================================= -->
# Abstract values

( The intention behind introducing "values" and their "representatives" is to
avoid thinking in terms of concrete values like numbers, characters, etc. )

constant, immutable

* a value `v` (or a constant `c`) represents some specific abstract value
* no representative `v` can be changed to represent a different value
* e.g. the literal `'2'` represents the abstract number value `2`
* i.e. a `1:1` relationship between a value and its representative

primitive values

* a primitive value is understood to be "atomic"
* i.e. self-enclosed, indivisible units of information

number identifiers (ids)

* `v2, v:2` := some value `v` identified by number `2`
* multiple values can be distinguished by number identifiers
* `v1` and `v2` never hold the same abstract value

letter identifiers (ids)

* `vi, v:i` := some value `v` identified by `i in [1,N]`
* number identifiers may be generalized into letter identifiers
* `vi` represents one of the available values
* e.g. `(vi == v2)` for `i = 2`

clarification

* the value of `vi` can not be changed (i.e. constant, immutable)
* `vi` is not a variable, `vi` does not represent a reference of sorts
* it is an error to attempt to assign any value to `vi` - e.g. `vi = 2`

clarification

* `(v3 == v3)` and `(vi == vi)` are always true
* `(vi == vj)` is true iff `(i == j)`, false otherwise
* different identifiers always refer to different specific values

<!-- ======================================================================= -->
## is-atomic

* `(is-atomic v)`, `isAtomic(v)` returns `true`, if value `v` is atomic
* synonymous - atomic, primitive, simple

remarks

* an atomic value can not be split into distinct values
* i.e. self-enclosed, indivisible units of information
* e.g. numbers, characters, colors, etc.

remarks

* this does not mean that a value can not be created from another value
* however, the resulting value is a new distinct value
* i.e. a value never changes into another value

<!-- ======================================================================= -->
## is-complex

* `(is-complex v)`, `isComplex(v)` := `not (is-atomic v)`
* synonymous - complex, composite

remarks

* `complex := < (atomic|complex)* >`
* complex values represent groups of atomic and/or complex values
* an empty group `< >` is itself a complex value
* complex values may be hierarchical
* i.e. the members of a complex value may be atomic or complex
* e.g. multisets, sets, sequences, strings, etc.

constant, immutable

* like atomic values, complex values can not be changed
* replacing the member of a complex value will result in a distinct entity

homogenous, heterogenous

* a complex value is said to be homogenous, if
  all values used to create it share the same characteristic
* a complex value is otherwise said to be heterogenous
* e.g. a complex value is heterogenous, if not all of its members are atomic
* e.g. `c := < 2, 'd', ... >` is heterogenous

unordered, order-relation, ordered

* `comp-1 := < v1, v2, ... >`, `comp-2 := < v2, v1, ... >`
* by default, the members within a complex value are unordered
* i.e. a complex value has no first/last/3rd member
* i.e. `comp-1` and `comp-2` represent the same complex value
* additional information is needed to define such an order
* this information must be provided by an order-relation
* a complex value with no order-relation is an "unordered complex value"
* a complex value paired with an order-relation is an "ordered complex value"
