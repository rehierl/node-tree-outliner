
<!-- ======================================================================= -->
# Ordered sets

simple sets of values

* a set is a group of values in which all values are different
* the values in a (simple) set have no order whatsoever
* a simple set has no first, no last, and no n-th value
* a set can essentially only answer the "element-of" question
* due to "no order" and the "in" operator, a set appears as a black box

ordered sets of values

* a (simple) set of elements paired with some order
* the order relation defines the relationship between the elements

<!-- ======================================================================= -->
## Linear set/sequence (`[{...}]`)

* the focus is on sequences derived from sets of elements
* each element within a sequence appears no more than once (a set)
* the order of elements in such a sequence corresponds with some order
* the indexes of those elements reflects that order (subsequent)
* referred to as a "distinct sequence", or as a "linear set/sequence"

order-related properties

* a (finite) linear set has a first, a last, and an n-th element
* every value `v(n)` has a predecessor `v(n-1)` and a successor `v(n+1)`
* a linear set can respond with the index of any given value
* e.g. `0` if not found, `+1` if it's the first value, etc.
* i.e. a strict monotone mapping between both orders (elements-to-index)

pre-sequent, in-sequent, sub-sequent

* `v(n)` is subsequent to `v(n-1)`
* `v(n)` is presequent to `v(n+1)`
* `v(n)` is insequent to itself

notation for "linear sets/sequences"

* note the issue of using `{` and `}` for simple and linear sets
* both symbols don't allow to distinguish a simple set from a linear set
* use (`{[`, `]}`) or (`[{`, `}]`) instead of only (`{`, `}`) ?!?
* `{[, ]}` - could be mis-understood as a set of sequences
* `[{, }]` - could be mis-understood as a sequence of sets
* read `[{,}]` as a "linearized/sequentialized set" 
* read `[{,}]` a "sequence which holds a linear set"
* the order of symbols in `[{,}]` seems to best reflect the order of words

<!-- ======================================================================= -->
## Examples

`V1 := { +, 1, @, a }`

* the elements in `V1` have no order, they are mere symbols
* any implicit ordinal number must be ignored (e.g. ascii, utf-8, etc.)

`V2 := { b, a, c }` <=> `V3 := { c, a, b }, order-by:"utf-8"`

* V2 is not necessarily an ordered set, if the order is unclear
* without clarification, `b` can be understood to come before `a`
* one could assume some other implicit order (e.g. alphabetical)
* one could also assume "in order of appearance"

`V4 := [{ a, b, c }]`

* the elements in V4 have an order - `a` comes before `b` and `b` before `c`
* the elements need to be understood to represent more than mere symbols
* each element has an implicit ordinal number associated with it

`V5 := < a, b, a, c >`

* this group is neither an ordered set, nor a simple set of values
* not all elements within that multiset are unique
