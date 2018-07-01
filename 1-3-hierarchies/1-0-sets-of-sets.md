
<!-- ======================================================================= -->
# Sets of sets

```
multiset-of-sets = <
  A: { 1, 2, 3, 4 },
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

Sets C and D are identical, which is because there is no element that would
allow to distinguish set C from D (or vice versa). Consequently, there is
no distinct order (e.g. inside vs. outside) between those two sets.

```
|-E-----|           |-F-----|  
|   |-F-|---|       |   |-E-|---|
| 1 | 2 | 3 |  <=>  | 3 | 2 | 1 |
|   |---|---|       |   |---|---|
|-------|           |-------| 
```

Set E contains the elements 1 and 2, and set F the elements 2 and 3.
That is, E does not contain 3, and F does not contain 1.

Note that the borders of both sets cross each other.

<!-- ======================================================================= -->
## fundamental definitions

subset-of

* `(V subset-of W), (V simple-subset-of W) := (v in W) for any (v in V)`
* `(V subset-of W) and (W subset-of V)` is true iff `(V == W)`
* Any set, including the empty set `{}`, is a subset to itself.
* The empty set `{}` is a subset to any set.

strict-subset-of

* `(V strict-subset-of W) := (V subset-of W) and (V != W)`
* `(V strict-subset-of W)` can only be true if `(#V < #W)`
* `(V strict-subset-of W) and (W strict-subset-of V)` is always false
* `(V strict-subset-of W) => not (W strict-subset-of V)`
* No set, including the empty set, is a strict subset to itself.
* The empty set `{}` is a strict subset to any non-empty set.

related-to

* `(V related-to W) := (V subset-of W) or (W subset-of V)`
* `(V related-to W) <=> (W related-to V)`

strictly-related-to

* `(V strictly-related-to W) := (V related-to W) and (V != W)`
* `(V strictly-related-to W) <=> (W strictly-related-to V)`
* `(V strictly-related-to W) => (V related-to W)`

unrelated-to

* `(V unrelated-to W) := not (V related-to W)`
* `(V unrelated-to W) <=> (W unrelated-to V)`

Note that the empty set `{}` has no element that could be in conflict with the
requirement of the `subset-of` definition. Because of that, "any element in the
subset is an element of the super-set" is understood to be true if the subset
is the empty set. That is, because the definition of the `subset-of` operator
merely states that, for `(V subset-of W)` to be true, any element in `V` must
also be an element of set `W`. Obviously, there is no element in the empty set
which could be in conflict with that requirement.

<!-- ======================================================================= -->
## fundamental definitions

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
Sets A and D share the **common element** 2.

* `(V coupled-with W) := ((V & W) != {})`
* `(V coupled-with W) <=> (W coupled-with V)`

Note that two or more sets have one or more elements in common, if the
intersection of all sets involved is non-empty. That is, an element which
is common to two or more sets must be an element of all those sets.

* `(V related-to W) <=!=> (V coupled-with W)`

It is important to note that, due to the empty set `{}`, two related sets are
not necessarily coupled with each other. That is, because the empty set is a
subset to any set.

Note that common elements can be understood to act as a "link" between the
sets involved. These kind of links can be understood to connect such sets with
each other, which is why those sets can be said to be "connected" or "coupled".

**CLARIFICATION**
Set A is **disjoint** from set E
because both sets have no elements in common.

* `(V disjoint-to W) := ((V & W) == {})`
* `(V disjoint-to W) <=> not (V coupled-with W)`

Note that two or more sets are disjoint from one another,
if the intersection of all sets is empty.

* `(V related-to W) => (V coupled-with W) or (V disjoint-to W)`
* `not (V related-to W) => (V coupled-with W) or (V disjoint-to W)`

Note that the empty `{}` set is disjoint to any set (including itself).
In contrary to that, no non-empty set is disjoint to itself.

**CLARIFICATION**
Set D is said to **overlap** set A
because both sets have one or more elements in common,
and because both have elements the other set does not have.

* `common := (A & D)` (e.g. `{2}`)
* `diffAD := (A - D)` (e.g. `{1}`)
* `diffDA := (D - A)` (e.g. `{3}`)
* `overlap(A,D) := (#common > 0) and (#diffAD > 0) and (#diffDA > 0)`

in general

* `(V overlaps W) := (V coupled-with W) and (V unrelated-to W)`
* `(V overlaps W) <=> (W overlaps V)`

Note that, if set V overlaps W, then W also overlaps V.
Both sets can be said to overlap each other.

Note that none of two overlapping sets is a subset of the other.

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
## TODOs

**TODO** -
a node loosely contains a distant descendant -
a node strictly contains a child -
a set loosely contains a child set -
a set strictly contains a distant set -
both notions are "inverse" to each other -
needs to be fixed before we focus on content injection
