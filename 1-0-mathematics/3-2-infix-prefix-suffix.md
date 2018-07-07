
<!-- ======================================================================= -->
# Infix, Prefix, Suffix

```
//- default notation
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

Given a sequence `t` that was derived from sequence `s` by removing a prefix
and/or suffix from `s`, then `t` can be defined by using the above left-bound
notation: `infixL(s,l,k)`.

```
//- right-bound notation
t = [ s[r-k+1], s[r-k+2], ..., s[r-1], s[r] ]
```

* `r` is referred to as the "right border" (r)
* `k` represents the length of sequence `t` (i.e. `k = #t`)

Given a sequence `t` that was derived from sequence `s` by removing a prefix
and/or suffix from `s`, then `t` can be defined by using the above right-bound
notation: `infixR(s,r,k)`.

<!-- ======================================================================= -->
## infix

```
s = [ s[1], s[2], ..., s[o], s[o+1], ..., s[o+n], s[o+n-1], ..., s[N] ]
t = [                  t[1], t[2],   ..., t[n-1], t[n]                ]
t = [                  s[o], s[o+1], ..., s[o+n], s[o+n-1]            ]
```

sequence `t` is **an infix of** sequence `s`

* `(t infix-of s)`, if `(s[o+j-1] = t[j])`
  for `o in [1,N]`, `n in [1,(N-o+1)]` and all `j in [1,n]`
* `(t infix-of s) -> (#t <= #s)`

Note that multiple offsets may exist at which sequence `t` begins in `s`. That
is, `infix-of` merely states that `t` can be located at least once within `s`.

<!-- ======================================================================= -->
## prefix

sequence `t` is **a prefix of** sequence `s`

* `(t prefix-of s)`, if `(t infix-of s)` and offset `(o = 1)`
* `t` is bound to the 1st entry of `s`

sequence `t` is **a strict prefix of** sequence `s`

* `(t strict-prefix-of s)`, if `(t prefix-of s)` and `(t != s)`
* `(t strict-prefix-of s) -> (#t < #s)`

sequence `t` is **an n-prefix of** sequence `s`

* `(t n-prefix-of s)`, if `(t prefix-of s)` and `(#t == n)`
* `(prefix(s,n) == t)`, if `(t n-prefix-of s)`
* the N-prefix of a sequence is the sequence itself

sequence `u` is **a common prefix of** sequence `s` and sequence `t`

* `(u prefix-of s,t)`, if `(u prefix-of s)` and `(u prefix-of t)`
* `s` and `t` share the common prefix `u`, if `#u in [1,min(#s,#t)]`
* for any common prefix `u`, there is a `n` such that `(u n-prefix-of s,t)`

sequence `u` is **a common n-prefix of** sequences `s` and `t`

* `(u n-prefix-of s,t)`, if `(u prefix-of s,t)` and `(#u = n)`
* `n in [1,min(#s,#t)]`

Note that, if two sequences have a common prefix of length `(n > 1)`,
then both sequences have more than one prefix in common.

sequence `u` is **the common prefix of** sequence `s` and sequence `t`

* `(u max-prefix-of s,t)`, is true if ...
* `u` is the longest common n-prefix possible
* that is, there is no other common prefix `v` such that `(#v > #u)`

<!-- ======================================================================= -->
## suffix/postfix

sequence `t` is **a suffix of** sequence `s`

* `(t suffix-of s)`, if `(t subsequence-of s)` and `(r == N)`
* `t` is bound to the last entry of `s`

sequence `t` is **a strict suffix of** sequence `s`

* `(t strict-suffix-of s)`, if `(t suffix-of s)` and `(t != s)`
* `(t strict-suffix-of s) -> (#t < #s)`

sequence `t` is **an n-suffix of** sequence `s`

* `(t n-suffix-of s)`, if `(t suffix-of s)` and `(#t == n)`
* `(suffix(s,n) == t)`, if `(t n-suffix-of s)`
* the N-th suffix of a sequence is the sequence itself

sequence `u` is **a common suffix of** sequence `s` and sequence `t`

* `(u suffix-of s,t)`, if `(u suffix-of s)` and `(u suffix-of t)`
* `s` and `t` share the common suffix `u`, if `#u in [1,min(#s,#t)]`
* for any common suffix `u`, there is a `n` such that `(u n-suffix-of s,t)`

sequence `u` is **a common n-suffix of** sequences `s` and `t`

* `(u n-suffix-of s,t)`, if `(u suffix-of s,t)` and `(#u = n)`
* `n in [1,min(#s,#t)]`

Note that, if two sequences have a common suffix of length `(n > 1)`,
then both sequences have more than one suffix in common.

sequence `u` is **the common suffix of** sequence `s` and sequence `t`

* `(u max-suffix-of s,t)`, is true if ...
* `u` is the longest common suffix possible
* that is, there is no other common suffix `v` such that `(#v > #u)`

<!-- ======================================================================= -->
## distinct notes

Note that infix/prefix/suffix `t` represents a distinct/exact pattern
in the corresponding sequence `s`.

Note that any non-empty infix/prefix/suffix `t` may appear several times
within the corresponding sequence `s`. That is, there may be more than one
offset at which `t` can be located in `s`.

Note that any non-empty sequence is an infix/prefix/suffix to itself.
