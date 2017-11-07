
<!-- ======================================================================= -->
# Variables, Elements

* a variable `var` (or an element `e`) represents some value `v`
* in contrary to values, the value of a variable may change over time

### value of

* 

clarification

* different elements may represent the same value
* `(ei !== ej) !> (ei != ej)`, e.g. `(e1 == v) and (e2 == v)`
* different elements may represent different values
* `(ei == ej) !> (ei === ej)`, e.g. `(i != j)`
* an element can not represent different values at the same time
* `(ei != ej) => (ei !== ej)`, i.e. `(i != j)`
* `(ei === ej) => (ei == ej)`, i.e. `(i == j)`

<!-- ======================================================================= -->
## Type, Domain

* the values a variable may represent is limited to a set of values
* 

<!-- ======================================================================= -->
## Sets of elements

* `E = {e1, e2, ...}` represents a set of elements
* `E` **contains** element `ei`, if `ei in E` is true
* `ei` **belongs to** `E`, if `ei in E` is true

* An element `e1` **belongs to** a set of elements,
  if that set **contains** the given element -
  i.e. if `e1 in E` is true

Any element `e(i)` is an element of its **domain** `E(i)` -
i.e. `e(i) in E(i)`, or simply `ei in Ei`.

* each element `e(i)` belongs to some set `E(i) = {`
