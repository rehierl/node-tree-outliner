
element-of vs. subsequence-of -
similar to contains vs. embedded -
only with regards to sequences -
`s = [1, [2, 3], 4]`, `t = [2, 3]` -
`t` is an element of `s = [1, t, 4]` -
that is, an element in `s` has `t` as its value -
`s = [1, 2, 3, 4]`, `t = [2, 3]` -
`t` is an infix/subsequence of `s`

* a set of sequences `S` contains sequences only
* `(is-sequence s)` is true for any `s in S`
* any sequence `s in S` may have any length - i.e. `#s in [0,*]`
* `(#si != #sj)` may be true for any two sequences `(si !== sj)`

inverted set of sequences (S')

* `S', inv(S) := { inv(s) : s in S }`
* `inv(inv(S)) <-> S`

<!-- ======================================================================= -->
## introduction

```
set-of-sequences = {
  A = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ],
  B = [    1, 2, 3, 4, 5, 6          ],
  C = [       2, 3,                  ],
  D = [                5, 6, 7       ],
  E = [                         8, 9 ]
}
```

This set-of-sequences could be visualized using the following
box-based representation:

```
|-A--------------------------------------------|
|    |-B-----------------------|               |
|    |    |-C-----|    |-D----------| |-E----| |
| 0, | 1, | 2, 3, | 4, | 5, 6, | 7, | | 8, 9 | |
|    |    |-------|    |------------| |------| |
|    |-------------------------|               |
|----------------------------------------------|
```

Note that the borders of sequences B and D cross each other.
That is, both sequences overlap each other.

An even more compact,
line-based representation is:

```
0 1 2 3 4 5 6 7 8 9 - ordered set
0 1 2 3 4 5 6 7 8 9 - A
  1 2 3 4 5 6   8 9 - B,E
    2 3   5 6 7     - C,D
```

Note that the order of numbers within each sequence (A to E) corresponds with
the order of numbers within the ordered set of numbers. Furthermore, sequence
A is "identical" to the ordered set. Because of that, the numbers only have to
be specified once by the "root sequence" (see below).

Note that the left-to-right order of identifiers (i.e. A to E) to the right
corresponds with the order of sequence definitions (i.e. the lines of `=`
characters): That is, the range of B begins with `1` and ends with `6`.

```
0 1 2 3 4 5 6 7 8 9 - A
  ===========   === - B,E
    ===   =====     - C,D
```

Note that it can still be visually detected whether or not two sequences
(e.g. B and D) overlap each other.

```
0 1 2 3 4 5 6 7 8 9 - A
  ===========   === - B,E
    ===   =====     - C,D
                    - F
```

Obviously, the line-based representation is more compact than the box-based
representation. However, this line-based representation only insufficiently
allows to include empty sequences (e.g. empty line/sequence F). Unfortunately,
and if visualized that way, empty sequences appear out of context. That is,
unlike with non-empty sequences, there is no "visual connection" of an empty
sequence with all the other sequences. Because of that, line-based "images"
will only be used in combination with non-empty sequences.


<!-- ======================================================================= -->
## linear sequences

```
A = [0,0,1,1,1,4,3,2,6,7]
B = [9,8,7,6,3,2,1,0,4,5]
C = [0,1,2,3,4,5,6,7,8,9]
X = [3,2], Y = [4,5], Z = [6,7]
```

* A, B and C all are sequences of elements/values.
* X is a subsequence of A and B.
* A and B share the (common) pattern X.
* B and C share pattern Y.
* A and C share pattern Z.
* All sequences are different from one another
  i.e. they differ in elements and/or length.
* No sequence (in `{A,B,C}`) is a subsequence of another sequence.

```
B = [9,8,7,6,3,2,1,0,4,5]
C = [0,1,2,3,4,5,6,7,8,9]
```

* Sequences B and C contain no element more than once.
* B and C can both be said to represent a sequentialized **set of values**.
* All of their values have an implicit order - e.g. `(2 < 3)`.
* B and C can both be said to represent **ordered sets of values**.
* That is regardless of where each value is located within a sequence.

```
C = [0,1,2,3,4,5,6,7,8,9]
```

* The indexes of each element within C corresponds with the order of elements.
* That is, if `(i < j)`, then also `(C[i] < C[j])`

Note that sequences which represent ordered sets of elements/values *and* in
which the positions of its elements correspond with the order of elements, are
integral to the whole discussion. Unfortunately, there does not seem to exist
a term that could be used to refer to this combination of characteristics.

Note that such sequences could be described as: A sequence of values in which
the position of each value corresponds with a particular order (e.g. `<`).

<!-- ======================================================================= -->
## (strict) subsequence

```
s, A = [ s(1), s(2), ..., s(o), s(o+1), ..., s(o+n), s(o+n-1), ..., s(N) ]
t, B = [                  t(1), t(2),   ..., t(n-1), t(n)                ]
```

* `(t subsequence-of s) := (t infix-of s)`
* `t` is a subsequence of `s`, if `t` can be located within `s`
* `t infix-of s`, if `(s(o+j-1) = t(j))` for some offset `o in [1,N]`,
  `t`'s length `n in [1,(N-o+1)]` and all indexes `j in [1,n]`
* Note that any sequence is a subsequence to itself.

Note that this definition of "subsequence" deviates from the mathematical
definition in such a way that a subsequence must represent an exact pattern
within the other sequence (i.e. no gaps allowed). As such this definition
is more strict and needs to be understood with the notion of "substring".

Note that there may be one or more offsets beginning with which the pattern
of B can be found in A. That is, B may be "embedded into" A more than once.

Note that B's offset within A may be 1. In that case, both sequences begin with
the same element (i.e. B is a prefix of A). Likewise, B's offset may be such
that B and A both end with the same element (i.e. B is a suffix of A).

* `(t strict-subsequence-of s) := (t subsequence-of s) and (t != s)`
* if `(t strict-subsequence-of s)`, then `(#t < #s)`
* if `(t strict-subsequence-of s)`, then `t` is not a prefix and/or a suffix
* Note that no sequence is a strict subsequence to itself.

Note that, if B is a subsequence of A, then A may also be a subsequence of B
(i.e. both are identical). That is, similar to the `subset-of` operator, each
sequence is a subsequence to itself. If, in contrary to that, B is a strict
subsequence of A, then A can not also be a (strict) subsequence of B. That is,
a sequence can not be a strict subsequence to itself.

<!-- ======================================================================= -->
## disjoint, overlap, continuous, ...

```
A = [ 1, 2 ]
B = [ 2 ]
C = [ 2, 3 ]
D = [ [2], 3 ]
E = [ 3, 4 ]
```

* Any sequence (e.g. A) is a subsequence to itself.
* Sequence B is a strict subsequence of A.
* Sequence C is not a subsequence of A, and A not a subsequence of C.
* Number 2 is a common element of sequences A and C, but not of D.
* Sequence C does not contain B as an element, sequence D however does.
* Sequence C is not a subsequence of D, and D is not a subsequence of C.

**CLARIFICATION**
Two sequences A and E are said to be **independent** from one another, if no
sequence X exists such that: `(X subsequence-of A)` and `(X subsequence-of E)`

Note that this includes not having even one element in common. That is,
because each element can be understood to represent a pattern of length 1.

**CLARIFICATION**
A set of sequences is said to be **disjoint**,
if each sequence within that set is independent to all other sequences.

**CLARIFICATION**
Sequence A is said to **(loosely) contain** sequence B
because B is a subsequence of A.

From a strict perspective, and similar to sets, A does not contain B because B
is not an element of A. However, A may still be said to loosely contain B, if
it is clear that the statement refers to the `subsequence-of` operator.

* A loosely contains B.
* i.e. B has no borders within A.
* synonymous - resolved-into, merged-into
* D strictly contains B.
* i.e. B has its own borders within D.

Note that A can be said to contain itself.
In contrary to that, A neither contains C nor E.

**CLARIFICATION**
Sequence B is said to be **(loosely) embedded** into sequence A
because B is a strict subsequence of A.

Note that, similar as before, the "loose" definition is with regards to B being
a subsequence of A and A having one or more additional elements. In contrary to
that, the "strict" counterpart is that B would have to be an element of A in
addition to A having one or more additional elements.

* B is loosely embedded into A.
* B is strictly embedded into D.

Note that A can not be said to be embedded into itself.
That is, A is neither loosely nor strictly embedded into itself.

**CLARIFICATION**
Sequence C is said to **overlap** sequence E.

Which is because both share the common pattern `[3]`, and because both have one
or more patterns that the other sequence does not have.

Note that neither of the two sequences is embedded into the other. Sequence E
therefore also overlaps C, which is why both sequences can be said to overlap
each other.

In addition to that, and due to the order of the elements,
C is said to reach into E, and E to reach out of C.

Also note that C ends with a prefix of E, and E begins with a suffix of C.
That is, a suffix of one sequence is a prefix of the other.

```
A = [0,1,2,3,4,5,6,7,8,9]
B = [3,4], C = [3,5]
```

**CLARIFICATION**
Sequence B is said to be **continuous** with regards to A as it is a subsequence
of A. In contrary to that, C is said to have a **gap** with regards to A as it
does not contain the interim number `4`. As such, C is no subsequence of A. That
is, in order to be continuous, a sequence must contain all available elements
within a given **range**.
