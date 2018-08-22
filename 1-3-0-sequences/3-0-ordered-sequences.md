
<!-- ======================================================================= -->
# Ordered sequences

As mentioned before, each node will be added to one or more sequences such that
no sequence contains a node more than once. Because of that, the set of elements
`E(s)` of a sequence `s` is therefore such that `(#E(s) == #s)`.

Furthermore, all nodes are added to sequences one after another in an orderly
fashion. Because of that, the index of each node in `s` corresponds with the
tree traversal's enter order. That is, `(s[i] < s[j])` iff `(i < j)`, where `<`
in the context of nodes represents the `entered-before` relationship between
nodes. As such, no node sequence contains any pair of incomparable nodes, which
is why a node sequence can be understood to define an ordered set of nodes `P`:

* `s = [{ n1, ..., nk }] in N*` is an ordered sequence of nodes
* `(E(s) subset-of N)` and `(#E(s) == #s)` are both true
* `P := (E(s),<)` where `(s[i] < s[j])` iff `(i < j)`
* `P` is an ordered set of nodes in enter order
* `sem(P)` := `xPy` iff `(x entered-before y)`
* `P` is a strict total order

Note that a sequence of elements, for which `(#E(s) == #s)` is true, will in
general be referred to as an **ordered sequence**, or as a **linear sequence**.
As such they can be understood to represent totally/linearly ordered sets.

<!-- ======================================================================= -->
## general characteristics

* the focus is on sequences `s` derived from some set `S`
* i.e. `(s[i] in S)` for some given set of elements `S`
* no sequence contains an element more than once
* i.e. `(#E(s) == #s)`
* the order of elements in `s` corresponds with a total order on `S`
* i.e. a strict monotone index-to-element mapping exists
* i.e. `(s[i] < s[j])` iff `(i < j)`
* an ordered sequence can respond with the index of an element
* i.e. `indexOf(e)` := `0` if `(e !in E(s))`, `+1` if `(e == s[1])`, etc.

pre-/in-/sub-sequent

* `(s[i] pre-sequent-to s[j])` iff `(i < j)`
* `(s[i] in-sequent-to s[j])` iff `(i == j)`
* `(s[i] sub-sequent-to s[j])` iff `(i > j)`

subsequences of ordered sequences

* each non-empty subsequence has a least (first) and a greatest (last)

<!-- ======================================================================= -->
## notational aspects

`V1 := { +, 1, @, a }`

* the elements in simple set `V1` have no order, they are mere symbols
* implicit ordinal numbers associated with elements may still exist
  (e.g. ascii/utf-8 code-points), but are not required to be relevant
  in a given context

`V2 := { b, a, c }` <=!=> `V3 := { c, a, b }, order-by:"utf-8"`

* `V2` is not necessarily an ordered set, if the element order is unclear
* without clarification, `a` in `V2` can be understood to be subsequent to `b`
* one could also assume some implicit order (e.g. "order of appearance")

`V4 := [{ a, b, c }]`

* the elements in `V4` have an order - `(a < b)` and `(b < c)`
* each element has an ordinal number (index) associated with it

`V5 := < a, b, a, c >`

* this group is neither an ordered set, nor a simple set of values
* not all components in `V5` hold unique elements
* i.e. `(a < b)` and `(b < a)` can not both be true

notation for "ordered/linear sequences"

* note the issue of using `{` and `}` for simple and ordered sets
* both symbols don't allow to distinguish a simple set from an ordered set
* use (`{[`, `]}`) or (`[{`, `}]`) instead of only (`{`, `}`)
* `{[, ]}` - could be mis-understood as a set of sequences
* `[{, }]` - could be mis-understood as a sequence of sets
* read `[{` and `}]` as a "sequence that holds an ordered set"
* i.e. the set is ordered according to the index of its elements

The order of symbols in `[{` and `}]` seems to best reflect the general notion
of ordered sequences as "linearized/sequentialized sets of elements".

<!-- ======================================================================= -->
## is-ordered

* `isOrdered(s)` := `(s[i] != s[j])` for all `(i != j)`
* `(is-linear s), (is-ordered s) := isOrdered(s)`

Note that the semantics of the implied order depends on a given context.
