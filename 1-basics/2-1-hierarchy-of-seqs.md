
<!-- ======================================================================= -->
# Subsequences of elements

```
s = [ s(1), s(2), ..., s(o), s(o+1), ..., s(o+n), s(o+n-1), ..., s(N) ]
t = [                  t(1), t(2),   ..., t(n-1), t(n)                ]
```

* `(t subsequence-of s) := (t infix-of s)`
* `t infix-of s`, if `(s(o+j-1) = t(j))` for some offset `o in [1,N]`,
  `t`'s length `n in [1,(N-o+1)]` and all indices `j in [1,n]`
* in words: `t` is a subsequence of `s`, if `t` can be located within `s`
* `(t strict-subsequence-of s) := (t subsequence-of s) and (t != s)`

Note that there may be one or more offsets at which `t`'s pattern can be
found within `s`. That is, `t` may be embedded into `s` several times.

Note that `t` is said to be an infix of `s`, if `t` is a subsequence of `s`.

Note that `t`'s offset (o) within `s` may be `1`. In that case, both sequences
begin with the same element (i.e. `t` is said to be a prefix of `s`).

Note that `t`'s offset may be such that `t` and `s` both sequences end with
the same element (i.e. `t` is a suffix of `s`).

Note that, if `t` is a subsequence of `s`, then `s` may also be a subsequence of
`t` (if both sequences are identical). However, if `t` is a strict subsequence
of `s`, then `s` can not be a (strict) subsequence of `t` at the same time.

```
s = [ 0, 0, 1, 1, 1, 4, 3, 2, 6, 7 ]
t = [ 9, 8, 7, 6, 3, 2, 1, 0, 4, 5 ]
u = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```

* `s,t,u` all are sequences of elements/values
* `a = [3, 2]` is a subsequence of `s` and `t`
* `s,t` only share pattern `a = [3, 2]`
* `t,u` only share pattern `b = [4, 5]`
* `s,u` only share pattern `c = [6, 7]`
* all sequences are different from one another
* no sequence is a subsequence of another sequence

```
t = [ 9, 8, 7, 6, 3, 2, 1, 0, 4, 5 ]
u = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```

* sequences `t` and `u` contain no element more than once
* `t` and `u` can be understood to **represent sets of values**
* all of their values have an implicit order - e.g. `(2 < 3)`
* `t` and `u` can be understood to **represent ordered sets of values**
* that is regardless of where each value is located

```
u = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```

* the indices of each element within `u` corresponds with the order of elements
* that is, `(u[i] < u[j])` if `(i < j)`

Note that sequences which represent ordered sets of elements/values *and* in
which the positions of its elements correspond with the order of elements, are
most relevant to the whole discussion. Unfortunately, there does not seem to
exist a term that could be used to refer to this combination of characteristics.

```
a = [ 1 ]
b = [ 1, 2 ]
c = [ [1], 2 ]
d = [ 2, 3 ]
```

* Sequence `a` is a strict subsequence of `b`.
* Sequence `b` does not (strictly) contain `a` (as an element).
* Sequence `b` is not a subsequence of `c`, and `c` not a subsequence of `b`.

Similar to sets of elements/values, from a strict perspective `b` does not
contain `a` because `a` is not an element of `b`. However, `b` may still be
loosely said to contain `a`, if it is clear that the statement refers to the
`subsequence-of` relationship.

**CONCLUSION**
Sequence `a` is said to be **embedded** into `b`,
if `a` is a strict subsequence of `b`.

**CONCLUSION**
Sequence `d` is said to **overlap** `b`, if both share a common pattern and if
both sequences contain patterns that the other sequence does not have.

Note that neither of the two sequences is embedded into the other. Sequence `b`
therefore also overlaps `d`. Both sequences can therefore be said to overlap
each other.

In addition to that, and due to the order of the elements, `b` can be said to
reach into `d` and `d` to reach out of `b`.

<!-- ======================================================================= -->
## Equivalent visual definitions

```
s = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
t = [    1, 2, 3, 4, 5, 6          ]
u = [       2, 3,                  ]
v = [                5, 6          ]
w = [                         8, 9 ]
```

A visual representation that embeds all these definitions
into a single "image" is:

```
|s---------------------------------------------|
|    |t--------------------------|             |
|    |    |u------|    |v------| |    |w-----| |
| 0, | 1, | 2, 3, | 4, | 5, 6, | | 7, | 8, 9 | |
|    |    |-------|    |-------| |    |------| |
|    |---------------------------|             |
|----------------------------------------------|
```

An even more compact representation is:

```
0 1 2 3 4 5 6 7 8 9 - s
  ===========   === - t,w
    ===   ===       - u,v
```

<!-- ======================================================================= -->
## A consistent setup



<!-- ======================================================================= -->
## An inconsistent setup

```
0 1 2 3 4 5 6 7 8 9 - s
  =======   ===     - t
    ===========     - u
            =====   - v
```

Inconsistency 1

* Sequence `t` has a "gap", it does not contain `5`.
* Sequence `t` is not a subsequence of `s`.

Inconsistency 2

* Sequence `u` is not a subsequence of `v`.
* Sequence `u` contains `2 to 5`, but `v` does not.
* Sequence `v` is not a subsequence of `u`.
* Sequence `v` contains `8`, but `u` does not.

**CONCLUSION**
A setup is said to be inconsistent with the definition of the `subsequence-of`
operator, if the following is true: Two sequences exist that have one or more
elements in common, but none of those two is a subsequence of the other.

**Memory hook**
Sequences must be continuous (i.e. have no gaps) and must not overlap each other.
