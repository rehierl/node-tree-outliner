
<!-- ======================================================================= -->
# Subsets of elements

Note that the definition operator (i.e. `X := Y`) in the following examples
needs to be read as "Element X declares set of elements Y".

```
A := { B, C, D }
B := { C }
C := { D, E }
```

* `(V subset-of W) := (v in W) for any (v in V)`
* `(V strict-subset-of W) := (V subset-of W) and (V != W)`
* Set B is a (strict) subset of set A, but A is not a subset of B.
* Set C is not a subset of set A, and A not a subset of C.
* However, set A and C still share the common element D.

```
D := { 1 }
E := { 1, 2 }
F := { { 1 }, 2 }
```

* Set D is a strict subset of set E.
* Set E does not contain set D, but set F does.
* Set E is not a subset of set F, and F is not a subset of E.

Note that from a strict perspective E does not contain D, because D is not an
element of E. However, E can still be loosely said to contain D, if it is clear
that the statement refers to the `subset-of` relationship.

**CLARIFICATION**
Set A and C are said to be **independent** from one another.

Which is because both sets have no elements in common.

**CLARIFICATION**
Set B is said to be **embedded** into set A.

Which is because B is a strict subset of A.

**CLARIFICATION**
Set C is said to **overlap** set A.

Which is because both sets have elements in common,
and because both have elements which the other set does not have.

Note that neither of the two sets is embedded into the other. Set A therefore
also overlaps set B, which is why both sets can be said to overlap each other.

<!-- ======================================================================= -->
## Visual representations

```
A := { B, C, D, E, F, G, H }
B := { C }
D := { E, F }
G := { H }
```

A visual representation that combines these declarations into one "image" is:

```
 A
|-----------------------|
|  B      D        G    |
| |---|  |-----|  |---| |
| | C |  | E   |  | H | |
| |---|  |   F |  |---| |
|        |-----|        |
|-----------------------|
```

Note that element A is an element, which does not belong to any of the above
sets of elements. However, A can be understood to declare and represent a set,
which will be referred to as "set A". Likewise, elements B, D and G declare
and represent their own sets of elements.

<!-- ======================================================================= -->
## A consistent setup

```
 A                           J
|-------------------------| |---|
|  B             C        | | K |
| |---------|   |-------| | |---|
| | D  E    |   |     F | |
| |   |---| |   |       | |
| |   | G | | H | I     | |
| |   |---| |   |       | |
| |---------|   |-------| |
|-------------------------|
```

* Set A contains elements B to I.
* Set B contains elements D, E and G.
* Set C contains elements F and I.
* Set E only contains element G.
* Set J only contains element K.

Elements may belong to more than one set:

* Elements B, C and H only belong to set A.
* Elements D and E belong to sets A and B.
* Element G belongs to sets A, B and E.
* Elements F and I belong to sets A and C.

Some of the relationships between those sets are:

* Set B is a subset of set A.
* Set E is a subset of sets A and B.
* Set B is independent of set C.

**CLARIFICATION**
A setup (i.e. a set of sets) is said to be consistent with the definition
of the `subset-of` operator, if the following is true: If two sets have one
or more elements in common, then one set is a subset of the other.

Note that this kind of consistency does not require that for each set (S1)
another set (S2) exists with which the first set (S1) has any elements in
common. For example, set J has no element in common with any of the other
sets (hint: a forest).

Note that such a setup does not have two sets that overlap each other.

**Memory hook**
Consistent: None of the borders of any two of the sets cross each other.

<!-- ======================================================================= -->
## An inconsistent setup

```
 A
|-----------------------|
|  B           C        |
| |-------|   |-------| |
| | D  E  |   |     F | |
| |   |-----------|   | |
| |   | G | H | I |   | |
| |   |-----------|   | |
| |-------|   |-------| |
|-----------------------|
```

Inconsistency 1

* Sets B and E both contain G.
* Set E contains H and I, both of which do not belong to set B.
* Set E is *not* a subset of set B.
* Set B contains D and E, both of which do not belong to set E.
* Set B is *not* a subset of set E.
* Sets B and E overlap each other.

Inconsistency 2

* Sets C and E both contain I.
* Set E contains G and H, both of which do not belong to set C.
* Set E is *not* a subset of set C.
* Set C contains F, which does not belong to set E.
* Set C is *not* a subset of set E.
* Sets C and E overlap each other.

**CLARIFICATION**
A setup is said to be inconsistent with the definition of the `subset-of`
operator, if the following is true: Two sets exist that have one or more
elements in common, but none of those two sets is a subset of the other.

Note that such a setup has at least two sets that overlap each other.

**Memory hook**
Inconsistent: The borders of two or more sets cross each other.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
With regards to a consistent setup, the following references may be used:

* The next outer set (S2) of a subset (S1)
  is said to be the subset's (S1) parent set (S2).
* The set, to which another set is its parent set,
  is said to be one of the parent set's child sets.
* All the subsets of a set
  are said to be the set's inner or descendant sets.
* A set to which another set is a descendant set
  is said to be one of the set's outer or ancestor sets.
* A set that has no outer set is said to be a root set.
* A set of sets that has no more than one root set
  is said to be a hierarchy of sets.
* A set of sets that has more than one root set
  is said to be a forest of hierarchies.
* Two sets that have the same parent set
  are said to be sibling sets.

Note that a root set is no subset of any other set.

```
 A
|-------------------------|
|  B             C        |
| |---------|   |-------| |
| | D  E    |   |  F    | |
| |   |---| |   | |---| | |
| |   | G | | H | | I | | |
| |   |---| |   | |---| | |
| |---------|   |-------| |
|-------------------------|
```

* Root set A is the parent set of sets B and C.
* Set B is the parent set of set E.
* Sets A and B both are outer or ancestor sets of set E.
* Sets B, C and E all are inner or descendant sets of set A.
* Sets B and C are sibling sets and independent from one another.

**CLARIFICATION**
If set E is a subset of set B, set F a subset of set C, and if sets B and C are
independent from one another, then both subsets (E and F) are also independent
from one another.

In general, any two subsets of two independent sets
are also independent from one another.
