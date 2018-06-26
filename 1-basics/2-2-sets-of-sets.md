
<!-- ======================================================================= -->
## TODOs

**TODO** -
a node loosely contains a distant descendant -
a node strictly contains a child -
a set loosely contains a child set -
a set strictly contains a distant set -
both notions are "inverse" to each other -
needs to be fixed before we focus on content injection

<!-- ======================================================================= -->
# Sets of sets

subset-of

* `(V subset-of W), (V simple-subset-of W) := (v in W) for any (v in V)`
* `(V subset-of W) and (W subset-of V)` is true if `(V = W)`
* Any set, including the empty set `{}`, is a subset to itself.
* The empty set `{}` is a subset to any set.

strict-subset-of

* `(V strict-subset-of W) := (V subset-of W) and (V != W)`
* `(V strict-subset of W)` can only  be true, if `(#V < #W)`
* `(V strict-subset-of W) and (W strict-subset-of V)` is always false
* No set, including the empty set, is a strict subset to itself.
* The empty set `{}` is a strict subset to any non-empty set.

Note that, if `(V subset-of W) or (V strict-subset-of W)` is true,
then `V` may be referred to as the "subset" and `W` as the "super-set".

Note that the empty set has no element that could be in conflict with the
requirement of the `subset-of` definition. Hence, "all the elements of the
empty set are elements of the super-set" is understood to be true. That is,
because the requirement does not have a "must have an element" part.

(Don't think too much about empty sets, exclude them if possible.)

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
Both sets can be understood to be **coupled** with each other.

Note that two or more sets have one or more elements in common,
if the intersection of all sets is non-empty.

Note that a common element has to be an element of all the sets involved.

**CLARIFICATION**
Set A is **disjoint** from set E
because both sets have no elements in common.

* disjoint <=> not coupled
* coupled <=> not disjoint

Note that two or more sets are disjoint from one another,
if the intersection of all sets is empty.

Note that the empty `{}` set is disjoint from any set (including itself).
In contrary to that, no non-empty set is disjoint from itself.

**CLARIFICATION**
Set D is said to **overlap** set A
because both sets have one or more elements in common,
and because both have elements which the other set does not have.

Note that set A also overlaps set D.
Both sets can therefore be said to overlap each other.

Note that none of the two sets is a subset of the other.

**CLARIFICATION**
Set A is said to **(loosely) contain** set C
because C is a subset of A.

Note that this "contains" definition is with regards to the `subset-of` operator
and therefore needs to be understood as "contains the elements of" instead of
"contains as an element". In order to distinguish both notions, one could use
qualifiers similar to "loosely contains" (i.e. contains the elements of) and
"strictly contains" (i.e. contains as an element):

* A (loosely) contains C => C has no border in A.
* synonymous - resolved-into, merged-into
* B strictly contains C => C has a border in B.
* synonymous - an element of

Note that set A can be said to contain itself.
In contrary to that, set A neither contains D nor E.

**CLARIFICATION**
Set C is said to be **(loosely) embedded** into set A
because C is a strict subset of A.

Note that similar as before, the "loose" definition is with regards to C
being a subset of A and A having one or more additional elements. In contrary
to that, the "strict" counterpart would be if set C would be an element of A
in addition to A having one or more additional elements.

* C is (loosely) embedded into A => C has no border in A.
* C is strictly embedded into B => C has a border in B.

Note that set A can not be said to be embedded into itself.
That is, A is neither loosely nor strictly embedded into itself.

**CLARIFICATION**
"(strictly/loosely) contains" vs. "(strictly/loosely) embedded into":

* contains <=> (simple) subset
* embedded <=> strict subset
* embedded => contains
* if "embedded", then also "contains", but not necessarily vice versa
* loosely contains/embedded -> resolved/merged into
* strictly contains/embedded -> an element of

Note that the "contains" vs. "embedded" distinction is used to clarify whether
or not a super-set is known to have more elements than a sub-set.

Note that the "loosely" vs. "strictly" distinction could be used to clarify how
content was injected into some other content.

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

Note that any two subsets of two disjoint sets are also disjoint from one
another. That is because otherwise, both subsets would not be subsets to
their respective super-sets.

**CLARIFICATION**
A set of sets is said to be **a (simple) setup**.

* `S := (V,P)`.
* `V` is a set of values/elements.
* `P` is a set of subsets over `V`.

Note that `P` is a subset of `V`'s power-set (i.e. `P subset-of P(V)`).
That is, the elements in `P` are elements in `P(V)`.

Note that `V` is the union of all sets in `P` (i.e. `V` may be empty). That is,
a (simple) setup is completely specified by its set-of-sets `P`.

Note that the above example is a setup. The example would however no longer be
a setup, if number 3 would be removed from sets A and C. That is, because this
example would then turn into a multiset of sets (i.e. sets C and F would then
be identical, but distinct elements).

**CLARIFICATION**
A setup is said to be **a consistent setup**,
if the following requirement is met:

* If two distinct sets have one or more elements in common,
  then one set is a subset of the other.

Note that this characteristic is understood as
"consistent with regards to the `subset-of` operator".

Note that an empty setup (i.e. an empty set of sets) is considered to be 
consistent. That is, because it does not contain two distinct sets that
could be in conflict with the above requirement. Likewise, a setup that
contains one set only, is also considered to be consistent.

Note that, a consistent setup, which contains the empty set as an element,
is still consistent. That is, because the above requirement only needs to be
satisfied by sets that are not disjoint from one another. The empty set is
however disjoint to any set, and as such not required to be a subset of the
other set (even though the empty set is a subset to any set). It can therefore
not be stated that "two sets within a consistent setup are either disjoint,
ex-or one set is a subset of the other", because the empty set always fulfills
both aspects at the same time (i.e. a singularity).

Note that, because a consistent setup is still a set of sets, each set in such
a setup is unique. Because of that, and if two distinct sets in a consistent
setup have one or more elements in common, then one set is a subset of the
other, and (in addition to that) the super-set has at least one element which
the other set does not have. Consequently, a consistent setup is automatically
also consistent with regards to the `strict-subset-of` operator.

Note that this kind of consistency does not require that for each set (S1)
another set (S2) exists with which the first set (S1) has any elements in
common (e.g. set E, the empty set).

**CLARIFICATION**
A setup is said to be **a strict setup**,
if the following requirement is met:

* The setup is a consistent setup.
* The setup does not contain the empty set `{}`.

Note that a strict setup allows to make the following statement:

* Two distinct sets in a strict setup are either disjoint,
  ex-or one set is a strict subset of the other.

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
