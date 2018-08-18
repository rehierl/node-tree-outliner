
<!-- ======================================================================= -->
# Subsequence

<!-- ======================================================================= -->
## ( s -> t )

Given a sequence `s` of arbitrarily many elements, the "default notation" is
from left-to-right, i.e. from the first (`s[1]`) to the last element (`s[N]`):

* `s := [ e1, e2, ..., eN ]`
* `s := [ s[1], ..., s[N] ]`
* `s := [ s1, s2, ..., sN ]`

The `get` access property of sequence `s` can be used to create a clone of `s`:

* `t := [ si ]` for `(i in [1,N])`
* `t := [ s1, s2, ..., sN ]`

The created sequence `t` however does not have to be equal to `s`. Any number
of elements in `s` may be omitted. That is, the multiplicity of elements taken
form `s` may be zero/0 in `t`:

* `t := [ s2, s3, s4, s5 ]`

In addition to that, the elements taken from `s` may be rearranged in `t`:

* `t := [ s3, s6, s2, s1 ]`

Finally, new sequences can be created by taking elements from `s` and adding
them several times to the sequences being created:

* `t := [ s2, s5, s2, s5 ]`

Note that the new sequence `t`, which was created from sequence `s`, is in
relationship with `s`. That is `t`, similar to the `subset-of` relationship,
contains one or more elements from `s`. The focus of this section is therefore
on reducing the number of options used to create new sequences (i.e. arrangement
of elements, multiplicity) in order to define the relationship between sequences.

<!-- ======================================================================= -->
## left/right-bound notation

In general, a new sequence `t` can be created from an existing sequence `s` by
removing a prefix and/or a suffix from `s`. Sequence `t` can be defined using
a "left-bound" (aka. an "offset-based") notation:

* `infixLe(s,l,k) := t`
* `t = [ s[l], s[l+1], ..., s[l+k-2], s[l+k-1] ]`
* `t = [ s[o], s[o+1], ..., s[o+k-2], s[o+k-1] ]`
* `l` is referred to as the "left border" (l) or "offset" (o)
* `k` represents the length of sequence `t` (i.e. `k = #t`)

Alternatively, `t` can be defined using a "right-bound" notation:

* `infixRe(s,r,k) := t`
* `t = [ s[r-k+1], s[r-k+2], ..., s[r-1], s[r] ]`
* `r` is referred to as the "right border" (r)
* `k` represents the length of sequence `t` (i.e. `k = #t`)

Note that `infixLe(s,l,k)` and `infixRe(s,r,k)` define intervals with regards
to sequence `s` - i.e. `[l,(l+k-1)]` and `[(r-k+1),r]`.
