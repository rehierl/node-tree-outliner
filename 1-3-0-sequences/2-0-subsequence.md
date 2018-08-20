
<!-- ======================================================================= -->
# Subsequence

Note that this discussion builds upon the following definition of the
`subsequence-of` operator. Hence, the characteristics of this operator
are similar to the set-based `subset-of` operator.

* `(t subsequence-of s)` := sequences `u,v` exist such that `s = (u × t × v)`
* The empty sequence `[]` is a subsequence to any sequence.
* Any sequence, including `[]`, is a subsequence to itself.

<!-- ======================================================================= -->
## (f: N* -> N*)

Given a sequence `(s in N*)` of arbitrarily many elements, the notation is by
default from left-to-right, i.e. from the first (`s[1]`) to the last element
(`s[k]`):

* `s := [ e1, e2, ..., ek ]`
* `s := [ s[1], ..., s[k] ]`
* `s := [ s1, s2, ..., sk ]`

The `get` access property of sequence `s` can be used to create a clone `t`:

* `t := [ si ]` for `(i in [1,k])`
* `t := [ s1, s2, ..., sk ]`
* `t := [ s[1], ..., s[k] ]`

The created sequence `t` however does not have to be equal to `s`. Any number
of elements in `s` may be omitted. That is, the multiplicity of elements taken
form `s` may be zero/0 in `t`:

* `t := [ s2, s3, s5, s6 ]`

In addition to that, the elements taken from `s` may be rearranged in `t`:

* `t := [ s3, s6, s2, s1 ]`

Finally, new sequences can be created by taking elements from `s` and adding
them repeatedly to the sequences being created:

* `t := [ s2, s5, s2, s5 ]`

Note that the general definition of the term "subsequence" does not allow
for elements to be rearranged (i.e. reordering), or for elements to be added
repeatedly (i.e. increased multiplicity).

Note that the new sequence `t` will be in relationship with the source sequence
`s`. That is, similar to the `subset-of` relationship, `t` contains one or more
elements of `s`. However, in addition to holding elements from `s`, the created
sequence needs to maintain the element order.
