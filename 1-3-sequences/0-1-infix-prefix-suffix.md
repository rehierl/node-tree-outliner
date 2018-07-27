
<!-- ======================================================================= -->
# Infix, Prefix, Suffix

Note that ...

* The following definitions will be referred to as "index-based".
* Any non-empty infix `t` may appear several times within the corresponding
  sequence `s`. That is, there may be more than one offset at which `t` can
  be located in `s`.
* The concatenation-based definitions still apply.

<!-- ======================================================================= -->
## infix/substring

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
