
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

Note that `t`'s offset (o) within `s` may be `1`. In that case, both sequences
begin with the same element (i.e. `t` is a prefix of `s`). Likewise, `t`'s
offset may be such that `t` and `s` both end with the same element (i.e. `t`
is a suffix of `s`).

Note that, if `t` is a subsequence of `s`, then `s` may also be a subsequence of
`t` (i.e. both are identical). However, if `t` is a strict subsequence of `s`,
then `s` can not also be a (strict) subsequence of `t`.

```
s = [ 0, 0, 1, 1, 1, 4, 3, 2, 6, 7 ]
t = [ 9, 8, 7, 6, 3, 2, 1, 0, 4, 5 ]
u = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```

* `s,t,u` all are sequences of elements/values
* `a = [3, 2]` is a subsequence of `s` and `t`
* `s,t` only share the pattern `a = [3, 2]`
* `t,u` only share the pattern `b = [4, 5]`
* `s,u` only share the pattern `c = [6, 7]`
* all sequences are different from one another
* no sequence is a subsequence of another sequence

```
t = [ 9, 8, 7, 6, 3, 2, 1, 0, 4, 5 ]
u = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```

* sequences `t` and `u` contain no element more than once
* `t` and `u` can be said to represent **sets of values**
* all of their values have an implicit order - e.g. `(2 < 3)`
* `t` and `u` can be said to represent **ordered sets of values**
* that is regardless of where each value is located within a sequence

```
u = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```

* the indices of each element within `u` corresponds with the order of elements
* that is, if `(i < j)`, then also `(u[i] < u[j])`

Note that sequences which represent ordered sets of elements/values *and* in
which the positions of its elements correspond with the order of elements, are
integral to the whole discussion. Unfortunately, there does not seem to exist
a term that could be used to refer to this combination of characteristics.

```
a = [ 1 ]
b = [ 1, 2 ]
c = [ [1], 2 ]
d = [ 2, 3 ]
e = [ 2, 4 ]
```

* Sequence `a` is a strict subsequence of `b`.
* Sequence `b` does not contain `a`, but sequence `c` does.
* Sequence `b` is not a subsequence of `c`, and `c` not a subsequence of `b`.

Similar to sets of elements/values, from a strict perspective `b` does not
contain `a` because `a` is not an element of `b`. However, `b` may still be
loosely said to contain `a`, if it is clear that the statement refers to the
`subsequence-of` relationship.

**CLARIFICATION**
Two sequences are said to be **independent** from one another,
if both have no pattern in common.

Note that this includes not having even one element in common. That is, because
an element can be understood to represent a pattern of length `1`.

**CLARIFICATION**
Sequence `a` is said to be **embedded** into `b`.

Which is because `a` is a strict subsequence of `b`.

**CLARIFICATION**
Sequence `d` is said to **overlap** `b`.

Which is because both share a common pattern, and because both have one or more
patterns that the other sequence does not have.

Note that neither of the two sequences is embedded into the other. Sequence `b`
therefore also overlaps `d`, which is why both sequences can be said to overlap
each other.

In addition to that, and due to the order of the elements,
`b` is said to reach into `d`, and `d` to reach out of `b`.

Also note that `b` ends with a prefix of `d`, and `d` begins with a suffix of
`b`. That is, a suffix of one sequence is a prefix of the other.

**CLARIFICATION**
Sequence `d` is said to be **continuous** with regards to `u` as it is a
subsequence of `u`. In contrary to that, `e` is said to have a **gap** with
regards to `u` as it does not contain `3`. As such, `e` is no subsequence
of `u`. That is, in order to be continuous, a sequence must contain all
available elements within a given **range**.

<!-- ======================================================================= -->
## Visual representations

```
s = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
t = [    1, 2, 3, 4, 5, 6          ]
u = [       2, 3,                  ]
v = [                5, 6, 7       ]
w = [                         8, 9 ]
```

A visual representation that embeds all these declarations
into a single "image" is:

```
|s---------------------------------------------|
|    |t------------------------|               |
|    |    |u------|    |v-----------| |w-----| |
| 0, | 1, | 2, 3, | 4, | 5, 6, | 7, | | 8, 9 | |
|    |    |-------|    |------------| |------| |
|    |-------------------------|               |
|----------------------------------------------|
```

Note that the borders of sequences `t` and `v` cross each other.
That is, both sequences overlap each other.

An even more compact representation is:

```
0 1 2 3 4 5 6 7 8 9 - s
  ===========   === - t,w
    ===   =====     - u,v
```

Note that the left-to-right order of identifiers corresponds with the order
of sequence definitions: The range of sequence `t` begins with `1` and ends
with `6`.

Note that the last visual representation only allows to accurately represent
non-empty sequences.

<!-- ======================================================================= -->
## A consistent setup

```
0 1 2 3 4 5 6 7 8 9 - s
  ===========   === - t,w
    ===   ===       - u,v
```

* Sequence `s` contains all elements from `0` to `9`.
* Sequence `t` contains all elements from `1` to `6`.
* Sequence `w` contains the elements `8` and `9`.
* Sequence `u` contains the elements `2` and `3`.
* Sequence `v` contains the elements `5` and `6`.

Elements may belong to more than one sequence:

* Elements `1` and `4` belong to `s` and `t`.
* Elements `8` and `9` belong to `s` and `w`.
* Elements `2` and `3` belong to `s`, `t` and `u`.
* Elements `5` and `6` belong to `s`, `t` and `v`.

Some of the relationships between those sequences are:

* `t` and `w` both are subsequences of `s`.
* `u` and `v` both are subsequences of `s` and `t`.
* `u` is independent of `v` and `w`.

**CLARIFICATION**
A setup (i.e. a set of sequences) is said to be consistent with the definition
of the `subsequence-of` operator, if the following is true: If two sequences
have one or more patterns in common, then one sequence is a subsequence of
the other.

Note that this kind of consistency does not require that for each sequence (S1)
another sequence (S2) exists with which the first set (S1) has any pattern in
common. A sequence may exist that does not share any elements/patterns with any
other sequence (hint: a forest).

Note that such a setup does not have two sequences that overlap each other.

**Memory hook**
Consistent: None of the borders of any two of the sequences cross each other.

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

**CLARIFICATION**
A setup is said to be inconsistent with the definition of the `subsequence-of`
operator, if the following is true: Two sequences exist that have one or more
elements in common, but none of those two is a subsequence of the other.

Note that such a setup has at least two sequences that overlap each other.

**Memory hook**
Consistent: Sequences must be continuous and must not overlap each other.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
With regards to a consistent setup, the following references may be used:

* The next outer sequence (S2) of a subsequence (S1)
  is said to be the subsequence's (S1) parent sequence (S2).
* The sequence, to which another sequence is its parent sequence,
  is said to be one of the parent sequence's child sequences.
* All the subsequences of a sequence
  are said to be the sequence's inner or descendant sequences.
* A sequence to which another sequence is a descendant sequence
  is said to be one of the sequence's outer or ancestor sequences.
* A sequence that has no outer sequence is said to be a root sequence.
* A set of sequences that has no more than one root sequence
  is said to be a hierarchy of sequences.
* A set of sequences that has more than one root sequence
  is said to be a forest of hierarchies.

Note that a root sequence is no subsequence of any other sequence.

```
|s-------------------------------------------------|
|    |t--------------------------|    |w---------| |
|    |    |u------|    |v------| |    |    |x--| | |
| 0, | 1, | 2, 3, | 4, | 5, 6, | | 7, | 8, | 9 | | |
|    |    |-------|    |-------| |    |    |---| | |
|    |---------------------------|    |----------| |
|--------------------------------------------------|
```

* Root sequence `s` is the parent sequence of sequences `t` and `w`.
* Sequence `t` is the parent sequence of `u` and `v`.
* Sequences `s` and `t` are both outer or ancestor sequences of `u` and `v`.
* Sequences `u` and `v` are both inner or descendant sequences of `s` and `t`.
* Sequences `u`, `v` and `w` are independent from one another.

**CLARIFICATION**
If sequence `u` is a subsequence of `t`, sequence `x` a subsequence of `w`, and
if sequences `t` and `w` are independent from one another, then both sequences
(`u` and `x`) are also independent from one another.

In general, any two subsequences of two independent sequences
are also independent from one another.
