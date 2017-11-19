
<!-- ======================================================================= -->
# The SxN relation

With regards to a tree of nodes, a section can initially be defined as a set of
nodes `s := { n1, ..., nk }`, and `k in [0,#N]` (or simply via `s subset-of N`).
Hence, the common operators defined for sets also apply to sections:

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

So far, the above definitions only allow to state if a section strictly contains
a given node, or if a node strictly belongs to some section.

There is no definition of any relationship between a section and those nodes
that are related to some node, which itself is associated with that section:

* `(s ??? nk)`, if `(s related-to n)` and `(n related-to nk)`

There is no definition of any relationship between two different sections:

* `(s1 ??? s2)`, if `(s1 and s2 in S)` and `(s1 !== s2)`
