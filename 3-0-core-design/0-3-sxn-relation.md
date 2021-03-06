
<!-- ======================================================================= -->
# The SxN relation

With regards to a tree of nodes, a section can initially be defined as a set of
nodes `s := { n1, ..., nk }`, and `k in [0,#N]` (or simply `(s subset-of N)`).
Hence, operators defined for sets also apply to sections:

* `isEmpty(s)` is true, if `(#s == 0)` (or `(s == {})`)
* `(n in s)` is true, if node `n` is an element of section `s`

Assumed that any number of sections is allowed, all sections of a tree can be
understood to be an element of some set of all-declared-sections `S`:

* `(s in S)` is true for any section `s`

<!-- ======================================================================= -->
## (s contains n)

With that in mind, a binary relation can be defined as follows:

* `R := (S,N,G)` where `S` is the set of sections and `N` the set of nodes
* `G := { (s,n) : (s in S), (n in N), (n in s) }`
* `sem(R) := (s contains n)`

This relation will be referred to as the `SxN` relation. Similar to this
definition, a relation can be defined that is antonymous to it:

* `(n element-of s)`, if `(n in s)`
* sem := node `n` is an element of section `s`
* synonymous - `element-of`, `belongs-to`, `located-inside`

Note that the direction of the `contains` relation is downwards (i.e. from a
superordinate entity towards a subordinate entity) and that the `element-of`
relation is antonymous to it.

Note that this relation does not yet define any specific structure. That is,
the relation merely states which nodes belong to which section. In addition to
that, any node may belong to one or more sections. However, any given section
may contain a specific node no more than once.

<!-- ======================================================================= -->
## (s related-to n)

So far, a `related-to` relation can only be defined based on a direct
relationship between a section and its nodes:

* `(s strictly-related-to n)`, if `(n in s)`
* `(s strictly-related-to n) <=> (n strictly-related-to n)`

The only generalization currently possible is:

* `(s related-to n)`, if `(s strictly-related-to n)`
* `(s related-to n) <=> (n related-to s)`
* synonymous - `related-to`, `associated-with`

Note that the `related-to` relation has no orientation (aka. is un-directional).

<!-- ======================================================================= -->
## questions

The above definitions only allow to state if section `s`, that already contains
node `n`, is strictly related to node `n`, or if node `n` strictly belongs to
section `s`. This means that, in order to make a statement, the relationship
between a section and its nodes must already exist.

* So, why is node `n in N` related to section `s in S`?

There is no definition that clarifies under which circumstances certain nodes
have to be associated with a given section.

* `(s ??? y)`, if `(s related-to x)` and `(y related-to x)`
* for `x,y in N`, `s in S` and `(x != y)`

There is no clarification of any relationship between a section and those nodes
that are related to some other, already associated node.

* `(s ??? t)`, if `(s related-to x)`, `(t related-to y)` and `(x related-to y)`
* for `x,y in N`, `s,t in S`, `(x != y)`, and `(s != t)`

There is no clarification of any relationship between two different sections,
if all the content nodes of a section are also content nodes of another section.
