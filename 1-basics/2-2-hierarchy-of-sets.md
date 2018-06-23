
<!-- ======================================================================= -->
# Subsets of elements

subset-of

* `(V subset-of W), (V simple-subset-of W) := (v in W) for any (v in V)`
* `(V subset-of W) and (W subset-of V)` is true iif `(V = W)`
* The empty set `{}` is a subset to any set (including itself).
* Any set, including the empty set `{}`, is a subset to itself.

strict-subset-of

* `(V strict-subset-of W) := (V subset-of W) and (V != W)`
* `(V strict-subset-of W) and (W strict-subset-of V)` is always false
* The empty set `{}` is a strict subset to any non-empty set.
* No set, including the empty set, is a strict subset to itself.

```
multiset-of-sets = <
  A: { 1, 2 },
  B: { 1, {2} },
  C: { 2 },
  D: { 2, 3 },      
  E: { 3, 4 }
>
```

* 2 is a common element of sets A, C and D.
* 2 is not a common element of sets A, B and D.
* Sets A and E have no common element.
* Set C is a (strict) subset of A, but A is not a subset of C.
* Set A does not contain set C as an element, set B however does.
* Set A is not a subset of D, and D not a subset of A.

**CLARIFICATION**
Set A and D share the **common element** 2.

In general, two or more sets have one or more elements in common,
if the intersection of all sets is non-empty.

Note that a common element has to be an element of all the sets involved.

**CLARIFICATION**
Set A is **disjoint** from set E
because both sets have no elements in common.

In general, two or more sets are disjoint from one another,
if the intersection of all sets is empty.

Note that the empty `{}` set is disjoint from any set (including itself).
In contrary to that, no non-empty set is disjoint from itself.

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
* synonymous - an element of

Note that A can be said to contain itself.
In contrary to that, A neither contains D nor E.

**CLARIFICATION**
Set C is said to be **(loosely) embedded** into set A
because C is a strict subset of A.

Note that similar as before, the "loose" definition is with regards to C
being a subset of A and A having one or more additional elements. In contrary
to that, the "strict" counterpart would be if set C would be an element of A
in addition to A having one or more additional elements.

* C is (loosely) embedded into A - i.e. C has no borders within A.
* C is strictly embedded into B - i.e. C has borders within B.

Note that A can not be said to be embedded into itself.
That is, A is neither loosely nor strictly embedded into itself.

**CLARIFICATION**
"(strictly/loosely) contains" vs. "(strictly/loosely) embedded into":

* contains - i.e. (simple) subset
* embedded - i.e. strict subset
* embedded => contains
* if "embedded", then also "contains", but not vice versa
* loosely contains/embedded - i.e. resolved/merged into
* strictly contains/embedded - i.e. an element of

Note that the "contains" vs. "embedded" distinction is used to clarify whether
or not an outer set is known to have more elements than an inner set.

Note that the "loosely" vs. "strictly" distinction could be used to clarify how
content was injected into some other content.

**CLARIFICATION**
Set D is said to **overlap** set A
because both sets have one or more elements in common,
and because both have elements which the other set does not have.

Note that set A also overlaps set D.
Both sets can therefore be said to overlap each other.

Note that none of the two sets is a subset of the other.

<!-- ======================================================================= -->
## Visual representations

```
multiset-of-sets = <
  A: { 1, 2, 3, 4, 5 },
  B: { 2 },
  C: { 3 },
  D: { 3 }
>
```

This multiset-of-sets could be visualized using the following
box/border-based representation:

```
|-A-----------------|
| 1 |-B-| |-C,D-| 4 |
|   | 2 | |  3  |   |
|   |---| |-----|   |
|-------------------|
```

Note that the following fragments are equivalent:

```
|-C,D-|       |-C-----|      |-D-----|       |-D,C-|
|  3  |  <=>  | |-D-| |  <=> | |-C-| |  <=>  |  3  |
|-----|       | | 3 | |      | | 3 | |       |-----|
              | |---| |      | |---| |
              |-------|      |-------|
```

Sets C and D are therefore identical. Consequently, there is also no
distinct order that could be derived based on `subset-of` operator.

<!-- ======================================================================= -->
## Consistent setup

```
|-A---------------------| |-E-|
| |-B-----|   |-C-----| | | 7 |
| | 1   2 |   | 3     | | |---|
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
* Sets A and B both contain set D.
* Set D is embedded into sets A and B.
* Set B is disjoint from set C.

**CLARIFICATION**
If set D is a subset of set B, set F a subset of set C, and if sets B and C
are disjoint from one another, then both subsets (D and F) are also disjoint
from one another.

In general, any two subsets of two disjoint sets
are also disjoint from one another.

**CLARIFICATION**
A set of sets is said to be **a setup**.

Note that the above example is a setup. The example would however no longer be
a setup, if number 3 would be removed from sets A and C. That is, because this
example would then turn into a multiset of sets (i.e. sets C and F would then
be identical).

**CLARIFICATION**
A setup is said to be **a consistent setup**,
if the following requirement is met:

* If two distinct sets have one or more elements in common,
  then one set is a subset of the other.

Note that this characteristic is understood as
"consistent with regards to the `subset-of` operator".

Note that an empty setup (i.e. an empty set of sets) is considered to be 
consistent. That is, because it does not contain two distinct sets that could
be in conflict with the above requirement. Likewise, a setup that contains one
set only, is also considered to be consistent.

Note that, a consistent setup, that contains the empty set as an element,
is still consistent. That is, because the above requirement only needs to be
satisfied by sets that are not disjoint from one another. The empty set is
however disjoint to any set, and as such not required to be a subset of the
other set (even though the empty set is also a subset to any set). It can
therefore not be stated that "two sets within a consistent setup are either
disjoint, ex-or one set is a subset of the other", because the empty set
always fulfills both aspects at the same time (i.e. a singularity).

Note that, because a consistent setup is still a set of sets, each set in such
a setup is unique. Because of that, and if two distinct sets in a consistent
setup have one or more elements in common, then one set is a subset of the
other, and (in addition to that) the other set has at least one element which
the other set does not have. Consequently, a consistent setup is automatically
also consistent with regards to the `strict-subset-of` operator.

Note that this kind of consistency does not require that for each set (S1)
another set (S2) exists with which the first set (S1) has any elements in
common (e.g. set E, the empty set).

<!-- ======================================================================= -->
## Inconsistent setup

```
|-A-----------------|
| |-B---|   |-C---| |
| | 1 2 |   | 3   | |
| | |-D-|---|---| | |
| | | 4 | 5 | 6 | | |
| | |---|---|---| | |
| |-----|   |-----| |
|-------------------|
```

Note the crossing borders of sets B and D.

* Sets B and D both contain 4.
* Set D contains 5 and 6, both of which do not belong to set B.
* Set D is not a subset of set B.
* Set B contains 1 and 2, both of which do not belong to set D.
* Set B is also not a subset of set D.
* Sets B and D overlap each other.
* The borders of B and D cross each other.

Note the similar inconsistency between sets C and D.

**Memory hook**
In a consistent setup, borders do not cross each other.

<!-- ======================================================================= -->
## derived statements

```
|-A---------------------| |-E-|
| |-B-----|   |-C-----| | | 7 |
| | 1   2 |   | 3     | | |---|
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

With regards to a consistent setup, the following references may be used:

* All (strict) subsets of a set
  are said to be the set's **(strict) inner** sets.
* All sets to which a set is an (strict) inner set
  are said to be the set's **(strict) outer** sets.

Because any set is a subset to itself, any set can be understood to be an
inner and an outer set to itself (loops). In contrary to that no set is a
strict subset and therefore neither a strict inner, nor a strict outer set
to itself (no loops).

Note that two sets, which are disjoint from each other, are not understood
to be outside of each other, not even if both sets have the same parent set
(siblings). That is, "outside" and "not inside" are not equivalent.

* Any strict outer set of set S is an **ancestor set**
  and as such **super-ordinate** to, or **more significant** than S.
* Any strict inner set of set S is a **descendant set**
  and as such **sub-ordinate** to, or **less significant** than S.

Note that no set is understood to be an ancestor
and/or a descendant set to itself (no loops).

Note that the empty set is a strict subset to any non-empty set. And, because
of that, any non-empty set is an ancestor to the empty set. The empty set is
therefore the only set possible that may have ancestors that are disjoint from
one another. Consequently, a hierarchy (see below) must not contain the empty
set. From this point on, all sets are assumed to be non-empty.

* A set, that has no ancestor set,
  is said to be a **root set**.
* The least significant ancestor set of set S
  is said to be the **parent set** of S.
* Set S1 is said to be one of the **child sets**
  of set S2, if S2 is the parent set of S1.
* Two sets that have the same parent set
  are said to be **siblings** to each other.

Note that none of the ancestors of a descendant set are disjoint from one
another. They always have at least all the elements of the descendant set in
common. Consequently, a consistent setup of non-empty sets (i.e. no crossing
borders) does not allow its sets to have more than one parent set. That is,
all sets that have one or more ancestors always have exactly one least
significant ancestor and therefore exactly one parent set.

Note that a set is not a parent set to itself (no loops). That is, because
a set is not understood to be an ancestor to itself. Consequently, each set
either has no parent set (e.g. a root set), ex-or exactly one parent set.

Note that a set can not be an ancestor set to itself (no cycles). Likewise,
a set can not be a descendant set to itself. That is, because a set can not
be a subset to one of its distinct inner sets. These inner sets always have
less elements than their ancestor sets.

Note that a non-empty consistent setup of non-empty sets always has one or more
root sets. That is, because (1) a setup that only contains a single non-empty
set has that set as a root set. In such a case, the setup does not have a set
which could be an ancestor to that one set. Finally, (2) the addition of a
non-empty set to a consistent setup of non-empty sets, in such a way that the
setup remains to be consistent, will either add a new root set, or a descendant
set (i.e. a non-root set) to an existing set.

<!-- ======================================================================= -->
## Hierarchies and forests

```
|-A-------|   |-B-----------|
| 1 |-A-| |   | |-A-| |-B-| |
|   | 2 | |   | | 1 | | 2 | |
|   |---| |   | |---| |---| |
|---------|   |-------------|
```

* Root sets A and B represent hierarchies.
* Inner set A/A is a strict subset of root set A.
* Inner sets B/A and B/B are both strict subsets of root set B.
* The union of all the sets represent a forest.

**CLARIFICATION**
A multiset (of sets) is said to be **a hierarchy (of sets)**,
if the following requirements are met:

1. The multiset must be a non-empty consistent setup.
2. The setup does not contain the empty set.
3. The setup has no more than one root set.

Notes on hierarchies

* A hierarchy always has a root set, but never more than one.
* A hierarchy has no loops and no cycles.
* No two sets within a hierarchy overlaps another set.
* Each set either has no, ex-or exactly one parent set.
* Each set has a distinct rooted path (i.e. root/to/set).
* Two sets are either disjoint, ex-or one set is a subset of the other.
* Ancestor sets have more elements than their descendant sets.

**CLARIFICATION**
A set of hierarchies is said to be **a forest (of hierarchies)**.

Note that a forest may be empty.
That is, a forest is not required to contain even one hierarchy.

Note that a hierarchy can be understood to represent
a forest which contains only one hierarchy.

Note that a set of root sets can be understood to be a forest. From a strict
perspective, the forest only contains the root sets. A less strict perspective
could also implicitly include all the subsets of these root sets.

**CLARIFICATION**
Any subset of a hierarchy is a forest of hierarchies.

Note that, under certain circumstances (i.e. the hierarchy's root set
is included), the subset will itself be a hierarchy.

**TODO** -
do the hierarchies within a forest have to be disjoint? -
disjoint ex-or sub-hierarchy?

**TODO** -
go meta with forests? -
a forest is itself a set of elements -
a hierarchy of forests? -
"an outline of an outline"? -
an unordered/ordered forest?

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
