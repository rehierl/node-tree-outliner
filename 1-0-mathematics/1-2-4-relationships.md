
<!-- ======================================================================= -->
# Relationships between sets

<!-- ======================================================================= -->
## overview

```
         |--> disjoint    |--> equal
(A ? B) -|                |
         |--> intersects -|--> proper subset
              (coupled)   |
                          |--> overlap
```

(A equal-to B)

* `(A == B) := ((A union B) == (A isect B))`
* i.e. all elements are common to both
* i.e. `A` and `B` are equal to each other
* i.e. `equal-to` has no orientation
* `(A == B) <-> (A subset-of B) and (B subset-of A)`
* i.e. `A ` and `B` are subsets to each other

(A unequal-to B)

* `(A != B) := not (A == B)`
* i.e. `unequal-to` is converse to `equal-to`
* synonymous - `distinct-to`, `distinct-form`

(A disjoint-to B)

* `(A disjoint-to B) := ((A & B) == {})`
* i.e. `A` and `B` have no elements in common
* i.e. `A` and `B` are disjoint to each other
* i.e. `disjoint-to` has no orientation

(A intersects B)

* `(A intersects B) := ((A & B) != {})`
* i.e. `A` and `B` have some elements in common
* i.e. `intersects` is converse to `disjoint-to`
* i.e. `A` and `B` intersect each other
* i.e. `intersects` has no orientation
* synonymous - `coupled-with` (via some point of contact)

(A subset-of B)

* `(A subset-of B) := ((A & B) == A)`
* i.e. all elements in `A` are elements in `B`
* i.e. `subset-of` has "some" orientation
* note - `({} subset-of {})`, `(A subset-of A)`
* `(A subset-of B) -> (#A <= #B)`

(A contains B)

* `(A contains B) := (B subset-of A)`
* note - `(B in A)` := `A` contains `B` as an element
* note - "element-of" vs. "subset-of"
* synonymous - `subset-of`, `inside-of`

(A related-to B)

* `(A related-to B) := (A subset-of B) or (B subset-of A)`
* i.e. one set is a subset of the other
* i.e. `related-to` has no orientation

(A unrelated-to B)

* `(A unrelated-to B) := not (A related-to B)`
* i.e. `unrelated-to` is converse to `related-to`

(A strict-subset-of B)

* `(A strict-subset-of B) := (A subset-of B) and (A != B)`
* i.e. `A` is distinct from, but still a subset-of `B`
* `(A strict-subset-of B) -> (B strict-superset-of A)`
* i.e. `B` has one or more elements not in `A`
* `(A strict-subset-of B) -> (B no-strict-subset-of A)`
* i.e. `strict-subset-of` is strictly oriented
* `(A strict-subset-of B) -> (#A < #B)`
* synonymous - `proper-subset-of`

(A strictly-related-to B)

* `(A strictly-related-to B) := (A related-to B) and (A != B)`
* i.e. `A` is distinct from, but still related to `B`
* i.e. both are unequal and one is a subset of the other
* i.e. `strictly-related` has no orientation
* synonymous - `properly-related-to`

(A overlaps B)

* `(A overlaps B) := (A intersects B) and (A unrelated-to B)`
* i.e. `((A & B) != {}) and ((A & B) != A) and ((A & B) != B)`
* i.e. each set has an element not in the other
* i.e. `overlaps` has no orientation

<!-- ======================================================================= -->
## remarks

Note that the `strict-subset-of` operator is the only set-related operator
that is strictly/properly oriented.

Note that `disjoint-to` and `subset-of` have strict definitions. That is, a set
either contains all elements of the other (i.e. subset-of), or none at all (i.e.
disjoint). In contrary to that, `overlaps` merely states that one set must have
one or more, but not all elements of the other. As such, the `overlaps` operator
is rather imprecise (i.e. how many elements exactly?).

Note that two distinct sets which do not overlap each other, are either
strictly related ex-or disjoint. As such, this either-or relationship
is fundamental to partial orders and node trees.

<!-- ======================================================================= -->
## remarks

Any two sets in a multiset of sets are:
(1) equal, (2) disjoint, (3) related, or (4) overlap each other.

```
|-A-----|
|   |-B-|---|
| 1 | 2 | 3 |
|   |---|---|
|-------|
```

The possibilities for subsets 1, 2 and 3 (being empty or non-empty) in sets
A and B, and therefore the relationships between sets A and B are as follows:

```
1 is empty        | 1 is non-empty |
==================|================|===
1: 000 - DI,RE,EQ |                | sets E and/or F
2: 001 - DI,RE    | 5: 100 - DI,RE | are empty
------------------|----------------|---
3: 010 - RE,EQ    | 6: 101 - DI    | neither E nor F
4: 011 - RE       | 7: 110 - RE    | is empty
                  | 8: 111 - OV    |
```

* XYZ := X represents subset 1, Y subset 2 and Z subset 3
* (X in {0,1}), where 0 := subset 1 is empty, 1 := subset 1 is non-empty
* e.g. in 001 subsets 1 and 2 are empty and subset 3 is not
* e.g. both sets are empty in case (1), only A in (2) and only B in (5)

The following types of relationships can be distinguished depending on which
subsets are empty: equal (EQ), disjoint (DI), related (RE), overlapping (OV).

Note that this listing of the different types of relationships is complete.
That is, there is no further type of relationship possible between two sets.

As mentioned above, there is no strict orientation between both sets in cases
1 and 3. In addition to that, cases 2 and 5 are ambiguous since an empty set
is disjoint and related to any set. That is, there is no clear answer as to
whether the empty set is inside or outside of a non-empty set. Furthermore,
the definition behind case 8 (i.e. overlapping) is non-trivial and does also
not include any strict orientation. Because of that, these cases will not be
taken int account, which is why the focus will only be on cases 4, 6 and 7.
That is, two distinct non-empty sets are then either disjoint ex-or (properly)
related (i.e. DI ex-or RE).
