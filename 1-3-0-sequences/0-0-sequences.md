
<!-- ======================================================================= -->
# Sequences

* see "mathematics" for the core concept of sequences.
* see "topology" for "every sequence is a net".

Note that, in the course of this discussion, the focus will be on "linear
orders of nodes" which result from some tree traversal.

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
