
<!-- ======================================================================= -->
# Variables, Elements

* a variable `var` (aka. element `e`) represents some value `v`
* in contrary to actual values, the value of a variable may change

clarification

* `ms := < e1, e2 >`
* variables/elements are values

<!-- ======================================================================= -->
## value-of e

* `(e.value == v)`, if value `v` was assigned to `e`
* `(value-of e), valueOf(e) := e.value`

<!-- ======================================================================= -->
## v value-of e

* `(e == v), (v value-of e) := (valueOf(e) == v)`
* `(ei == ej)`, if `(valueOf(ei) == valueOf(ej))`

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
* different elements are needed to store different values
* different elements may hold the same value
