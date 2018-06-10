
<!-- ======================================================================= -->
# Subsequences of elements

```
s = [ s(1), s(2), ..., s(o), s(o+1), ..., s(o+n), s(o+n-1), ..., s(N) ]
t = [                  t(1), t(2),   ..., t(n-1), t(n)                ]
```

* `t infix-of s`, if `(s(o+j-1) = t(j))`
  for `o in [1,N]`, `n in [1,(N-o+1)]` and `j in [1,n]`
* `(t subsequence-of s) := (t infix-of s)`

In simple words: `t` is a subsequence of sequence `s`,
if `t`'s pattern can be located within `s`.
