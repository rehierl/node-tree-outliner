
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

<!-- ======================================================================= -->
## domain of, type of

* `e.domain := V`, if `e` may represent any value `v in V`
* `dom(e), domainOf(e), (domain-of e) := e.domain`
* `typeOf(e), (type-of e) := e.domain`
* the value `v` an element `e` may represent is limited to a set of values `V`
* signature - (element) -> set

clarification

* `domainOf(v) := { v }`
* a value can not represent any other value
* the domain of a value is essentially the value itself

<!-- ======================================================================= -->
## V domain of e

* `(V domain-of e), (V type-of e) := (e.domain == V)`
* `V` is said to be the domain or type of element `e`
* signature - (set,element) -> boolean

