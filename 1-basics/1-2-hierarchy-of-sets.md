
<!-- ======================================================================= -->
# Subsets of elements

subset-of

* `(V subset-of W), (V simple-subset-of W) := (v in W) for any (v in V)`
* `(V subset-of W) and (W subset-of V)` is true if `(V = W)`
* The empty set `{}` is a subset to any set.
* Any set is a subset to itself.

strict-subset-of

* `(V strict-subset-of W) := (V subset-of W) and (V != W)`
* `(V strict-subset-of W) and (W strict-subset-of V)` is always false
* The empty set `{}` is a strict subset to any non-empty set.
* No set is a strict subset to itself.

```
set-of-sets = {
  A = { 1, 2 },
  B = { 1, {2} },
  C = { 2 },
  D = { 2, 3 },
  E = { 3, 4 }
}
```

* 2 is a common element of sets A, C and D.
* 2 is not a common element of sets A, B and E.
* Sets A and E have no common element.
* Set C is a (strict) subset of set A, but A is not a subset of C.
* Set A does not contain set C as an element, set B however does.
* Set A is not a subset of set D, and D not a subset of A.

**CLARIFICATION**
Set A and E are said to be **independent** from one another
because both sets have no elements in common.

Note that the empty set is independent to any other set.

**CLARIFICATION**
A set of sets is said to be **disjoint**,
if each set within the super-set is independent from all the other sets.

**CLARIFICATION**
Set A is said to **(loosely) contain** set C
because C is a subset of A.

Note that this "contains" definition is with regards to the `subset-of` operator
and therefore needs to be understood as "contains the elements of" instead of
"contains as an element". In order to distinguish both notions, one could use
qualifiers similar to "loosely contains" (i.e. contains the elements of) and
"strictly contains" (i.e. contains as an element):

* A (loosely) contains C - i.e. C has no borders within A.
* synonymous - resolved-into, merged-into
* B strictly contains C - i.e. C has a border within B.

Note that A can be said to contain itself.
In contrary to that, A neither contains D nor E.

**CLARIFICATION**
Set C is said to be **(loosely) embedded** into set A
because C is a strict subset of A.

Note that similar as before, the "loose" definition is with regards to C
being a subset of A and A having one or more additional elements. In contrary
to that, the "strict" counterpart is that C would have to be an element of A
in addition to A having one or more additional elements.

* C is (loosely) embedded into A - i.e. C has no borders within A.
* C is strictly embedded into B - i.e. C has borders within B.

Note that A can not be said to be embedded into itself.
That is, A is neither loosely nor strictly embedded into itself.

**CLARIFICATION**
"(strictly/loosely) contains" vs. "(strictly/loosely) embedded into":

* contains - i.e. (simple) subset
* embedded - i.e. strict subset
* if "embedded", then also "contains", but not vice versa
* loosely contains/embedded - i.e. resolved/merged into
* strictly contains/embedded - i.e. an element of

Note that the "contains" vs. "embedded" distinction is used to tell
whether or not an ancestor set has more elements than a descendant set.

Note that the "loosely" vs. "strictly" distinction could be used
with regards to content injection.

**CLARIFICATION**
Set D is said to **overlap** set A.

Which is because both sets have elements in common,
and because both have elements which the other set does not have.

Note that set A also overlaps set D.
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
box/border-based representation:

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
| | |-D-| |   | |-F-| | |
| | | 4 | | 5 | | 6 | | |
| | |---| |   | |---| | |
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

**CLARIFICATION**
If set D is a subset of set B, set F a subset of set C, and if sets B and
C are independent from one another, then both subsets (D and F) are also
independent from one another.

In general, any two subsets of two independent sets
are also independent from one another.

**CLARIFICATION**
A setup (i.e. a set of sets) is said to be consistent with regards to the
the `subset-of` operator, if the following requirement is met:

* If two sets have one or more elements in common,
  then one set is a subset of the other.
* synonymous - simple consistency, **simple setup**

Note that this kind of consistency does not require that for each set (S1)
another set (S2) exists with which the first set (S1) has any elements in
common (e.g. set E).

**CLARIFICATION**
A setup (i.e. a set of sets) is said to be consistent with regards to the
`strict-subset-of` operator, if the following requirement is met:

* If two sets have one or more elements in common,
  then one set is a strict subset of the other.
* synonymous - strict consistency, **strict setup**

Note that a strict setup is also a simple setup.
However, not every simple setup is also a strict setup:

* strict setup => simple setup

Note that the above setup is a strict and therefore also a simple setup.
If set A would not have element 5, then that setup would still be a simple
setup, but no longer a strict setup.

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

Note the crossing borders of sets B and D.

* Sets B and D both contain 4.
* Set D contains 5 and 6, both of which do not belong to set B.
* Set D is not a subset of set B.
* Set B contains 1 and 2, both of which do not belong to set D.
* Set B is also not a subset of set D.
* Sets B and D overlap each other.
* The borders of B and D cross each other.

Note that a similar inconsistency exists between sets C and D.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
With regards to simple/strict setups, the following references may be used:

* All (strict) subsets of a set
  are said to be the set's **inner** sets.
* All sets to which a set is a (strict) subset
  are said to be the set's **outer** sets.

With regards to a simple setup, and because any set is a subset to itself, any
set can be understood to be an inner and an outer set to itself. In contrary
to that, and with regards to a strict setup, no set is a strict subset and
therefore neither an inner, nor an outer set to itself.

Note that two sets, which are independent from each other, are not understood
to be outside of each other, not even if both sets have the same parent set
(i.e. siblings). That is, "outside" and "not inside" are not equivalent.

* Any outer set of set S (except for S itself) is an **ancestor set**
  and as such **super-ordinate** to (or **more significant** than) S.
* Any inner set of set S (except for S itself) is a **descendant set**
  and as such **sub-ordinate** to (or **less significant** than) S.

Note that no set is understood to be an ancestor
and/or a descendant set to itself.

Note that the empty set is a descendant set to any other set.
Because of that, a hierarchy (see below) must not contain the empty set.

* A set, that has no ancestor set, is said to be a **root set**.
* The least significant ancestor set of set S
  is said to be the **parent set** of S.
* Set S1 is said to be one of the **child sets** of set S2,
  if S2 is the parent set of S1.
* Two sets that have the same parent set
  are said to be **siblings** to each other.

Note that a simple/strict setup of non-empty sets (i.e. no crossing borders)
does not allow its sets to have more than one parent set. Because any ancestor
set is a descendant set to its own ancestor sets, outer sets are not independent
from one another. Consequently, any set that has ancestor sets also has exactly
one least significant ancestor set (i.e. its parent set).

Note that a set is not a parent set to itself (no loops). That is, because a
set is not understood to be an ancestor set to itself. Consequently, each set
either has no parent set (e.g. a root set), or exactly one parent set.

Note that a set can not be an ancestor set to itself (no cycles). Likewise,
a set can not be a descendant set to itself. That is, because a set can not
be a subset to one of its distinct inner sets. These sets always have less
elements than their ancestor sets.

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

<!-- ======================================================================= -->
## Hierarchy

**CLARIFICATION**
A setup (i.e. a set of sets) is said to be **a simple hierarchy**,
if the following requirements are met:

1. The setup is a simple setup.
2. The setup does not contain the empty set.
3. The setup has no more than one root set.

Note that each set within a hierarchy has no or exactly one parent set.
In addition to that, a simple hierarchy has no loops and no cycles.

* simple hierarchy => simple setup

**CLARIFICATION**
A setup (i.e. a set of sets) is said to be **a strict hierarchy**,
if the following requirements are met:

1. The setup is a strict setup.
2. The setup does not contain the empty set.
3. The setup has no more than one root set.

Note that a strict hierarchy is also a simple hierarchy. In contrary to that,
a simple hierarchy is not necessarily also a strict hierarchy.

* strict hierarchy => strict setup, simple hierarchy

**CLARIFICATION**
The union of one or more simple hierarchies is said to be
**a forest of simple hierarchies**, or a "simple forest of hierarchies".

Note that a simple hierarchy is therefore also a simple forest.

**CLARIFICATION**
The union of one or more strict hierarchies is said to be
**a forest of strict hierarchies**, or a "strict forest of hierarchies".

Note that a forest of strict hierarchies is also a forest of simple hierarchies.
However, if the strict forest contains even one non-strict hierarchy, then the
forest is only a non-strict/simple forest.

* strict forest => simple forest

<!-- ======================================================================= -->
## Example hierarchies

```
|-A-----| |-B-|
| |-B-| | | 1 |
| | 1 | | |---|
| |---| |
|-------|
```

* Root set A does not represent a consistent setup.
* That is, because set A is identical to its inner set B.
* Hence, root set A does not represent a set of sets, but a list of sets.
* In contrary to that, root set B represents a strict hierarchy.

```
|-C-------|   |-D-----------|
| 1 |-A-| |   | |-A-| |-B-| |
|   | 2 | |   | | 1 | | 2 | |
|   |---| |   | |---| |---| |
|---------|   |-------------|
```

* Root sets C and D represent strict hierarchies.
* Inner set A in C is a strict subset of C.
* Inner sets A and B in D are both strict subsets of D.
* The union of root sets C and D represent a forest of strict hierarchies.

<!-- ======================================================================= -->
## Identifying subset (ISS)

* `ISS(s, H) := s - (union of all descendant sets of s)`
* `s in H`, where `H` is a simple or strict hierarchy

```
Hierarchy A: ISS(A,A)={}, ISS(B,A)={1}
Hierarchy B: ISS(B,B)={1}, ISS(A,B)={2}
Hierarchy C: ISS(C,C)={}, ISS(A,C)={1}, ISS(B,C)={2}
```

Note that the identifying subset of a set, taken from a strict hierarchy,
is mpty, if the corresponding set is the union of its descendant sets (e.g.
`ISS(C,C)`). That is, a strict hierarchy does not guarantee that all its
inner identifying subsets are non-empty.

**CLARIFICATION**
The identifying subset `ISS(s,H)` of set `s`, which is taken from a simple or
strict hierarchy `H`, is a potentially empty subset of `s`, such that none of
the elements in `ISS(s,H)` is also an element of any of the descendants of `s`.

In addition to that, `s` is the parent set of `ISS(s,H)`. Put differently,
`s` is the least significant set in `H` that still contains all the elements
in `ISS(s,H)`.

**CLARIFICATION**
Given a non-empty identifying subset ISS and the corresponding hierarchy of
sets H, the parent set of ISS in H can be uniquely identified. Hence the name.

1. Determine all the sets in H that contain ISS as a subset.
2. Determine the least significant set of those sets.

**CLARIFICATION**
In order to guarantee that each identifying subset within a hierarchy is
non-empty, every set within a hierarchy must have one or more elements that
none of its descendant sets have.
