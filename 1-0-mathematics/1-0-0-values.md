
<!-- ======================================================================= -->
# Abstract, atomic and complex values

( The intention behind introducing "values" and their "representatives" is to
move past thinking in terms of concrete values like numbers, strings, etc. )

constant, immutable

* a value `v` (or a constant `c`) represents some specific abstract value
* no representative `v` can be changed to represent a different value
* e.g. the literal `'2'` represents the abstract number value `2`
* i.e. a fixed relationship between a value and its representative

primitive values

* a primitive value is understood to be "atomic"
* i.e. self-enclosed, indivisible units of information

number identifiers (ids)

* `v2, v:2` := some value `v` identified by number `2`
* multiple values can be distinguished by number identifiers
* `v1` and `v2` never hold the same abstract value

letter identifiers (ids)

* `vi, v:i` := some value `v` identified by `(i in [1,N])`
* number identifiers may be generalized into letter identifiers
* `vi` represents one of the available values
* e.g. `(vi == v2)` iff `(i == 2)`

clarification

* the value of `vi` can not be changed (i.e. constant, immutable)
* `vi` is not a variable, `vi` does not represent a reference of sorts
* it is an error to attempt to assign any value to `vi` - e.g. `vi = 2`

clarification

* `(v3 == v3)` and `(vi == vi)` are always true
* `(vi == vj)` is true iff `(i == j)`, false otherwise
* different identifiers always refer to different specific values

<!-- ======================================================================= -->
## Atomic values

* an atomic value can not be split into distinct values
* i.e. self-enclosed, indivisible units of information
* e.g. numbers, characters, colors, etc.

### is-atomic

* `(is-atomic v)`, `isAtomic(v)` returns `true`, if value `v` is atomic
* synonymous - atomic, primitive, simple

### is-complex

* `(is-complex v)`, `isComplex(v)` := `not (is-atomic v)`
* synonymous - complex, composite, compound

<!-- ======================================================================= -->
## Components

( The intention behind the introduction of "components" is to avoid confusion
with the "elements" of a complex value - i.e. distinguish between "elements"
and "components". The term "element" is in general used to refer to the value
of a component. That is, both terms refer to distinct concepts. )

* aka. slot, component, container
* components represent the bearers of atomic or complex values
* components are used to group values into more complex values
* components allow to define the structure of complex values

components always hold a single value

* they hold one value, and one value only
* a component always holds a defined value
* the value of a component is never undefined

components are immutable entities/objects

* the value a component holds is set during the creation of a complex value
* after that, the value of a component can not be changed (i.e. immutable)

components need to be understood as being globally unique

* complex values do not share the same components
* no complex value contains a component more than once
* complex values are sets of components

### (value-of c)

* `c.value` := the value of component `c`
* `(value-of c), valueOf(c) := c.value`

### (v == c)

* `(c == v), (v value-of c) := (c.value == v)`
* `(ci == cj)`, if `(ci.value == cj.value)`

clarification

* `(c == v) <-> (v == c)`
* the test for equality refers to the values components hold
* i.e. components are implicitly dereferenced to their values

clarification

* `(ci == ci)` is always true
* `(ci == cj)` is not necessarily true

### (c1 === c2)

* `(c1 === c2)` is true if `c1` and `c2` represent the same component
* `(c1 !== c2)` is true if `c1` and `c2` represent different components

clarification

* `(ci !== cj) =!> (ci != cj)`
* `(ci == cj) =!> (ci === cj)`
* different components may hold the same value
* `(ci != cj) -> (ci !== cj)`, i.e. `(i != j)`
* `(ci === cj) -> (ci == cj)`, i.e. `(i == j)`
* a component can not represent several different values

clarification

* a component can not hold multiple values at the same time
* multiple components are needed to hold different values
* different components may however hold identical values

<!-- ======================================================================= -->
## Complex values

* `complex := < (atomic|complex)* >`
* complex values represent groups of atomic and/or complex values
* i.e. complex values may themselves be hierarchical
* an empty group `< >` is itself a complex value
* e.g. multisets, sets, sequences, strings, etc.

constant, immutable

* like atomic values, complex values can not be changed
* replacing the element of a complex value will result in a new complex value
* i.e. the elements of a complex value can not be replaced

homogenous, heterogenous

* a complex value is said to be homogenous,
  if all values used to create it share the same characteristics
* otherwise, a complex value is said to be heterogenous
* e.g. a complex value is heterogenous, if not all of its members are atomic
* e.g. `c := < 2, 'd', ... >` is heterogenous

unordered, ordered, order-relation

* `x := < v1, v2, ... >`, `y := < v2, v1, ... >`
* by default, the components within a complex value have no order
* i.e. a complex value has no first/last/n-th component
* i.e. `x` and `y` represent the same complex value
* additional information is needed to define such an order
* this information must be provided by an associated order-relation
* a complex value with no order-relation is an "unordered complex value"
* a complex value paired with an order-relation is an "ordered complex value"

<!-- ======================================================================= -->
## Cardinality

* `#V, #(V)` := the number of components in some complex value `V`
* `(cardinality-of V), cardinalityOf(V) := #V`
* similar, but not synonymous terms - size, length, strength, power

Note that the cardinality of a complex value is in general understood
to refer to the number of components needed to hold its values/elements.

### wikipedia, equinumerosity

* two sets A and B are equinumerous, if a bijection exists between them
* i.e. for every element (y in B) there is one element (x in A) - f(x)=y
* both sets are then said to have the same cardinality
* has properties of an equivalence relation
* A~B, |A|=|B| - both sets are equinumerous

examples

* the sets of natural and real numbers are not equinumerous
* i.e. there are different kinds of infinity
* the sets of natural and rational numbers however are
* i.e. the proper subset of an infinite set may be equinumerous

### wikipedia, cardinality

* cardinality of a set - the number of its elements
* in the context of a set - aka. the set's size
* notations - |S|, n(S), card(S), #S

comparing sets

* functional definition - e.g. in the context of infinite sets
* (#S = #T), if a bijection exists between sets S and T
* (#S <= #T), if an injective function exists between both sets
* (#S < #T), if an injective, but no bijective, function exists

cardinal numbers

* equivalence class - all sets that have the same cardinality
* a representative set is designated for each class
