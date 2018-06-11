
<!-- ======================================================================= -->
# Subsets of elements

Note that the definition operator (i.e. `X := Y`) in the following examples
needs to be read as "Element X declares set Y", not as an operator that
establishes an identity.

```
A := { B, C, D }
B := { C }
C := { D, E }
```

* `(V subset-of W) := ((v in W) for any (v in V))`
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
* Set E does not (strictly) contain set D (as an element).
* Set E is not a subset of set F, and F is not a subset of E.

Note that from a strict perspective E does not contain D, because D is not an
element of E. However, E can still be loosely said to contain D, if it is clear
that the statement refers to the `subset-of` relationship.

**CONCLUSION**
Set B is said to be **embedded** into set A,
if B is a strict subset of A.

**CONCLUSION**
Set C is said to **overlap** set A, if both share common elements
and if both sets contain elements that the other set does not have.

Note that neither of the two sets is embedded into the other. Set A therefore
also overlaps set B. Both both sets can therefore be said to overlap each other.

<!-- ======================================================================= -->
## An equivalent visual definition

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

Note that element A is an element, that does not belong to any of the above
sets of elements. However, A can be understood to declare and represent a set,
which will be referred to as "set A" that contains the elements B to H.
Likewise, elements B, D and G declare and represent their own sets of elements.

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

Elements may belong to one or more sets of elements:

* Elements B, C and H only belong to set A.
* Elements D and E belong to set A and set B.
* Element G belongs to set A, set B and set E.
* Elements F and I belong to set A and set C.

The relationships between those sets of elements:

* Set B is a subset of set A.
* Set E is a subset of set B.
* Set E is also a subset of set A.
* Set C is a subset of set A.
* Set B is not a subset of set C.

**CONCLUSION**
A setup (i.e. a set of sets) is said to be consistent with the definition
of the `subset-of` operator, if the following is true: If two sets have one
or more elements in common, then one set is a subset of the other.

Note that this kind of consistency does not require that for each set (S1)
another set (S2) exists with which the first set (S1) has any elements in
common. For example, set J has no element in common with any of the other
sets (hint: a forest).

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

**CONCLUSION**
A setup is said to be inconsistent with the definition of the `subset-of`
operator, if the following is true: Two sets exist that have one or more
elements in common, but none of those two sets is a subset of the other.

**Memory hook**
Inconsistent: The borders of two or more sets cross each other.

<!-- ======================================================================= -->
## derived statements

**CONCLUSION**
With regards to a consistent setup, the following references may be used:

* The next outer set (S2) of another set (S1) will be
  referred to as the second set's (S1) parent set (S2).
* The set to which another set is its parent set will be
  referred to as one of the parent set's child sets.
* All inner sets of an outer set will be
  referred to as the outer set's inner or descendant sets.
* All the sets to which a set is a descendant set will be
  referred to as the set's outer or ancestor sets.
* A set that has no outer set will be referred to as a root set.
* A set of sets that has no more than one root set will be
  referred to as a hierarchy of sets.
* A set of sets that has more than one root set will be
  referred to as a forest of hierarchies.
* Two sets that have no elements in common are said to be
  independent from one another.

Note that a root set is no subset to another set.

```
 A
|-------------------------|
|  B             C        |
| |---------|   |-------| |
| | D  E    |   |     F | |
| |   |---| |   |       | |
| |   | G | | H | I     | |
| |   |---| |   |       | |
| |---------|   |-------| |
|-------------------------|
```

* Root set A is the parent set of set B and C.
* Set B is the parent set of set E.
* Sets A and B both are outer or ancestor sets of set E.
* Sets B, C and E all are inner or descendant sets to set A.
* Sets B and C are independent from one another.

**CONCLUSION**
If set "a" is a subset of set "A", set "b" a subset of set "B", and if sets "A"
and "B" are independent from one another, then "a" and "b" are also independent
from one another.

Put differently, any two subsets of two independent sets are also independent
from one another.
