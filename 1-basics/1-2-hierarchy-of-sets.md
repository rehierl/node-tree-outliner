
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

* Like any other set, set A is a subset to itself.
* Set B is a (strict) subset of set A, but A is not a subset of B.
* Set C is not a subset of set A, and A not a subset of C.
* Number 2 is a common element of sets A and C, but not of set D.
* Set C does not contain set B as an element, set D however does.
* Set C is not a subset of set D, and D not a subset of C.

Note that from a strict perspective C does not contain B, because B is itself
not an element of C. However, C can still be loosely said to contain B, if it
is clear that the statement refers to the `subset-of` relationship.

**CLARIFICATION**
Set A and E are said to be **independent** from one another
because both sets have no elements in common.

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

Note that, similar to the "contains" definition, this "embedded" definition
needs to be understood to represent a loose definition. As before, qualifiers
can be used in order to distinguish both notions. However, "strict subset"
means "has more elements than" and "strictly embedded into"
means "is an element of" in addition to "strict subset".

* B is loosely embedded into A.
* B is strictly embedded into D.

Note that A can not be said to be embedded into itself.

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
A = { 1, 2, 3, 4, 5 }
B = { 2 }
C = { 3, 4 }
```

These definitions could be visualized as follows:

```
|-A-----------------|
| 1 |-B-| |-C---| 5 |
|   | 2 | | 3   |   |
|   |---| |   4 |   |
|         |-----|   |
|-------------------|
```

<!-- ======================================================================= -->
## A consistent setup

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
definition of the `subset-of` operator), if the following is true:

* If two sets have one or more elements in common,
  then one set is a subset of the other.

Note that each set is by definition a subset to itself.

Note that this kind of consistency does not require that for each set (S1)
another set (S2) exists with which the first set (S1) has any elements in
common. For example, set J has no elements in common with any of the other
sets (hint: a forest).

**Memory hook**
Consistent: None of the borders of any two sets cross each other.

<!-- ======================================================================= -->
## An inconsistent setup

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

Note that a similar inconsistency exists between sets C and D.

**CLARIFICATION**
A setup is said to be inconsistent (with regards to the definition of the
`subset-of` operator), if the following is true:

* Two sets exist that have one or more elements in common,
  but none of those two is a subset of the other.

Note that such a setup has at least two sets that overlap each other.

**Memory hook**
Inconsistent: The borders of two or more sets cross each other.

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
* A strict forest of hierarchies is a forest
  in which each hierarchy is strict.

Note that a root set is no strict subset to any other set.

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
