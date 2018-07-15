
**TODO** - (open aspects)

<!-- ======================================================================= -->
# Setup of sequences

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
