
<!-- ======================================================================= -->
# Relationships between graphs

Note that the following operators are largely equal/similar to the set-based
operators. (/see/ "relationships between sets" in "mathematics" /).

<!-- ======================================================================= -->
## overview

```
         |--> disjoint    |--> equal
(S ? G) -|                |
         |--> intersects -|--> strict sub/super-graph
              (coupled)   |
                          |--> overlap
```

* given two graphs `S := (T,U)` and `G := (V,E)`

(S equal-to G)

* `(S == G) := (T == V) and (U == E)`
* i.e. both graphs have the same set of vertices and edges
* i.e. the intersection graph is equal to `S` and `G`
* i.e. `equal-to` has no orientation
* `(S == G) <-> (S subgraph-of G) and (G subgraph-of S)`
* i.e. `S` and `G` are subgraphs to each other

(S unequal-to G)

* `(S != G) := not (S == G)`
* i.e. `unequal-to` is converse/antonymous to `equal-to`
* synonymous - `distinct-to`, `distinct-from`

(S disjoint-to G)

* `(S disjoint-to B) := (T disjoint-to V)`
* i.e. `S` and `G` have no vertices in common
* i.e. `S` and `G` are disjoint to each other
* i.e. `disjoint-to` has no orientation
* note - `(S disjoint-to G) -> (S distinct-to G)`
* note - `(T disjoint-to V) -> (U disjoint-to E)`

(S intersects G)

* `(S intersects G) := ((T & V) != {})`
* i.e. `S` and `G` have some vertices in common
* i.e. `S` and `G` intersect each other
* i.e. `intersects` has no orientation
* note - `(U intersects E) -> (T intersects V)`
* synonymous - `coupled-with` (via some point of contact)

(S subgraph-of G)

* `(S subgraph-of G) := (T subset-of V) and (U subset-of E)`
* i.e. all vertices/edges in `S` are vertices/edges in `G`
* i.e. `subgraph-of` has "some" orientation
* note - `(Ø subgraph-of Ø)`, `(G subgraph-of G)`

(S contains G)

* `(G contains S) := (S subgraph-of G)`
* i.e. `contains` has "some" orientation
* note - no issue similar to "element-of" vs. "subset-of"
* synonymous - `inside-of`

(S related-to G)

* `(S related-to G) := (S subset-of G) or (G subset-of S)`
* i.e. one graph is a subgraph of the other
* i.e. `related-to` has no orientation

(S unrelated-to G)

* `(S unrelated-to G) := not (S related-to G)`
* i.e. `unrelated-to` is converse/antonymous to `related-to`

(S proper-subgraph-of G)

* `(S proper-subgraph-of G) := (S subgraph-of G) and (S != G)`
* i.e. `S` is distinct from, but still a subgraph-of `G`
* `(S proper-subgraph-of G) -> (G proper-supergraph-of S)`
* i.e. `G` has one or more vertices not in `S`
* `(S proper-subgraph-of G) -> (G no-proper-subgraph-of S)`
* i.e. `proper-subgraph-of` has a strict/proper orientation/direction
* synonymous - `strict-subgraph-of`

(S properly-related-to G)

* `(S properly-related-to G) := (S related-to G) and (S != G)`
* i.e. `S` is distinct from, but still related to `G`
* i.e. both are unequal and one is a subgraph of the other
* i.e. `properly-related-to` has no orientation
* synonymous - `strictly-related-to`

(S overlaps G)

* `(S overlaps G) := (S intersects G) and (S unrelated-to G)`
* i.e. each graph has a vertex not in the other
* i.e. `overlaps` has no orientation

<!-- ======================================================================= -->
## remarks

Note that the `proper-subgraph-of` operator is the only graph-related operator
that has a strict/proper orientation/direction.

Note that `disjoint-to` and `subgraph-of` have strict definitions. That is, a
graph either contains all the vertices/edges of the other (i.e. subgraph-of),
or none at all (i.e. disjoint). In contrary to that, `overlaps` merely states
that one graph must have one or more, but not all the corresponding elements
of the other. As such, the `overlaps` operator is rather imprecise (i.e. how
many elements exactly?).

Note that two distinct (i.e. unequal) graphs which do not overlap each other,
are either properly related ex-or disjoint. In the context of simple sets of
elements, this either-or relationship allows to define partial orders.
