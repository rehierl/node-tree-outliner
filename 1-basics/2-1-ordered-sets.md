
<!-- ======================================================================= -->
# Ordered sets of values

simple sets of values

* a set is a group of values in which all values are different
* the values in a (simple) set have no order
* a (simple) set has no first, no last, and no n-th value
* a set can essentially only answer the "element-of" question
* due to "no order" and the "in" operator, a set appears as a black box

ordered sets of values

* an ordered set of values is a simple set of values
* the values in an ordered set of values have an order

order-related properties

* an ordered set has a first, a last, and an n-th value
* every value `v(n)` has a previous `v(n-1)` and a next `v(n+1)` sibling
* an ordered set of values can respond with the index of a given value
* e.g. `-1` if does not contain a value, `1` if it's the first value, etc.

pre-sequent, in-sequent, sub-sequent

* `v(n)` is subsequent to `v(n-1)`
* `v(n)` is presequent to `v(n+1)`
* `v(n)` is insequent to itself

<!-- ======================================================================= -->
## Examples

* note the issue of using `{` and `}` for simple and ordered sets
* both symbols don't allow to distinguish a simple from an ordered set
* use (`{[`, `]}`) or (`[{`, `}]`) instead of (`{`, `}`) ?!?

`V1 := { +, 1, @, a }`

* the elements in `V1` have no order, they are mere symbols
* any implicit ordinal number must be ignored (e.g. ascii, utf-8, etc.)

`V2 := { a, b, c }` <=> `V3 := { b, a, c}, order-by:"utf-8"`

* this set is not necessarily an ordered set, if the order is not clear
* without the clarification, `b` can be understood to come before `a`
* one could however assume "in order of appearance"

`V4 := { a, b, c }`

* the elements in `V2` have an order, `a` comes before `b` and `b` before `c`
* the elements need to be understood to represent more than mere symbols
* each element has an implicit ordinal number associated with it

`V5 := { a, b, a, c }`

* this group is neither an ordered set, nor a simple set of values
* not all elements within that group are unique
