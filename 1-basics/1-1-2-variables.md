
<!-- ======================================================================= -->
# Variables, Elements

* a variable `var` (aka. element `e`) represents some value `v`
* in contrary to values, the value of a variable may change over time

<!-- ======================================================================= -->
## value of e

* `e.value := v`, if value `v` was assigned to `e`
* `(value-of e), valueOf(e) := e.value`
* signature - (element) -> value

<!-- ======================================================================= -->
## v value of e

* `(e == v), (v value-of e) := (valueOf(e) == v)`
* `(ei == ej)`, if `(valueOf(ei) == valueOf(ej))`
* signature - (value,element) -> boolean

clarification

* `(ei == ei)` is always true
* different elements may represent the same value
* `(ei !== ej) !> (ei != ej)`, e.g. `(e1 == v) and (e2 == v)`
* different elements may represent different values
* two elements aren't necessarily identical, if they hold the same value
* `(ei == ej) !> (ei === ej)`, e.g. `(i != j)`
* an element can not represent different values at the same time
* `(ei != ej) => (ei !== ej)`, i.e. `(i != j)`, but not `<=`
* `(ei === ej) => (ei == ej)`, i.e. `(i == j)`

clarification

* an element can not store different values at the same time
* different elements are needed to store different values
* different elements may still represent the same value
