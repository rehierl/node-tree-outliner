
<!-- ======================================================================= -->
# Ordered sets of values

simple sets of values

* a simple set of values is a group of values in which all values are different
* the values of a (simple) set of values have no order
* a (simple) set has no first, no last, and no n-th value
* due to having "no order" and the `in` operator, a set appears as a black box
* the only question that can be answered is whether a set "contains" a value

ordered sets of values

* an ordered set of values is a simple set of values
* the values in an ordered set of values have an order
* an ordered set has a first, a last, and an n-th value
* every value `v(n)` has a previous `v(n-1)` and a next `v(n+1)` sibling
* an ordered set of values can respond with the index of a given value -
  e.g. `-1` if does not contain a value, `1` if it's the first value, etc.

<!-- ======================================================================= -->
## Examples

`V1 := { +, 1, @, a }`

* the elements in `V1` have no order, they are mere symbols
* the elements need to be understood to represent mere symbols/images
* any implicit ordinal number must be ignored (e.g. ascii, utf-8, etc.)

`V2 := { a, b, c }`

* the elements in `V2` have an order, `a` comes before `b` and `b` before `c`
* the elements need to be understood to represent more than mere symbols
* each element has an implicit ordinal number associated with it

`V3 := { a, a, b, c }`

* this group is neither an ordered set, nor a simple set of values
* not all elements within that group are unique
