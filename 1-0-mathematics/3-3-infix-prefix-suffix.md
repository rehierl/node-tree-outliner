
<!-- ======================================================================= -->
# Infix, Prefix, Suffix

<!-- ======================================================================= -->
## infix/subsequence

```
s = [ s[1], s[2], ..., s[o], s[o+1], ..., s[o+n], s[o+n-1], ..., s[N] ]
t = [                  t[1], t[2],   ..., t[n-1], t[n]                ]
```

Note that this definition of "subsequence" deviates from the mathematical
definition in such a way that a subsequence must represent an exact pattern
within the other sequence (i.e. no gaps). As such this definition is more
strict and needs to be understood with the notion of "substring".

sequence `t` is **an infix/subsequence of** sequence `s`

* `t infix-of s`, if `(s[o+j-1] = t[j])`
  for `o in [1,N]`, `n in [1,(N-o+1)]` and all `j in [1,n]`
* `(t subsequence-of s) := (t infix-of s)`
* signature - (sequence,sequence) -> boolean

sequence `t` is **a strict infix/subsequence of** sequence `s`

* `t strict-infix-of s`, if `(t infix-of s)` and `(t != s)`
* `(t strict-subsequence-of s) := (t strict-infix-of s)`

element-of vs. subsequence-of

* `s = [1, [2, 3], 4]`, `t = [2, 3]`
* `t` is an element of `s = [1, t, 4]`
* that is, an element in `s` has `t` as its value
* `s = [1, 2, 3, 4]`, `t = [2, 3]`
* `t` is an infix/subsequence of `s`

clarification

* a sequence is a subsequence, but not a strict subsequence to itself
* `(t == s)` => `(t infix-of s)` and `(#t == #s)`
* `(s == s)` and `(s infix-of s)` are both always true

**TODO** -
clarification

* the empty sequence has no subsequence (`s[i]` is undefined)
* the empty sequence is no subsequence to any sequence

<!-- ======================================================================= -->
## prefix

sequence `t` is **a prefix of** sequence `s`

* `t prefix-of s`, if `t infix-of s` and offset `(o = 1)`
* `t` is bound to the 1st entry of `s`
* `s prefix-of s` is always true
* a sequence is a prefix to itself

sequence `t` is **a strict prefix of** sequence `s`

* `t strict-prefix-of s`, if `(t prefix-of s)` and `(t != s)`

sequence `t` is **the n-th prefix of** sequence `s`

* `t n-prefix-of s`, if `t prefix-of s` and `(#t == n)`
* `(prefix(s,n) == t)`, if `(t n-prefix-of s)`
* the N-th prefix of a sequence is the sequence itself

sequence `u` is **a common prefix of** sequence `s` and sequence `t`

* `u prefix-of s,t`, if `(u prefix-of s)` and `(u prefix-of t)`
* `s` and `t` share the common prefix `u`
* `#u in [1,min(#s,#t)]`
* for any common prefix `u`, there is a `n` such that `u n-prefix-of s,t`

sequence `u` is **the n-th common prefix of** sequences `s` and `t`

* `u n-prefix-of s,t`, if `(u prefix-of s,t)` and `(#u = n)`
* `n in [1,min(#s,#t)]`

sequence `u` is **the common prefix of** sequence `s` and sequence `t`

* `u max-prefix-of s,t`, is true if ...
* `u` is the longest common prefix possible
* if there is no other common prefix `v` such that `(#v > #u)`

<!-- ======================================================================= -->
## suffix

sequence `t` is **a suffix of** sequence `s`

* `t suffix-of s`, if `t subsequence-of s` and `(r == N)`
* `t` is bound to the last entry of `s`
* `t` and `s` have the same order (i.e. `t` is not reversed)
* `s suffix-of s` is always true
* any sequence is a suffix to itself

sequence `t` is **a strict suffix of** sequence `s`

* `t strict-suffix-of s`, if `(t suffix-of s)` and `(t != s)`

sequence `t` is **the n-th suffix of** sequence `s`

* `t n-suffix-of s`, if `t suffix-of s` and `(#t == n)`
* `(suffix(s,n) == t)`, if `(t n-suffix-of s)`
* the N-th suffix of a sequence is the sequence itself

sequence `u` is **a common suffix of** sequence `s` and sequence `t`

* `u suffix-of s,t`, if `(u suffix-of s)` and `(u suffix-of t)`
* `s` and `t` share the common suffix `u`
* `#u in [1,min(#s,#t)]`
* for any common suffix `u`, there is a `n` such that `u n-suffix-of s,t`

sequence `u` is **the n-th common suffix of** sequences `s` and `t`

* `u n-suffix-of s,t`, if `(u suffix-of s,t)` and `(#u = n)`
* `n in [1,min(#s,#t)]`

sequence `u` is **the common suffix of** sequence `s` and sequence `t`

* `u max-suffix-of s,t`, is true if ...
* `u` is the longest common suffix possible
* if there is no other common suffix `v` such that `(#v > #u)`
