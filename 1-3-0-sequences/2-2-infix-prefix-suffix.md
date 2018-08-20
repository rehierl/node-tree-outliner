
<!-- ======================================================================= -->
# Infix, Prefix, Suffix

* `(t subsequence-of s) := (t infix-of s)`
* `(t substring-of s) := (t infix-of s)`
* `(t postfix-of s) := (t suffix-of s)`

<!-- ======================================================================= -->
## left/right-bound notation

* `s = [ s1, s2, ..., sN ]`

In general, a new sequence `t` can be created from an existing sequence `s`
by removing a prefix and/or a suffix from `s`. Sequence `t` can therefore be
defined using a **left-bound notation** (aka. an **offset-based notation**):

* `infixLe(s,l,k) := t`
* `t = [ s[l], s[l+1], ..., s[l+k-2], s[l+k-1] ]`
* `t = [ s[o], s[o+1], ..., s[o+k-2], s[o+k-1] ]`
* `l` is referred to as the "left border" (l) or "offset" (o)
* `k` represents the length of sequence `t` (i.e. `k = #t`)

Alternatively, `t` can be defined using a **right-bound notation**:

* `infixRi(s,r,k) := t`
* `t = [ s[r-k+1], s[r-k+2], ..., s[r-1], s[r] ]`
* `r` is referred to as the "right border" (r)
* `k` represents the length of sequence `t` (i.e. `k = #t`)

Note that both notations can be understood to define intervals with regards
to the index set of sequence `s` - i.e. `[l,(l+k-1)]` and `[(r-k+1),r]`.

<!-- ======================================================================= -->
## index-based definitions

The following definitions are based on the get-operator of a known source
sequence. They may therefore be referred to as the **index-based definitions**.

```
s = [ s[1], s[2], ..., s[o], s[o+1], ..., s[o+n], s[o+n-1], ..., s[N] ]
t = [                  s[o], s[o+1], ..., s[o+n], s[o+n-1]            ]
t = [                  t[1], t[2],   ..., t[n-1], t[n]                ]
```

Sequence `t` is said to be **an infix of** sequence `s`

* `(t infix-of s)`, if `(s[o+j-1] = t[j])`
  for `o in [1,N]`, `n in [1,(N-o+1)]` and all `j in [1,n]`

Sequence `t` is **a prefix of** sequence `s`

* `(t prefix-of s)`, if `(t infix-of s)` and offset `(o = 1)`
* `t` is bound to the 1st entry of `s`

Sequence `t` is **a suffix of** sequence `s`

* `(t suffix-of s)`, if `(t infix-of s)` and `(r == N)`
* `t` is bound to the last entry of `s`

Note that ...

* `(t == s) -> (#t == #s)`
* `(t infix-of s) -> (#t <= #s)`
* Any prefix/suffix is also an infix.
* Any infix `t` represents a distinct/exact pattern in `s`.
* More than one offset may exist at which infix `t` can be located in `s`.
* The empty sequence `[]` is not an infix of any sequence.
* Any non-empty sequence is an infix to itself.

<!-- ======================================================================= -->
## concatenation-based definitions

The following definitions are based on the concatenation-operator for sequences.
They may therefore be referred to as the **concatenation-based definitions**.

* (×) is the concatenation operator for sequences
* `(a × b × c) := [ a1,..,ai,b1,..,bj,c1,..,ck ]`

Sequence `t` is said to be **an infix of** sequence `s`

* `(t infix-of s)`, if sequences `a` and `b` exist
  such that `s = (a × t × b)`.

Sequence `t` is said to be **a prefix of** sequence `s`

* `(t prefix-of s)`, if a sequence `u` exists
  such that `s = ([] × t × u)`

Sequence `t` is said to be **a suffix of** sequence `s`

* `(t suffix-of s)`, if sequence `u` exists
  such that `s = (u × t × [])`

Note that ...

* `(t == s) -> (#t == #s)`
* `(t infix-of s) -> (#t <= #s)`
* Any prefix/suffix is also an infix.
* Any infix `t` represents a distinct/exact pattern in `s`.
* Several sequences `u` and `v` may exist such that `s = (u × t × v)`.
* The empty sequence `[]` is an infix of any sequence.
* Any sequence, including `[]`, is an infix to itself.

<!-- ======================================================================= -->
## derived statements

Neither the index-based, nor the concatenation-based definitions require an
infix to be "unique". That is, any infix `t` may appear several times within
its super-sequence `s`. Because of that, several indexes may exist at which
`t` can be located in `s`. Put differently, `(s == (u × t × v))` may hold
for several distinct sequences `u` and `v`.

Note that the number of distinct offsets of infix `t` in `s` may in general
be referred to as the **multiplicity** of `t` in `s`. Generalized, the
multiplicity of an infix is equal to the number of distinct prefixes `u`
such that `(s == (u × t × v))`. Because of that, the multiplicity of the
empty sequence `[]` always is `(1 + #s)`.

* `#(t,s)` := the multiplicity of `t` in `s`
* `#([],s) := (1 + #s)`

However,  the exact value of `#(t,s)` is not relevant to `infix-of`. Because
of that the above definitions may be reduced to:

* `(t infix-of s) := 1` iff `(t == [])`
* `(t infix-of s) := (#(t,s) != 0)`

The index-based definitions obviously require non-empty sequences. Because
of that, the empty sequence `[]` can not be understood to be an infix of any
sequence. These definitions are therefore in contrast to `subset-of`.

In contrary to that, the concatenation-based definitions don't exclude empty
sequences. Because of that, the empty sequence `[]` is understood to be an
infix of any sequence. As such, these definitions are consistent with the
set-based `subset-of` operators.

Note that this discussion therefore builds upon the concatenation-based view
on the `infix-of` operator.

<!-- ======================================================================= -->
## extended definitions

### (t infix-of s)

Sequence `t` is **a strict infix of** sequence `s`

* `(t strict-infix-of s)`, if `(t infix-of s)` and `(t != s)`
* `(t strict-infix-of s) -> (#t < #s)`

Sequence `t` is **an n-infix of** sequence `s`

* `(t n-infix-of s)`, if `(t infix-of s)` and `(#t == n)`
* `(infix(s,n) == t)`, if `(t n-infix-of s)`
* the N-prefix of a sequence is the sequence itself

Sequence `u` is **a common infix of** sequence `s` and `t`

* `(u infix-of s,t)`, if `(u infix-of s)` and `(u infix-of t)`
* `s` and `t` share the common infix `u`, if `#u in [1,min(#s,#t)]`
* for any common infix `u`, there is a `n` such that `(u n-infix-of s,t)`

Sequence `u` is **a common n-infix of** sequences `s` and `t`

* `(u n-infix-of s,t)`, if `(u infix-of s,t)` and `(#u = n)`
* `n in [1,min(#s,#t)]`

Sequence `u` is **the common infix of** sequence `s` and `t`

* `(u max-infix-of s,t)`, is true if ...
* there is no other common infix `v` of `s` and `t` such that `(#v > #u)`

Sequence `t` is **an infix of** set of sequences `S`

* `(t infix-of S)`, if `(t infix-of s)` for all `(s in S)`
* i.e. all sequences `(s in S)` have `t` as an infix
* i.e. `t` is a common infix to all sequences `(s in S)`

Set of sequences `T` is **an infix of** set of sequences `S`

* `(T infix-of S)`, if `(t infix-of s)` for all `(s in S)` and all `(t in T)`
* i.e. `(t infix-of S)` for all `(t in T)`

### (t prefix-of s)

Similar extensions for ...

* `(t strict-prefix-of s)`
* `(t n-prefix-of s)`
* `(u prefix-of s,t)`
* `(u n-prefix-of s,t)`
* `(u max-prefix-of s,t)`
* `(t prefix-of S)`

### (t suffix-of s)

Similar extensions for ...

* `(t strict-suffix-of s)`
* `(t n-suffix-of s)`
* `(u suffix-of s,t)`
* `(u n-suffix-of s,t)`
* `(u max-suffix-of s,t)`
* `(t suffix-of S)`
