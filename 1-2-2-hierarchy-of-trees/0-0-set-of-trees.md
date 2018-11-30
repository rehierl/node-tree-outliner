
<!-- ======================================================================= -->
# Set of sub-trees

* (/see/ "relationships" in "graph theory" /)
* (/see/ "set of sets" in "hierarchy of sets" /)

<!-- ======================================================================= -->
## relationships

```
multiset-of-trees = <
A: 1 , B: 4 , C: 4 , D: 2 , E: 2, F: 3
  ===    ===    ===    ===
  2 3     2      2      5
>
```

Elements B and C represent trees that are equal. The relationship between
both trees is therefore neither "disjoint" nor "properly related". Because
of that, there is no **distinct order** (i.e. inside vs. outside, i.e.
subtree vs. super-tree) between the two.

Consequently, and in order to avoid these kind of circumstances, each element
must represent a unique tree. Put differently, all trees **must be distinct**,
which is why a set-of-trees, rather than a multiset-of-trees is required.

Similar to that, there is no distinct relationship between the trees A and
B. That is because both trees have nodes in common (they would otherwise be
disjoint) and nodes the other tree does not have (they would otherwise be
related). As such, both trees **overlap** each other and therefore represent
another type of relationship between two trees.

Likewise, trees A and D overlap each other. However, the root of D is a node
in A, which is why the union of both trees is, in contrary to A and B, another
tree. As before, there is no clear relationship between trees A and D.

```
|-A-----|
| 1 |---|-B-|
|   | 2 | 4 |
| 3 |---|---|
|-------|
```

Note that the set of nodes of trees A and B overlap each other. The same applies
to trees A and D. Hence if the sets of these trees are visualized as a set of
nested sets, then the borders of those sets cross each other. Because of that,
overlapping trees may be referred to as trees that **cross each other**.

<!-- ======================================================================= -->
## disjoint, coupled, overlap

**CLARIFICATION**
Trees `S := (T,U)` and `G := (N,E)` are **disjoint** (from one another),
if the intersection graph between the two is equal to the empty graph.

* `(S disjoint-to G) := ((S & G) == Ø)`
* `(S disjoint-to G) <-> (G disjoint-to S)`

Recall that two trees, which have an edge in common, must also have both
of the endpoints of that edge in common. Hence, if the sets of nodes of
two trees are disjoint, then both trees have neither nodes nor edges in
common (i.e. both trees are disjoint).

* `(U coupled-with E) -> (T coupled-with N)`
* `(T disjoint-to N) -> (U disjoint-to E)`
* `(S disjoint-to G) <-> (T disjoint-to N)`

**CLARIFICATION**
Trees `S := (T,U)` and `G := (N,E)` are **coupled** (with each other),
if the intersection graph between the two is non-empty.

* `(S coupled-with G) := ((S & G) != Ø)`
* `(S coupled-with G) <-> (G coupled-with S)`
* `(S coupled-with G) <-> (T coupled-with N)`

Note that "disjoint-to" and "coupled-with" are exclusive to each other.
That is, two trees are either disjoint ex-or coupled with each other.
Because of that, "disjoint-to" is converse/antonymous to "coupled-with".

* `(S disjoint-to G) ex-or (S coupled-with G)` is true
* `(disjoint ex-or coupled) <=> (disjoint <-> not-coupled)`

Note that the common elements can be understood to act as a "link" between two
trees. These links can be understood to bind both trees together, which is why
those trees can be said to be "connected" or "coupled" with each other via some
"point of contact".

**CLARIFICATION**
Two trees `S := (T,U)` and `G := (N,E)` are said to **overlap** (each other),
if the intersection between the two is non-empty, and if each tree has a node
that is not a node in the other tree. Put differently, both trees must be
coupled with each other and none is a subtree of the other.

* `(S overlaps G) := (I != Ø) and (I != S) and (I != G)` where `I := (S & G)`
* `(S overlaps G) := (S coupled-with G) and (S unrelated-to G)`
* `(S overlaps G) <-> (G overlaps S)`

<!-- ======================================================================= -->
## (simple/strict/proper) subtree (of a tree)

**CLARIFICATION**
Tree `S := (T,U)` is a **(simple) subtree of** tree `G := (N,E)`,
if all the elements in `S` are also elements in `G`.

* `(S subtree-of G) := (S subgraph-of G)`
* `(S subtree-of G) -> (#T <= #V) and (#U <= #E)`
* note - `S` and `G` are both required to be trees (i.e. subtree of a tree)

**CLARIFICATION**
Tree `S := (T,U)` is a **strict/proper subtree of** tree `G := (N,E)`,
if `S` is a (simple) subtree of and unequal to `G`.

* `(S proper-subtree-of T) := (S subtree-of G) and (G no-subtree-of S)`
* `(S proper-subtree-of T) := (S subtree-of G) and (S != T)`
* `(S proper-subtree-of G) -> (#T < #N) and (#U < #E)`

<!-- ======================================================================= -->
## related, strictly/properly related

**CLARIFICATION**
Tree `S := (T,U)` is **related to** tree `G := (N,E)`,
if one tree is a (simple) subtree of the other.

* `(S related-to G) := (S subtree-of G) or (G subtree-of S)`
* `(S related-to G) <-> (G related-to S)`

**CLARIFICATION**
Tree `S := (T,U)` is **unrelated to** tree `G := (N,E)`,
if none is a (simple) subtree of the other.

* `(S unrelated-to G) := not (S related-to G)`
* `(S unrelated-to G) <-> (G unrelated-to S)`
* synonymous - "unrelated-to", "not-related-to"

Note that unrelated trees may or may not be coupled with each other.

**CLARIFICATION**
Tree `S := (T,U)` is **strictly/properly related to** tree `G := (N,E)`,
if both trees are related and distinct to each other. Put differently,
one (and only one) tree must be a subtree of the other.

* `(S strictly-related-to G) := (S subtree-of G) ex-or (G subtree-of S)`
* `(S strictly-related-to G) := (S related-to G) and (S != G)`
* `(S strictly-related-to G) <-> (G strictly-related-to S)`

Note that the definition of the "related-to" terms is intended to shift
ones focus away from the elements the trees contain. That is, the focus
is shifted towards the relationship between two trees.

<!-- ======================================================================= -->
## remarks

Note that, since a tree must by definition have at least a root node,
a tree is always unequal to the empty graph.
