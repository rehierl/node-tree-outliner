
<!-- ======================================================================= -->
# Sequences

* see "mathematics" for the core concept of sequences
* see "formal languages" for string-related aspects
* see "topology" for "every sequence is a net"

<!-- ======================================================================= -->
## which term is appropriate?

* term "sequence" will be used in the course of this discussion
* in the course of this discussion, an "ordered sequence of nodes"

tuples

* `t := [1, 'a'] := (1,a)`
* an ordered list of "anything"
* in general of finite length

sequences

* `s := [1, 2, ...] := (1,2, ...)`
* an enumerated collection of "anything" of any length
* in general a rule exists such that subsequent elements
  in a sequence can be calculated from presequent ones
* e.g. `an := a(n-2) + a(n-1)` (Fibonacci)

strings

* `s := "abac..." := ['a', 'b', 'a', 'c', ...]`
* traditionally a sequence of characters
* elements are selected from an alphabet
* in computing generalized into a sequence of binary data
* depending on the context, a mutable/immutable sequence

vectors

* `v := [1.0, 2.0, 3.0] := < 1, 2, 3 >`
* in general an element of the real coordinate space (R^n)

<!-- ======================================================================= -->
## Sequences are more than "sequences"

* `s = [ e1, ..., eN ]` for `(s in ×Ti)`
* `(f: (×Ti,Index) -> Element)`
* note - closely related to orders
* note - distinct elements may hold the same value
* i.e. a sequence is a group of elements paired with an order-relation
* sequences represent ordered multisets - nope
* sequences may represent ordered sets

<!-- ======================================================================= -->
## left/right-bound notation

```
//- default notation
s = [ e1, e2, ..., eN ]
s = [ s[1], s[2], ..., s[N-1], s[N] ]
```

Given a sequence `s` of arbitrarily many elements, the "default notation" is
from left-to-right, i.e. from the first (`s[1]`) to the last element (`s[N]`).

```
//- left-bound, offset-based notation
t = [ s[l], s[l+1], ..., s[l+k-2], s[l+k-1] ]
t = [ s[o], s[o+1], ..., s[o+k-2], s[o+k-1] ]
```

* `l` is referred to as the "left border" (l) or "offset" (o)
* `k` represents the length of sequence `t` (i.e. `k = #t`)

Given a sequence `t` derived from sequence `s` by removing a prefix and/or
suffix from `s`, then `t` can be defined by using the above left-bound
notation: `infixLe(s,l,k) := [ s[o],...,s[o+k-1] ]`.

```
//- right-bound notation
t = [ s[r-k+1], s[r-k+2], ..., s[r-1], s[r] ]
```

* `r` is referred to as the "right border" (r)
* `k` represents the length of sequence `t` (i.e. `k = #t`)

Given a sequence `t` derived from sequence `s` by removing a prefix and/or
suffix from `s`, then `t` can be defined by using the above right-bound
notation: `infixRi(s,r,k) := [ s[r-k+1],...,s[r] ]`.
