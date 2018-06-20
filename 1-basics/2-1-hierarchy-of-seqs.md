
<!-- ======================================================================= -->
# Subsequences of elements

```
s, A = [ s(1), s(2), ..., s(o), s(o+1), ..., s(o+n), s(o+n-1), ..., s(N) ]
t, B = [                  t(1), t(2),   ..., t(n-1), t(n)                ]
```

* `(t subsequence-of s) := (t infix-of s)`
* `t` is a subsequence of `s`, if `t` can be located within `s`
* `t infix-of s`, if `(s(o+j-1) = t(j))` for some offset `o in [1,N]`,
  `t`'s length `n in [1,(N-o+1)]` and all indexes `j in [1,n]`

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

Note that, if B is a subsequence of A, then A may also be a subsequence of B
(i.e. both are identical). That is, similar to the `subset-of` operator, each
sequence is a subsequence to itself. If, in contrary to that, B is a strict
subsequence of A, then A can not also be a (strict) subsequence of B. That is,
a sequence can not be a strict subsequence to itself.

<!-- ======================================================================= -->

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

<!-- ======================================================================= -->
## Visual representations

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
## Consistent setup

```
0 1 2 3 4 5 6 7 8 9 - A
  ===========   === - B,E
    ===   ===       - C,D
```

* Sequence A contains all numbers from `0` to `9`.
* Sequence B contains all numbers from `1` to `6`.
* Sequence E contains only contains the numbers `8` and `9`.
* Sequence C contains the numbers `2` and `3`.
* Sequence D contains the numbers `5` and `6`.

Elements may belong to more than one sequence:

* Elements `1` and `4` belong to A and B.
* Elements `8` and `9` belong to A and E.
* Elements `2` and `3` belong to A, B and C.
* Elements `5` and `6` belong to A, B and D.

Some of the relationships between those sequences are:

* B and E both are subsequences of A.
* C and D both are subsequences of A and B.
* E is independent of B, C and D.

**CLARIFICATION**
A setup (i.e. a set of sequences) is said to be consistent (with regards to the
definition of the `subsequence-of` operator), if the following requirements are
satisfied:

1. Each sequence represents a set of values (see below: distinct)
2. If two sequences have one or more elements in common,
   then one sequence is a subsequence of the other.

Note that this kind of consistency does not require that for each sequence (S1)
another sequence (S2) exists with which the first sequence (S1) has any pattern
in common. A sequence may exist that does not share any elements/patterns with
any other sequence. Put differently such a setup may have more than one root
sequence (see below).

Note that there is no pair of sequences that overlap each other.

**Memory hook**
Consistent: None of the borders of any two of the sequences cross each other.

<!-- ======================================================================= -->
## Inconsistent setup

Inconsistency 1

```
0 1 2 3 4 5 6 7 8 9 - A
  =======   ===     - B
```

* Sequence B is defined as `B = [1,2,3,4,6,7]`
* Sequence B is not continuous with regards to A.
* Sequence B has a gap because it does not contain `5`.
* Sequence B is not a subsequence of A.

Inconsistency 2

```
0 1 2 3 4 5 6 7 8 9 - A
    ===========     - C
            =====   - D
```

* Sequences C and D share the pattern `[6,7]`.
* Both sequences overlap each other.
* None of those two is a subsequence of the other.
* The borders of C and D cross each other.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
With regards to a consistent setup, the following references may be used:

* The next outer sequence (S2) of a subsequence (S1) is
  the shortest sequence, to which S1 is a subsequence.
* The next outer sequence (S2) of a subsequence (S1)
  is said to be the subsequence's (S1) parent sequence (S2).
* The sequence, to which another sequence is its parent sequence,
  is said to be one of the parent sequence's child sequences.
* All the subsequences of a sequence
  are said to be the sequence's inner or descendant sequences.
* A sequence to which another sequence is a descendant sequence
  is said to be one of the sequence's outer or ancestor sequences.
* A sequence that has no outer sequence is said to be a root sequence.
* Two sequences that have the same parent sequence
  are said to be sibling sequences.

(simple) hierarchies:

* A set of sequences that has no more than one root sequence
  is said to be a hierarchy of sequences.
* A set of sequences that has more than one root sequence
  is said to be a forest of hierarchies.

Note that a root sequence is no subsequence to any other sequence than itself.

strict hierarchies:

* A strict hierarchy is based upon the `strict-subsequence-of`
  operator instead of the "simple" `subsequence-of` operator.
* A strict hierarchy is a hierarchy in which each sequence has
  one or more elements that none of its strict subsequences has.
* That is, any subsequence is a strict subsequence to all of
  its ancestor sequences.
* A strict forest of hierarchies is a forest of hierarchies
  in which each hierarchy is strict.

Note that a root sequence is no strict subsequence to any sequence,
including itself.

Note that a strict hierarchy is also a simple hierarchy.

```
|-A------------------------------------------------|
|    |-B-------------------------|    |-E--------| |
|    |    |-C-----|    |-D-----| |    |    |-F-| | |
| 0, | 1, | 2, 3, | 4, | 5, 6, | | 7, | 8, | 9 | | |
|    |    |-------|    |-------| |    |    |---| | |
|    |---------------------------|    |----------| |
|--------------------------------------------------|
```

* Root sequence A is the parent sequence of sequences B and E.
* Sequence B is the parent sequence of C and D.
* Sequences A and B are both outer or ancestor sequences of C and D.
* Sequences C and D are both inner or descendant sequences of A and B.
* Sequences C, D and F are independent from one another.

**CLARIFICATION**
If sequence C is a subsequence of B, sequence F a subsequence of E, and if
sequences B and F are independent from one another, then both sequences
(C and F) are also independent from one another.

In general, any two subsequences of two independent sequences
are also independent from one another.

<!-- ======================================================================= -->
## Distinct setup

```
0 1 2 3 4 5 2 3 8 9 - A
  ======= =======   - C, D
```

* Sequences B and C share the pattern `B = [2,3]`.
* Both are not independent from one another.
* Both sequences do not overlap each other.
* C is not a subsequence of D and D not a subsequence of C.
* The consistency requirement is violated.

Note that there are similar issues, if B is a suffix xor prefix of C xor D.

```
0 1 2 3 4 5 2 3 8 9 - A
    ===     ===     - B, B
```

* Sequences A and B share the pattern `[2,3]`.
* Sequence B is a (strict) subsequence to A.
* The consistency requirement is satisfied.

Even though the above setup is consistent and therefore counts as a hierarchy,
sequence B has no definite position within A. And because there are two offsets
at which B can be located, B can be said to have A twice as parent sequence.
Because of that, the hierarchy can be understood to be broken.

```
0 1 2 3 4 5 2 3 8 9 - A
    ===   =======   - B, D
            ===     - B
```

* Sequences A, B and C share the pattern `[2,3]`.
* Sequence B is a subsequence of A and C.
* The consistency requirement is satisfied.

From a strict perspective, B's parent sequence (shortest next outer) is B.
However, from a less strict perspective, A could also be considered to be B's
parent sequence, which is why B could be considered to have two unique parent
sequences. Consequently, the hierarchy is broken.

```
0 1 2 3 4 5 6 3 8 9 - A
      =       =     - B
```

Note that similar issues arise, if B is a sequence of length 1.

**CLARIFICATION**
A setup is said to be **a distinct setup** if (and only if) each sequence
within the setup represents a set of values.

Note that distinct setups are the main object of discussion. Because of that,
it is an implicit requirement that every setup needs to be distinct.

Note that a setup, which is not distinct, does not necessarily have any issues.
Nothing bad will happen, if repeated patterns appear within a single sequence
but nowhere else. To be more accurate, repeated patterns may only appear within
root sequences.
