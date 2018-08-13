
<!-- ======================================================================= -->
# Abstract, atomic and complex values

The intention behind introducing "values" and their "representatives" is to
move past thinking in terms of specific values like numbers, sequences, etc.

constant, immutable

* a value `v` (or a constant `c`) represents some specific abstract value
* no representative `v` can be changed to represent a different value
* e.g. the literal `'2'` represents the abstract number value `2`
* i.e. a fixed relationship between a value and its representative

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
* different identifiers always refer to different abstract values

<!-- ======================================================================= -->
## Atomic values

* a primitive value can not be split into distinct atomic values
* i.e. atomic, self-enclosed, indivisible units of information
* e.g. numbers, characters, colors, etc.

### is-atomic

* `(is-atomic v)`, `isAtomic(v)` returns `true`, if value `v` is atomic
* synonymous - atomic, primitive, simple

### is-complex

* `(is-complex v)`, `isComplex(v)` := `not (is-atomic v)`
* synonymous - complex, composite, compound

<!-- ======================================================================= -->
## Components

components are the building blocks of complex values

* components are used to group values into more complex values
* in addition to their value, components may have further properties
* e.g. a reference to the next/previous component
* components therefore allow to define the structure of complex values

components represent abstract values

* components hold abstract or complex values
* i.e. complex values may themselves be hierarchical
* components hold one value, and one value only

components are immutable entities

* the value of a component is never undefined
* the value of a component is set during the creation of a complex value
* after that, the value of a component can not be changed (i.e. immutable)

components are globally unique entities

* complex values do not share the same components
* no complex value contains a component more than once
* complex values represent groups of unique of components
* any component always belongs to a complex value

### (value-of c)

* `c.value` := the value of component `c`
* `(value-of c), valueOf(c) := c.value`

### (v == c)

* `(c == v), (v value-of c) := (c.value == v)`
* `(ci == cj)`, if `(ci.value == cj.value)`

clarification

* `(c == v) <-> (v == c)`
* the test for equality refers to the values the components hold
* i.e. components are implicitly dereferenced

clarification

* `(ci == ci)` is always true
* `(ci == cj)` is not necessarily true

### (c1 === c2)

* `(ci === cj)` is true iff `(i == j)`
* i.e. both reference the same component
* `(ci !== cj)` is true iff `(i != j)`
* i.e. both reference different components

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
* complex values represent groups of unique components
* each component within a complex value holds an abstract value
* by default, any component may hold any value
* an empty group `< >` is itself a complex value
* e.g. multisets, sets, sequences, strings, etc.

constant, immutable

* like atomic values, complex values can not be changed
* i.e. replacing the value of a component will yield a different complex value

homogenous, heterogenous

* a complex value is homogenous, if its elements share certain characteristics
* heterogenous - its elements have different characteristics
* e.g. a complex value is heterogenous, if not all of its members are atomic
* e.g. the complex value `c := < 2, 'd', ... >` is heterogenous

unordered, ordered, order-relation

* by default, the components within a complex value have no order
* i.e. components have by default no relationship with each other
* i.e. other than being part of the same or different complex values
* i.e. a complex value has no first/last/n-th component
* additional information is needed to define such an order
* this information must be provided by an associated order-relation
* unordered complex value - a complex value with no associated order-relation
* ordered complex value - a complex value paired with an order-relation

<!-- ======================================================================= -->
## Components vs. Elements

The intention of introducing "components" (aka. slots or containers) is to
avoid confusion with the "elements" of a complex value.

components

* components are unique entities that hold/represent values/elements
* no complex value contains a component more than once
* distinct complex values do not share any components

values/elements

* the term "element" is in general used synonymous to "(abstract) value"
* elements are not necessarily unique to complex values
* a complex value may contain elements more than once
* complex values may share the same elements

Note that the term "element" is used to point out that a value belongs to a
complex value. That is, the term emphasizes the relationship with a complex
value. In contrary to that, the term "value" focuses more on isolated entities.

clarification

* components are used to define the structure of a complex value
* components and elements combined define complex values

<!-- ======================================================================= -->
## Cardinality

* `#V, #(V)` := the number of components within the complex value `V`
* `(cardinality-of V), cardinalityOf(V) := #V`
* similar, but not synonymous terms - size, length, strength, power

Note that the cardinality of a complex value is in general understood
to refer to the number of components needed to hold its elements.

* `#(v,V)` := the number of components within `V` that hold value `v`
* the cardinality of an element is also known as its "multiplicity"
* the cardinality of a value, which is not an element of `V`, is zero/0

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
