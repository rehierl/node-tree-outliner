
<!-- ======================================================================= -->
# Relationships between sets

```
         |--> disjoint    |--> equal
(A ? B) -|                |
         |--> intersects -|--> strict subset
              (coupled)   |
                          |--> overlap
```

(A disjoint-to B)

* `(A disjoint-to B) := ((A & B) == {})`
* i.e. `A` and `B` have no elements in common
* i.e. `A` and `B` are disjoint to each other
* i.e. `disjoint-to` has no orientation
* note - `(A disjoint-to B) -> (A distinct-to B)`

(A intersects B)

* `(A intersects B) := ((A & B) != {})`
* i.e. `A` and `B` have some elements in common
* i.e. `A` and `B` intersect each other
* i.e. `intersects` has no orientation
* synonymous - `coupled-with` (via some point of contact)

(A subset-of B)

* `(A subset-of B) := ((A & B) == A)`
* i.e. `A` and `B` intersect each other
* i.e. all elements in `A` are elements in `B`
* i.e. `subset-of` has some orientation

(A contains B)

* `(A contains B) := (B subset-of A)`
* i.e. `contains` has some orientation
* note - `(B !in A)` - i.e. `A` does not contain `B` as an element
* synonymous - `inside-of`

(A related-to B)

* `(A related-to B) := (A subset-of B) or (B subset-of A)`
* i.e. one set is a subset of the other
* i.e. `related-to` has no orientation
* antonymous - `unrelated-to`

(A equal-to B)

* `(A == B) := (A subset-of B) and (B subset-of A)`
* `(A == B) := ((A isect B) == (A union B))`
* i.e. `A ` and `B` are subsets to each other
* i.e. the intersection is equal to `A` and `B`
* i.e. `equal-to` has no orientation
* antonymous - `unequal-to`, `distinct-to/from`

(A strict-subset-of B)

* `(A strict-subset-of B) := (A != B) and (A subset-of B)`
* i.e. `A` is distinct-from, but still a subset-of `B`
* `(A strict-subset-of B) -> (B strict-superset-of A)`
* i.e. `B` has one or more elements not in `A`
* `(A strict-subset-of B) -> (B !strict-subset-of A)`
* i.e. `strict-subset-of` is (strictly) oriented
* synonymous - `proper-subset-of`

(A strictly-related-to B)

* `(A strictly-related-to B) := (A != B) and (A related-to B)`
* i.e. `A` is distinct-from, but still related-to `B`
* i.e. both sets are unequal and one is a subset of the other
* i.e. `strictly-related` has no orientation

(A overlaps B)

* `(A overlaps B) := (A coupled-with B) and (A unrelated-to B)`
* i.e. `((A & B) != {}) and ((A & B) != A) and ((A & B) != B)`
* i.e. each set has an element not in the other
* `(A overlaps B) <-> (B overlaps A)`
* i.e. `overlaps` has no orientation

<!-- ======================================================================= -->
## remarks

Note that the `strict-subset-of` is the only set-related qualifier which is
(strictly) oriented/directed.

Note that `disjoint-to` and `subset-of` have strict definitions. That is, a set
either contains all elements of the other (i.e. subset-of), or none at all (i.e.
disjoint). In contrary to that, `overlaps` merely states that one set must have
one or more, but not all elements of the other. As such, the `overlaps` operator
is rather imprecise (i.e. how many exactly?).

Note that two distinct (i.e. unequal) sets that do not overlap each other, are
either strictly related ex-or disjoint. As such, this either-or relationship
is fundamental to partial orders and node trees.
