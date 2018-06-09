
<!-- ======================================================================= -->
# Subsets of elements

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

Element A is an element, that does not belong to any of the displayed sets of
elements. However, it can be understood to define and represent the outermost
box/set of elements. Likewise, elements B, C and E define and represent their
own sets of elements.

* Elements B to I all belong to set A.
* Set A is said to contain elements B to I.
* Set B contains elements D, E and G.
* Set C contains elements F and I.
* Set E only contains element G.

Elements may belong to one or more sets of elements:

* Elements B, C and H only belong to set A.
* Elements D and E belong to set A and set B.
* Element G belongs to set A, set B and set E.
* Elements F and I belong to set A and set C.

The relationships between those sets of elements:

* `(V subset-of W) := ((v in W) for any (v in V))`
* Set B is a subset of set A.
* Set E is a subset of set B and also of set A.
* Set C is a subset of set A.
* There are no more relationships.
* e.g. Set B is not a subset of set C.

**CONCLUSION**
Such a setup (i.e. a set of sets) is said to be consistent with the definition
of the `subset-of` operator, if the following is true: If two sets have one or
more elements in common, then one set is a subset of the other.

Note that this kind of consistency does not require that for each set (S1)
another set (S2) exists with which the first set has one or more elements in
common. That is, such a second set does not have to exist (hint: a forest).

**Memory hook**
Consistent: None of the borders of any two of the sets cross each other.

<!-- ======================================================================= -->
## An inconsistent setup

What if set E would also contain elements H and I?

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
* Set E contains H and I, which both do not belong to set B.
* Set E is *not* a subset of set B.
* Set B contains D and E, which both do not belong to set E.
* Set B is *not* a subset of set E.

Inconsistency 2

* Sets C and E both contain I.
* Set E contains G and H, which both do not belong to set C.
* Set E is *not* a subset of set C.
* Set C contains F, which does not belong to set E.
* Set C is *not* a subset of set E.

Set E overlaps other sets.

* Set E has an element which set B also has, and
  it has elements which set B does not have.
* Set E overlaps set B.
* Set E has an element which set C also has, and
  it has element which set C does not have.
* Set E overlaps set C.

**CONCLUSION**
Such a setup is said to be inconsistent with the definition of the `subset-of`
operator, if the following is true: If two sets have one or more elements in
common, then none of those two sets is a subset of the other. In such a case,
both sets are said to "overlap" each other.

**Memory hook**
Inconsistent: The borders of two or more sets cross each other.

<!-- ======================================================================= -->
## derived statements

**CONCLUSION**
With regards to a consistent setup, the following references may be used:

* The next outer set (S2) of another set (S1) will be
  referred to as the initial set's parent set.
* The set to which another set is a parent set will be
  referred to as one of the parent set's child sets.
* All inner sets of an outer set will be
  referred to as the outer set's inner or descendant sets.
* All the sets to which a set is a descendant set will be
  referred to as the set's outer or ancestor sets.
* A set that has no outer set will be referred to as a root set.
* A set of sets that has no more than one root set will be
  referred to as a hierarchy of sets.
* A set of sets that has more than one root set will be
  referred to as a forest of such hierarchies.

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
* Sets A and B both are outer or ancestor sets to set E.
* Sets B, C and E all are inner or descendant sets to set A.
