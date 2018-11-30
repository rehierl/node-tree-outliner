
<!-- ======================================================================= -->
# Set of sets

* (/see/ "relationships between sets" in "mathematics" /)

<!-- ======================================================================= -->
## relationships

```
multiset-of-sets = <
  A: { 1, 2, 3, 4 },
  B: { 2 },
  C: { 3 },
  D: { 3 }
>
```

This multiset-of-sets can be visualized as nested sets
(i.e. a box/border-based representation):

Note that the term "nested set" in general refers to a set that has another
set as an element. Obviously, the focus here is on a set that has another
set as subset (i.e. "subset-of" vs. "element-of").

```
|-A-----------------|
| 1 |-B-| |-C,D-| 4 |
|   | 2 | |  3  |   |
|   |---| |-----|   |
|-------------------|
```

Every element in B is also an element in A, but not every element in A is
also an element in B (i.e. related). Sets A and B are therefore distinct. In
contrary to that, sets B and C are distinct since both sets have no element
in common (i.e. disjoint).

Note that even though A is distinct to B, and B is distinct to C, the borders
of both sets do not cross each other. That is, the borders of B and C are both
inside of A and outside of each other.

Sets C and D are equal because there is no element that allows to distinguish
both sets from one another. Because of that, there is no **distinct order**
(i.e. inside vs. outside, i.e. subset vs. superset) between the two. The
following representations are therefore equivalent:

```
|-C,D-|       |-C-----|      |-D-----|       |-D,C-|
|  3  |  <=>  | |-D-| |  <=> | |-C-| |  <=>  |  3  |
|-----|       | | 3 | |      | | 3 | |       |-----|
              | |---| |      | |---| |
              |-------|      |-------|
```

In order to avoid this kind of circumstances, each set needs to have
elements that allow to distinguish a set from any other set. That is,
sets **must be distinct** from one another, which is why a set-of-sets
rather than a multiset-of-sets, is required.

```
|-E-----|           |-F-----|  
|   |-F-|---|       |   |-E-|---|
| 1 | 2 | 3 |  <=>  | 3 | 2 | 1 |
|   |---|---|       |   |---|---|
|-------|           |-------| 
```

Set E contains elements 1 and 2, and set F elements 2 and 3. That is, both
sets contain element 2, but E does not contain 3 and F does not contain 1.
As before, there is no distinct order between both sets since both are
neither disjoint nor (properly) related.

Note that sets E and F are said to **overlap** each other, which is visible
due to the **crossing borders**. That is, both sets have elements in common
(they would otherwise be disjoint) and elements that the other set does not
have (they would otherwise be related). As such, overlapping sets represent
another type of relationship between two sets.

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
* Sets A and E have no common element, they are disjoint.
* Likewise, sets B and D have no element in common.
* Set C is a (strict) subset of A, but A is not a subset of C.
* Set A does not contain set C (as an element), set B however does.
* Set A is not a subset of D, and D is not a subset of A.
* Sets A and D overlap each other.

**CLARIFICATION**
Set A is **disjoint to** set E
since both sets have no element in common.

* `(V disjoint-to W) := ((V & W) == Ø)`
* `(V disjoint-to W) <-> (W disjoint-to V)`

Note that the empty set `Ø` is the only set that is disjoint to itself.
In contrary to that, any non-empty set is coupled with itself.

Note that two non-empty subsets of two disjoint sets are disjoint from one
another. That is because otherwise both subsets could not be subsets of
their respective supersets.

**CLARIFICATION**
Set A is **coupled with** set D
since both sets have element 2 in common.

* `(V coupled-with W) := ((V & W) != Ø)`
* `(V coupled-with W) <-> (W coupled-with V)`
* `(V coupled-with W) <-> not (V disjoint-to W)`
* `(V coupled-with W) -> ((V != Ø) and (W != Ø))`

Note that `disjoint-to` and `coupled-with` are exclusive to each other.
That is, two sets are either disjoint ex-or coupled with each other.
Because of that, "disjoint-to" is converse/antonymous to "coupled-with".

* `(V disjoint-to W) ex-or (V coupled-with W)` is true
* `(disjoint ex-or coupled) <=> (disjoint <-> not-coupled)`

Note that the empty set `Ø` is the only set that is not coupled with
itself. In contrary to that, any non-empty set is coupled with itself.

Note that common elements can be understood to act as a "link" between two
sets. These links can be understood to bind both sets together, which is
why those sets can be said to be "connected" or "coupled" with each other
via some "point of contact".

**CLARIFICATION**
Set D **overlaps** set A
since both sets are coupled with each other,
and since each set has an element that the other set does not have.

* `(V overlaps W) := (I != Ø) and (I != V) and (I != W)` where `I := (V & W)`
* `(V overlaps W) := ((V & W) != Ø) and ((V \ W) != Ø) and ((W \ V) != Ø)`
* e.g. `(A overlaps D) == [ ({2} != Ø) and ({1} != Ø) and ({3} != Ø) ]`
* `(V overlaps W) := (V coupled-with W) and (V unrelated-to W)`
* `(V overlaps W) <-> (W overlaps V)`

Note that a set, which overlaps another set, is not a subset of the other.
Overlapping sets are therefore always unrelated to each other.

<!-- ======================================================================= -->
## (simple/strict/proper) subset

**CLARIFICATION**
Set V is a **(simple) subset of** set W,
if all elements in V are also elements in W.

* `(V subset-of W) := (v in W) for any (v in V)`
* `(V subset-of W) -> (#V <= #W)`

**CLARIFICATION**
Set V is a **strict/proper subset of** set W,
if V is a subset of W, and if W is no subset of V.

* `(V strict-subset-of W) := (V subset-of W) and (W no-subset-of V)`
* `(V strict-subset-of W) := (V subset-of W) and (V != W)`
* `(V strict-subset-of W) -> (#V < #W)`

Note that any set (including `Ø`) is a subset to itself.
However, no set (including `Ø`) is a strict subset to itself.

Note that the empty set `Ø` is a subset to any (non-empty) set.
In contrary to that, no non-empty set is a subset of the empty set.

Note that the empty set `Ø` is a strict subset to any non-empty set.
In contrary to that, no non-empty set is a strict subset of the empty set.

<!-- ======================================================================= -->
## related, strictly/properly related

**CLARIFICATION**
Set V is **related to** set W,
if one set is a (simple) subset of the other.

* `(V related-to W) := (V subset-of W) or (W subset-of V)`
* `(V related-to W) <-> (W related-to V)`

**CLARIFICATION**
Set V is **unrelated to** set W,
if none is a subset of the other.

* `(V unrelated-to W) := not (V related-to W)`
* `(V unrelated-to W) <-> (W unrelated-to V)`
* synonymous - "unrelated-to", "not-related-to"

Note that unrelated sets may or may not be coupled with each other.

**CLARIFICATION**
Set V is **strictly/properly related to** set W, if both sets are related
and distinct to each other. Put differently, one (and only one) set must
be a subset of the other.

* `(V strictly-related-to W) := (V subset-of W) ex-or (W subset-of V)`
* `(V strictly-related-to W) := (V related-to W) and (V != W)`
* `(V strictly-related-to W) <-> (W strictly-related-to V)`

Note that the definition of the "related-to" terms is intended to shift
ones focus away from the elements the sets contain. That is, the focus
is shifted towards the relationship between two sets.

<!-- ======================================================================= -->
## remarks

* The empty set is disjoint and related to any set.
* A non-empty set is coupled with and related to itself.
* Two distinct coupled sets may still overlap each other.

```
     \ set-2 |          |          |
set-1 \      | E        | A        | B
-----------------------------------------------------
 E           | !C and R | !C and R | !C and R
-----------------------------------------------------
 A           | !C and R | C and R  | !C or (!R or R)
```

* `E` represents the empty set `Ø`
* `A` and `B` represent distinct non-empty sets - i.e. `(A,B != E)`
* two sets are coupled (`C`) or disjoint (`!C`)
* two sets are related (`R`) or unrelated (`!R`)

**CLARIFICATION**
Two disjoint sets are not necessarily distinct.
Likewise, two distinct sets are not necessarily disjoint.

* `disjoint <=!=> distinct`
* (=!>) `Ø` is disjoint to any set, but not distinct to itself
* (<!=) both sets may be related to each other

**CLARIFICATION**
Two disjoint sets are not necessarily unrelated.
Likewise, two unrelated sets are not necessarily disjoint.

* `disjoint <=!=> unrelated`
* (=!>) `Ø` is disjoint and related to any set
* (<!=) both sets may overlap each other

**CLARIFICATION**
Two coupled sets are not necessarily related.
Likewise, two related sets are not necessarily coupled with each other.

* `coupled <=!=> related`
* (=!>) both sets may overlap each other
* (<!=) `Ø` is disjoint and related to any set
* hint: `(a <-> b) <-> (!a <-> !b)`

Note that the attempt to support the empty set `Ø` as an element in a set of
sets, will add additional difficulty when classifying the relationship between
two sets. That is due to its unique characteristics.
