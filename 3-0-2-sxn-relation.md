
<!-- ======================================================================= -->
# The SxN relation

With regards to a tree of nodes, a section can initially be defined as a set of
nodes `s := { n1, ..., nk }`, and `k in [0,#N]` (or simply via `s subset-of N`).
Hence, operators defined for sets also apply to sections:

* `(isEmpty(s) == true)`, if `(#s == 0)` (put differently: `(s == {})`)
* `(n in s)`, if node `n` is an element of section `s`

Assumed that any number of sections is allowed, all sections of a tree can be
seen to be an element of some set-of-sections `S`:

* `s in S` for any section `s`

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

<!-- ======================================================================= -->
## (s related-to n)

So far, a `related-to` relation can only be defined based upon a direct
relationship between a section and its nodes:

* `(s strictly-related-to n)`, if `(n in s)`
* `(s strictly-related-to n) <=> (n strictly-related-to n)`

The only generalization currently possible is:

* `(s related-to n)`, if `(s strictly-related-to n)`
* `(s related-to n) <=> (n related-to s)`
* synonymous - `related-to`, `associated-with`

<!-- ======================================================================= -->
## Summary

The above definitions only allow to state if section `s`, that already contains
node `n`, is strictly related to node `n`, or if node `n` strictly belongs to
section `s`. This means, that in order to make such a statement, the
relationship between a section and its nodes must already exist.

* Why are nodes `n,x,y in N` related to sections `s,t in S`?
* for `(n != x != y)` and `(s != t)`

There is no definition that forces to establish any relationship between
nodes and sections: Under which circumstances must node `n` be associated
with section `s`?

* `(s ??? y)`, if `(s related-to x)` and `(y related-to x)`

There is no clarification of any relationship between a section
and those nodes that are related to some other, already associated node.

* `(s ??? t)`, if `(s related-to x)`, `(t related-to y)` and `(x related-to y)`

There is no clarification of any relationship between two different sections.
