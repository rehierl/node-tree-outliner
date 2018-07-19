
**TODO** - (open aspects)

<!-- ======================================================================= -->
# Hierarchy of sequences

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
