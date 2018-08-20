
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

* `s` is a super-sequence to sub-sequences `t` and `u`
* super-string `s` is said to contain the sub-string `u`
* a substring is a sequence of contiguous/consecutive elements

Note that the definition of "subsequence" in the context of this discussion
deviates from the generalized mathematical definition in such a way that a
subsequence represents an exact pattern which can be located within another
sequence (i.e. contiguous/consecutive/no gaps). In general, the definition
used here is more strict and needs to be understood to be similar to the
definition of "substring" or "infix".

Note that the definition of "subsequence" is similar to, but more complex
than the definition of "subset". The additional complexity is a result of
the element order, which does not have to be taken into account in the
context of sets of elements.

<!-- ======================================================================= -->
## subsequence

In mathematics, sequence `t` is a subsequence of the source sequence `s`, if
`t` was derived from `s` by the removal of elements. That is, without changing
the order of the remaining elements.

Based on this definition, it can be stated that the empty sequence `[]` is a
subsequence to any sequence. That is, even though the empty sequence has no
distinct offset within the source sequence.

```
s = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
t = [          3,    5, 6,         ]
u = [          3, 4, 5, 6,         ]
```

Despite of `t` having gaps, sequences `t` and `u` are both (mathematical)
subsequences of `s`. Furthermore, and with regards to `s`, the elements in
`u` are said to be consecutive, contiguous and/or strictly subsequent. In
contrast to that, the elements in `t` are said to be loosely subsequent.

**CLARIFICATION**
In the context of this discussion, a sequence `t` is referred to as
a **subsequence** of sequence `s`, if `t` can be created from `s` by
removing elements, and if `t` is a sequence of consecutive elements.

* `s := (u x t x v) = [a, b, c, d, e]`
* e.g. `u := [a, b]`, `t := [c, d]`, `v := [e]`

Put differently, subsequence `t` is created from sequence `s` by removing a
prefix and/or suffix from `u`. If this view is turned upside-down, then it can
be stated that the super-sequence `s` can be created from its sub-sequence `u`
by adding a prefix and/or suffix to `u`.

Note that the mathematical definition may be referred to as
the **removal-based definition**, and the afore mentioned
one as the more specific **concatenation-based definition**.

Note that, in case of repetitions, it is possible to create the exact
same subsequence by removing different prefixes and/or suffixes:

* `s := (u x t x v) := [a, x, c, x, e]`
* if subsequence `t` is assumed to be `t:=[x]`, then
* prefix `u` may be `u:=[a]` or `u:=[a, x, c]`

In cases where explicit clarity is needed, such a sequence may be referred to
as a **consecutive/contiguous subsequence**, or as a **subsequence of strictly
subsequent elements**.

<!-- ======================================================================= -->
## subsequence-of

* `(t subsequence-of s)` := "t is a consecutive subsequence of s"
* i.e. some prefix `u` and/or suffix `v` exists such that `s = (u x t x v)`

Note that, if `(t subsequence-of s)` is true,
then `t` may be referred to as "the sub-sequence"
and `s` as "the super-sequence".

clarification

* `(t subsequence-of s) -> (#t <= #s)`
* `(t subsequence-of s)` implies an order (<=)
* i.e. `s` is super-ordinate to `t`

clarification

* The empty sequence `[]` is a subsequence to any sequence.
* Any sequence, including `[]`, is a subsequence to itself.

<!-- ======================================================================= -->
## strict-subsequence-of

* `(t strict-subsequence-of s) := (t subsequence-of s) and (t != s)`
* some non-empty prefix `u` and/or suffix `v` exists such that `s = (u x t x v)`
* synonymous - proper-subsequence-of, true-subsequence-of

Note that, if `(t strict-subsequence-of s)` is true,
then `t` may be referred to as "the (strict) sub-sequence"
and `s` as "the (strict) super-sequence".

clarification

* `(t strict-subsequence-of s) -> (#t < #s)`
* `(t strict-subsequence-of s)` implies an order (<)
* i.e. `s` is super-ordinate to `t`

clarification

* The empty sequence `[]` is a strict subsequence to any non-empty sequence.
* No sequence, including `[]`, is a strict subsequence to itself.

<!-- ======================================================================= -->
## general notes

Note that the above definitions are similar to the "subset-of" definitions.

Note that it is not relevant whether or not subsequence `t` appears several
times in super-sequence `s` (i.e. multiple offsets). The "subsequence" operator
only allows to determine if `t` appears in `s` at some position, or not at all.

Note that sequences have in general no set-like operators (e.g. union of sets).
