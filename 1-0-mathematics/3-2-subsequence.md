
<!-- ======================================================================= -->
# Subsequence

<!-- ======================================================================= -->
## left-bound, right-bound

```
t = [ t[1],     t[2],     ..., t[N-1],   t[N] ]     // default notation
t = [ t[l],     t[l+1],   ..., t[l+k-2], t[l+k-1] ] // left-bound notation
t = [ t[r-k+1], t[r-k+2], ..., t[r-1],   t[r] ]     // right-bound notation
```

* (left-bound, offset-based notation)
  `t = [t[l],t[l+1],...,t[l+k-1]]`
  for `l = 1` and `k in [1,(N-1)]` -
  `l` is the (l)eft border,  (o)ffset `o = l`.
* (right-bound notation)
  `t = [t[r-k+1],...,t[r-1],t[r]]`
  for some `r = N` and `k in [1,N]` -
  `r` is the (r)ight border.

<!-- ======================================================================= -->
## subsequence

```
s = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
t = [ 0,       3,    5, 6,       9 ]
```

* sequence `t` is a subsequence of sequence `s`,
  because it was derived from `s`
  by removing one or more values,
  without changing the order of these values.
* based on that definition, `[]` is a subsequence to any sequence
