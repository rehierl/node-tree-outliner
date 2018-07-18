
<!-- ======================================================================= -->
# Subsequence

```
s = [ a, b, c, d, e, f, g, h, i, ... ]
t = [          d, e, f,    h         ]
u = [          d, e, f, g            ]
```

* `u` is a substring of `s`
* `u` is said to be **consecutive** with regards to `s`
* `t` is not a substring of `s`
* `t` is said to **have gaps** with regards to `s`

clarification

* an infix/prefix/suffix is a substring
* a super-string (`s`) is said to contain its substrings (`u`)
* a substring is a sequence of contiguous/consecutive elements

Note that the definition of "subsequence" in the context of this discussion
deviates from the mathematical definition in such a way that a subsequence
represents an exact pattern that can be located within another sequence (i.e.
contiguous/ consecutive/ has no gaps). In general, the definition used here
is more strict and needs to be understood to be similar to the definition of
"substring" or "infix".

Note that the definition of "subsequence" is similar to, but more complex than
the definition of "subset". The additional complexity is a result of the element
order, which does not have to be taken into account in the context of sets of
elements.

<!-- ======================================================================= -->
## subsequence

In mathematics, sequence `t` is a subsequence of sequence `s`, if `t` was
derived from `s` by the removal of elements. That is, without changing the
order of these elements.

Based on that definition, it can be stated that the empty sequence `[]` is a
subsequence to any sequence. That is, even though the empty sequence has no
clear offset within the initial sequence. And because `[]` has no effect on
the result of a concatenation, `[]` can be said to be an infix, prefix and
suffix to any non-empty sequence.

```
s = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
t = [          3,    5, 6,         ]
u = [          3, 4, 5, 6,         ]
```

* `t` and `u` are both (mathematical) subsequences of `s`
* that is, even though `t` "has gaps"

With regards to `s`, the elements in `u` can be said to be consecutive,
contiguous, and/or strictly subsequent. In contrary to that, the elements
in `t` are said to be loosely subsequent.

**CLARIFICATION**
In the context of this discussion, a sequence `t` is said to be a subsequence
of sequence `s`, if `t` can be created from `s` by removing elements, and if
`t` is a sequence of consecutive elements.

* `s := (t x u x v) = [a, b, c, d, e]`
* `u := [c, d]`

Put differently, subsequence `t` is created from sequence `s` by removing a
prefix and/or suffix from `u`. And if this view is turned upside-down, then
it can even be stated that the super-sequence `s` can be created from its
sub-sequence `u` by adding a prefix and/or suffix to `u`.

Note that the mathematical definition may be referred to as the "removal-based"
definition and the above definition as the "concatenation-based" definition.

Note that, in case of repetitions, it is possible to create the exact same
subsequence by removing different elements:

* `(s x t x u) := [a, b, c, b, e]`
* if subsequence `t` is assumed to be `[b]`, then
* `s` may be `[a]` or `[a,b,c]`

In cases where explicit clarity is needed, such a sequence may be referred
to as a "consecutive subsequence" or as a "subsequence of strictly subsequent
elements".

Note the following similarities with the set-based `subset-of` definition.

<!-- ======================================================================= -->
## subsequence-of

* `(s subsequence-of t)` := "s is a consecutive subsequence of t"

Note that, if `(s subsequence-of t)` is true,
then `s` may be referred to as "the subsequence"
and `t` as "the super-sequence".

Note that sequences have no operators like the ones defined for sets of
elements (e.g. union, intersection, etc).

clarification

* The empty sequence `[]` is a subsequence to any sequence.
* Any sequence, including `[]`, is a subsequence to itself.

clarification

* `(s subsequence-of t) -> (#s <= #t)`
* `subsequence-of` implies an order (<=)

<!-- ======================================================================= -->
## strict-subsequence-of

* `(i strict-subsequence-of t) := (i subsequence-of t) and (i != t)`
* some non-empty prefix `p` and/or suffix `s` exists such that `t = (p x i x s)`
* synonymous - proper-subsequence-of, true-subsequence-of

Note that, if `(s strict-subsequence-of t)` is true,
then `s` may be referred to as "the (strict) subsequence"
and `t` as "the (strict) super-sequence".

clarification

* The empty sequence `[]` is a strict subsequence to any non-empty sequence.
* No sequence, including `[]`, is a strict subsequence to itself.

clarification

* `(s strict-subsequence-of t) -> (#s < #t)`
* `strict-subsequence-of` implies an order (<)
