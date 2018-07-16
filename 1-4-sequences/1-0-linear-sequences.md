
<!-- ======================================================================= -->
## Linear set/sequence

* the focus is on sequences derived from sets of elements
* each element within a sequence appears no more than once (a set)
* the order of elements in such a sequence corresponds with some order
* the indexes of those elements reflects that order (subsequent)
* referred to as a "distinct sequence", or as a "linear set/sequence"
* the notation used in the context of this discussion is: **[{..}]**
* as it denotes "a sequentialized set of elements"

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
## linear sequence

* `(is-linear s), (is-linear s) := isLinear(s)`
* `isLinear(s)` := `(s[i] != s[j])` for any `i,j in [1,#s]` and `(i != j)`

A sequence is said to be linear, if the sequence holds unique/distinct elements
only. That is, a linear sequence contains none of its elements more than once.
As such, a linear sequence can be understood to define a simple set of elements.

In addition to that, a linear sequence defines an ordered set (see relations),
if the order of positions is understood to correspond with the set's order of
elements. Depending on the respective context, the semantics of the element
order may therefore be:

* `(s[i] before s[i+1])`, `(s[i] presequent-to s[i+1])`
* `(s[i+1] after s[i])`, `(s[i+1] subsequent-to s[i])`

The word "linear" therefore needs to be understood
with regards to the "linear order" it defines.

Note that set-based operators can be used in combination with linear sequences.

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
