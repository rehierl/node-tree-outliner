
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

Note that `t`'s offset (o) within `s` may be `1`. That is, `s` begins with `t`'s
pattern (i.e. `o = 1`). Likewise, `t`'s offset may even be such that `t` and `s`
both end with the same element.

Note that there may be one or more offsets at which `t`'s pattern can be found.
That is, `s` may contain `t`'s pattern several times.

```
s = [ 0, 0, 1, 1, 1, 4, 3, 2, 6, 7 ]
t = [ 9, 8, 7, 6, 3, 2, 1, 0, 4, 5 ]
u = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```

1 - observations

* `s,t,u` all are sequences of elements/values
* `a = [3, 2]` is a subsequence of `s` and `t`
* `s,t` only share the pattern `a = [3, 2]`
* `t,u` only share the pattern `b = [4, 5]`
* `s,u` only share the pattern `c = [6, 7]`
* no sequence is a subsequence of another sequence

2 - observations

* only `t` and `u` can be understood to **represent sets of values**
* sequences `t` and `u` contain no element more than once
* `t` and `u` can also be understood to **represent ordered sets of values**
* all of their values have an implicit order - i.e. `(4 < 5)`
* regardless of where each value is located within a sequence

3 - observations

* each element index within `u` corresponds with the order of elements
* that is, `(u[i] < u[j])` if `(i < j)`

Note that sequences, which represent ordered sets of elements/values *and* in
which the positions of its elements correspond with the element order, are most
relevant with regards to the whole discussion. Unfortunately, there does not
seem to exist a term dedicated to these particular sequences of elements.

```
s = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
t = [    1, 2, 3, 4, 5, 6          ]
u = [       2, 3,                  ]
v = [                5, 6          ]
w = [                         8, 9 ]
```

A visual representation that embeds all sequence definitions into one is:

```
|s---------------------------------------------|
|    |t--------------------------|             |
|    |    |u------|    |v------| |    |w-----| |
| 0, | 1, | 2, 3, | 4, | 5, 6, | | 7, | 8, 9 | |
|    |    |-------|    |-------| |    |------| |
|    |---------------------------|             |
|----------------------------------------------|
```

An even more compact method to visualize these definitions is:

```
0 1 2 3 4 5 6 7 8 9 - s
  ===========   === - t,w
    ===   ===       - u,v
```

<!-- ======================================================================= -->
## A consistent setup

