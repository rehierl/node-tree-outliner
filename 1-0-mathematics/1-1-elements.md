
<!-- ======================================================================= -->
# Elements

* aka. container, slot, member
* an element represents the bearer of a value
* elements are used to group values into complex values
* elements may hold atomic or complex values
* elements allow to describe the structure of complex values

clarification

* the value of an element is set during the creation of a complex value
* after that, the value of an element can not be changed (immutable)

<!-- ======================================================================= -->
## value-of e

* `(e.value == v)` is true, if value `v` was assigned to `e`
* `(value-of e), valueOf(e) := e.value`

<!-- ======================================================================= -->
## v value-of e

* `(e == v), (v value-of e) := (e.value == v)`
* `(ei == ej)`, if `(ei.value == ej.value)`

clarification

* `(ei == ei)` is always true
* `(ei !== ej) =!> (ei != ej)`
* `(ei == ej) =!> (ei === ej)`
* different elements may hold the same value
* `(ei != ej) -> (ei !== ej)`, i.e. `(i != j)`
* `(ei === ej) -> (ei == ej)`, i.e. `(i == j)`
* an element can not represent different values at the same time

clarification

* an element can not hold multiple values at the same time
* different elements are needed to hold different values
* different elements may however hold the same value
