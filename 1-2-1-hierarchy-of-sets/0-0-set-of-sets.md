
<!-- ======================================================================= -->
# Set of sets

* (/see/ relationships between sets /)

```
multiset-of-sets = <
  A: { 1, 2, 3, 4 },
  B: { 2 },
  C: { 3 },
  D: { 3 }
>
```

This multiset-of-sets could be visualized using nested sets
(i.e. a box/border-based representation):

```
|-A-----------------|
| 1 |-B-| |-C,D-| 4 |
|   | 2 | |  3  |   |
|   |---| |-----|   |
|-------------------|
```

Note that sets A and B are distinct. They differ in size and in the elements
they contain. Likewise, sets B and C are distinct. Even though both sets have
the same amount of elements, both sets differ in the element(s) they contain.

Note that the following representations are equivalent:

```
|-C,D-|       |-C-----|      |-D-----|       |-D,C-|
|  3  |  <=>  | |-D-| |  <=> | |-C-| |  <=>  |  3  |
|-----|       | | 3 | |      | | 3 | |       |-----|
              | |---| |      | |---| |
              |-------|      |-------|
```

Sets C and D are equivalent because there is no element that would allow
to distinguish both sets from one another. Because of that, there is **no
distinct order** (i.e. inside vs. outside) between the two.

Note that, in order to avoid these kind of circumstances, each set needs to
have elements which allow to **distinguish** a set from all the other sets.
That is, **sets must be distinct**, which is why a set of sets would be
required (instead of a multiset of sets).

```
|-E-----|           |-F-----|  
|   |-F-|---|       |   |-E-|---|
| 1 | 2 | 3 |  <=>  | 3 | 2 | 1 |
|   |---|---|       |   |---|---|
|-------|           |-------| 
```

Set E contains elements 1 and 2, and set F elements 2 and 3. That is, both sets
contain 2, but E does not contain 3 and F does not contain 1. As before, there
is no distinct order (i.e. inside vs. outside) between those two sets.

Note that sets E and F are said to **overlap** each other, which is visible via
the **crossing borders**. That is, both sets have elements in common (they would
otherwise be disjoint) and elements that the other set does not have (one set
would otherwise be a subset of the other). As such, overlapping sets represent
a third type of relationship between sets.

Note that, even though A is distinct from B, and that B distinct is from C,
the borders of those sets do not cross each other.

<!-- ======================================================================= -->
## E(), set-of-elements

**CLARIFICATION**
The **set of elements** `E(S)` is
the union of all the sets in a set/multiset of sets `S`.

* `E(S)` := "the union of all sets (s in S)"
* `E(S) := { e | (e in s) and (s in S) }`

Note that `E(S)` is empty if `S` is itself empty,
or if `S` contains no other set than the empty set `{}`.

<!-- ======================================================================= -->
## subset, strict subset

subset-of

* `(V subset-of W), (V simple-subset-of W) := (v in W) for any (v in V)`
* Any set, including the empty set `{}`, is a subset to itself.
* The empty set `{}` is a subset to any set.
* `(V subset-of W) -> (#V <= #W)`

strict-subset-of

* `(V strict-subset-of W) := (V subset-of W) and (V != W)`
* No set, including the empty set, is a strict subset to itself.
* The empty set `{}` is a strict subset to any non-empty set.
* `(V strict-subset-of W) -> (#V < #W)`

<!-- ======================================================================= -->
## related, strictly related

related-to

* `(V related-to W) := (V subset-of W) or (W subset-of V)`
* `(V related-to W) <-> (W related-to V)`

strictly-related-to

* `(V strictly-related-to W) := (V related-to W) and (V != W)`
* `(V strictly-related-to W) <-> (W strictly-related-to V)`
* `(V strictly-related-to W) -> (V related-to W)`
* `(V strictly-related-to W) := (V strict-subset-of W) xor (W strict-subset-of V)`

unrelated-to

* `(V unrelated-to W) := not (V related-to W)`
* `(V unrelated-to W) <-> (W unrelated-to V)`

Note that the definition of the "(un-|strictly-)related-to" terms is intended
to shift ones focus away from the elements the sets contain. That is, the focus
is shifted towards the relationships the sets have with each other.

<!-- ======================================================================= -->
## disjoint, coupled, overlap

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
* Set A does not contain set C (as an element), set B however does.
* Set A is not a subset of D, and D is not a subset of A.

**CLARIFICATION**
Set A is **disjoint** to/from set E
because both sets have no elements in common.

* `(V disjoint-to W) := ((V & W) == {})`
* `(V disjoint-to W) <-> (W disjoint-to V)`

Note that any two subsets of two disjoint sets are also disjoint from one
another. That is because otherwise, both subsets would not be subsets to
their respective super-sets.

**CLARIFICATION**
Set A is **coupled** with set D
because both sets have the common element 2.

* `(V coupled-with W) := ((V & W) != {})`
* `(V coupled-with W) <-> (W coupled-with V)`
* `(V coupled-with W) <-> not (V disjoint-to W)`
* `(V coupled-with W) -> ((V != {}) and (W != {}))`

Note that `disjoint-to` and `coupled-with` are exclusive.
That is, two sets are either disjoint ex-or coupled with each other.

* `(disjoint <-> !coupled) <-> (disjoint ex-or coupled)`
* `( (V coupled-with W) or (V disjoint-to W) )` is always true

Note that common elements can be understood to act as a "link" between the
sets involved. These links can be understood to bind sets together, which
is why those sets can be said to be "connected" or "coupled" with each other
via some "point of contact".

**CLARIFICATION**
Set D is said to **overlap** set A
because both sets are coupled with each other,
and because both sets contain elements that the other set does not have.

* `common := (A & D)` (e.g. `{2}`)
* `diffAD := (A - D)` (e.g. `{1}`)
* `diffDA := (D - A)` (e.g. `{3}`)
* `overlap(A,D) := (#common > 0) and (#diffAD > 0) and (#diffDA > 0)`

Generalized definition:

* `(V overlaps W) := (V coupled-with W) and (V unrelated-to W)`
* `(V overlaps W) <=> (W overlaps V)`

Note that, if set V overlaps W, then W also overlaps V.
Both sets can be said to overlap each other.

Note that none of two overlapping sets is a subset of the other.
Both sets are therefore unrelated to each other.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The empty set is disjoint and related to any set, but not distinct to itself.
A non-empty set is coupled with and related to itself. Two distinct non-empty
sets may be coupled. Two distinct non-empty and coupled sets are not necessarily
related.

```
     \ set-2 |          |          |
set-1 \      | E        | A        | B
-----------------------------------------------------
 E           | !C and R | !C and R | !C and R
-----------------------------------------------------
 A           | !C and R | C and R  | !C or (!R or R)
```

* `E` is the empty set `{}`
* `A` and `B` are non-empty sets - i.e. `(A,B != E)`
* `A` and `B` are distinct - i.e. `(A != B)`
* two sets are coupled (`C`) or disjoint (`!C`)
* two sets are related (`R`) or unrelated (`!R`)

**CLARIFICATION**
Two disjoint sets are not necessarily distinct.
Likewise, two distinct sets are not necessarily disjoint.

* `disjoint <=!=> distinct`
* (=!>) `{}` is disjoint to any set, but not distinct to itself.
* (<!=) both sets may overlap each other.
* (<!=) both sets may be strictly related.

**CLARIFICATION**
Two disjoint sets are not necessarily unrelated.
Likewise, two unrelated sets are not necessarily disjoint.

* `disjoint <=!=> unrelated`
* (=!>) `{}` is disjoint and related to any set.
* (<!=) both sets may overlap each other.

**CLARIFICATION**
Two coupled sets are not necessarily related.
Likewise, two related sets are not necessarily coupled.

* `coupled <=!=> related`
* (=!>) both sets may overlap each other.
* (<!=) `{}` is disjoint and related to any set.
* hint: `(a <-> b) <-> (!a <-> !b)`
