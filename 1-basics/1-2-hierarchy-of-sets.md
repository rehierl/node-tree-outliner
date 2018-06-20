
<!-- ======================================================================= -->
# Subsets of elements

* `(V subset-of W) := (v in W) for any (v in V)`
* `(V strict-subset-of W) := (V subset-of W) and (V != W)`

```
A = { 1, 2 }
B = { 2 }
C = { 2, 3 }
D = { {2}, 3 }
E = { 3, 4 }
```

* Any set (e.g. A) is a subset to itself.
* Set B is a (strict) subset of set A, but A is not a subset of B.
* Set C is not a subset of set A, and A not a subset of C.
* Number 2 is a common element of sets A and C, but not of set D.
* Set C does not contain set B as an element, set D however does.
* Set C is not a subset of set D, and D not a subset of C.

**CLARIFICATION**
Set A and E are said to be **independent** from one another
because both sets have no elements in common.

**CLARIFICATION**
A set of sets is said to be **disjoint**,
if each set within that super-set is independent to all other sets.

**CLARIFICATION**
Set A is said to **(loosely) contain** set B
because B is a subset of A.

Note that this "contains" definition is with regards to the `subset-of` operator
and therefore needs to be understood as "contains the elements of" instead of
"contains as an element". In order to distinguish both notions, one could use
qualifiers similar to "loosely contains" (i.e. contains the elements of) and
"strictly contains" (i.e. contains as an element):

* A loosely contains B.
* i.e. B has no borders within A.
* synonymous - resolved-into, merged-into
* D strictly contains B.
* i.e. B has its own borders within D.

Note that A can be said to contain itself.
In contrary to that, A neither contains C nor E.

**CLARIFICATION**
Set B is said to be **(loosely) embedded** into set A
because B is a strict subset of A.

Note that similar as before, the "loose" definition is with regards to B being
a subset of A and A having one or more additional elements. In contrary to that,
the "strict" counterpart is that B would have to be an element of A in addition
to A having one or more additional elements.

* B is loosely embedded into A.
* B is strictly embedded into D.

Note that A can not be said to be embedded into itself.
That is, A is neither loosely nor strictly embedded into itself.

**CLARIFICATION**
Set C is said to **overlap** set E.

Which is because both sets have elements in common,
and because both have elements which the other set does not have.

Note that set E also overlaps set C.
Both sets therefore can be said to overlap each other.

Note that neither of those two sets is embedded into the other.

<!-- ======================================================================= -->
## Visual representations

```
set-of-sets = {
  A = { 1, 2, 3, 4, 5 },
  B = { 2 },
  C = { 3, 4 }
}
```

This set-of-sets could be visualized using the following
box-based representation:

```
|-A-----------------|
| 1 |-B-| |-C---| 5 |
|   | 2 | | 3   |   |
|   |---| |   4 |   |
|         |-----|   |
|-------------------|
```

<!-- ======================================================================= -->
## Consistent setup

```
|-A---------------------| |-E-|
| |-B-----|   |-C-----| | | 7 |
| | 1   2 |   |     3 | | |---|
| |       |   |       | |
| | |-D-| |   |       | |
| | | 4 | | 5 | 6     | |
| | |---| |   |       | |
| |-------|   |-------| |
|-----------------------|
```

* Set A contains elements 1 to 6.
* Set B contains elements 1, 2 and 4.
* Set C contains elements 3 and 6.
* Set D only contains element 4.
* Set E only contains element 7.

Elements may belong to more than one set:

* Element 5 only belongs to set A.
* Elements 1 and 2 belong to sets A and B.
* Element 4 belongs to sets A, B and D.

Some of the relationships between those sets are:

* Set A contains set B.
* Set B is embedded into set A.
* Sets A and B contain set D.
* Set D is embedded into sets A and B.
* Set B is however independent of set C.

Note that there are no two sets that overlap each other.

**CLARIFICATION**
A setup (i.e. a set of sets) is said to be consistent (with regards to the
definition of the `subset-of` operator), if the following requirements are
satisfied:

1. If two sets have one or more elements in common,
   then one set is a subset of the other.

Note that each set is by definition a subset to itself.

Note that this kind of consistency does not require that for each set (S1)
another set (S2) exists with which the first set (S1) has any elements in
common. Put differently, such a setup may have more than one root set
(see below).

**Memory hook**
Consistent: None of the borders of any two sets cross each other.

<!-- ======================================================================= -->
## Inconsistent setup

```
|-A---------------------| |-E-|
| |-B-----|   |-C-----| | | 7 |
| | 1   2 |   |     3 | | |---|
| |       |   |       | |
| | |-D---|---|---|   | |
| | | 4   | 5 | 6 |   | |
| | |-----|---|---|   | |
| |-------|   |-------| |
|-----------------------|
```

Inconsistency

* Sets B and D both contain 4.
* Set D contains 5 and 6, both of which do not belong to set B.
* Set D is no longer a subset of set B.
* Set B contains 1 and 2, both of which do not belong to set D.
* Set B is also not a subset of set D.
* Sets B and D overlap each other.
* The borders of B and D cross each other.

Note that a similar inconsistency exists between sets C and D.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
With regards to a consistent setup, the following references may be used:

* The next outer set (S2) of a subset (S1) is the smallest set
  (in terms of number of elements), to which S1 is a subset.
* The next outer set (S2) of a subset (S1)
  is said to be the subset's (S1) parent set (S2).
* The set, to which another set is its parent set,
  is said to be one of the parent set's child sets.
* All the subsets of a set
  are said to be the set's inner or descendant sets.
* A set to which another set is a descendant set
  is said to be one of the set's outer or ancestor sets.
* Any ancestor set is said to be super-ordinate to
  (or more significant than) any of its descendant sets.
* Any descendant set is said to be sub-ordinate to
  (or less significant than) any of its ancestor sets.
* A set that has no outer set is said to be a root set.
* Two sets that have the same parent set
  are said to be sibling sets.

(simple) hierarchies:

* A set of sets that has no more than one root set
  is said to be a hierarchy of sets.
* A set of sets that has more than one root set
  is said to be a forest of hierarchies.

Note that a root set is no subset to any other set than itself.

strict hierarchies:

* A strict hierarchy is based upon the `strict-subset-of`
  operator instead of the "simple" `subset-of` operator.
* A strict hierarchy is a hierarchy in which each set has
  one or more elements that none of its strict subsets has.
* A strict forest of hierarchies is a forest of hierarchies
  in which each hierarchy is strict.

Note that a root set is no strict subset to any set,
including itself.

Note that a strict hierarchy is also a simple hierarchy.

```
|-A---------------------| |-E-|
| |-B-----|   |-C-----| | | 7 |
| | 1   2 |   |     3 | | |---|
| |       |   |       | |
| | |-D-| |   | |-F-| | |
| | | 4 | | 5 | | 6 | | |
| | |---| |   | |---| | |
| |-------|   |-------| |
|-----------------------|
```

* Root set A is the parent set of sets B and C.
* Set B is the parent set of set D.
* Sets A and B both are outer or ancestor sets of set D.
* Sets B, C and D all are inner or descendant sets of set A.
* Sets B and C are sibling sets and independent from one another.

**CLARIFICATION**
If set D is a subset of set B, set F a subset of set C, and if sets B and C are
independent from one another, then both subsets (D and F) are also independent
from one another.

In general, any two subsets of two independent sets
are also independent from one another.
