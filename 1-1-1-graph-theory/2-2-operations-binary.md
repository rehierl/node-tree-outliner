
<!-- ======================================================================= -->
# Binary operations on graphs

<!-- ======================================================================= -->
## equal, unequal, distinct

* (/see/ "core definitions" /)
* given two graphs `S := (T,U)` and `G := (V,E)`

`S` and `G` are **equal**, if ...

* `(S == G)`, if `(T == V)` and `(U == E)`
* i.e. both have the same vertex-set and the same edge-set
* i.e. all vertices and edges of one graph are elements of the other
* `(S == G) := (S subgraph-of G) and (G subgraph-of S)`

`S` and `G` are **unequal**, if ...

* `(S != G) := not (S == G)`
* i.e. both differ in their vertex-set and/or in their edge-set
* i.e. a graph (or both) has elements that the other does not have

Note that two unequal graphs are said to be **distinct** (from one another).

<!-- ======================================================================= -->
## disjoint, coupled, overlap

Given two (simple) sets `A` and `B`, the following definitions apply:

* `(A disjoint-to B) := ((A & B) == {})`
* `(A coupled-with B) := not (A disjoint-to B)`

Two graphs `S := (T,U)` and `G := (V,E)` are said to be **disjoint**
(from one another), if both have neither vertices nor edges in common:

* `(S disjoint-to G)`, if `(T disjoint-to V)` and `(U disjoint-to E)`
* `(S disjoint-to G) <-> (G disjoint-to S)`

Two graphs `S` and `G` are said to be **coupled** (with each other),
if both have one or more vertices and/or edges in common:

* `(S coupled-with G) := not (S disjoint-to G)`
* `(S coupled-with G) <-> (G coupled-with S)`

Like the common elements in coupled simple sets of elements, the above common
vertices and/or edges act as a "link" between both graphs. These links can
therefore be understood to bind both graphs together, which is why two such
graphs can be said to be "connected" or "coupled" via some "point of contact".

Two graphs `S` and `G` are said to **overlap** (each other), if both are coupled
with each other, and if both have one or more vertices and/or edges the other
graph does not have.

* `(S overlaps G) := (S coupled-with G) and (S unrelated-to G)`
* `(S overlaps G) <-> (G overlaps S)`

<!-- ======================================================================= -->
## remarks on - disjoint, coupled, related

Note that both endpoints of an edge `(e in E)` in a graph `G := (V,E)` must
be elements in the graph's set of vertices `V` (i.e. `(E(e) subset-of V)`).
If that is not the case, then `G` would not satisfy the definition of a graph.

Two coupled graphs `S := (T,U)` and `G := (V,E)` always have coupled sets of
vertices. That is because the endpoints of a common edge are always elements
in both sets of vertices `T` and `V`. The converse is however not necessarily
true. That is because both sets of vertices may be coupled via disconnected
vertices.

* `(U coupled-with E) -> (T coupled-with V)`

Note that an empty subgraph `S` of a graph `G` is disjoint to its supergraph,
regardless whether the supergraph is itself empty or not.

* `(S == Ø)` => `(S subgraph-of G)` and `(S disjoint-to G)`

Note that a non-empty subgraph is coupled with its supergraph.
That is, a non-empty subgraph is never disjoint to its supergraph.

* `(S != Ø)` and `(S subgraph-of G)` => `(S coupled-with G)`
* `(S related-to G) -> (S coupled-with G)` if `(S != Ø)`

Note that the converse is not necessarily true. That is, two graphs that are
coupled with each other, are not necessarily related to each other.

* `(S coupled-with G)` =!> `(S related-to G)`
* `(S coupled-with G)` <=> `(S related-to G)` or `(S overlaps G)`

Note that two graphs are unrelated if they overlap each other. Likewise, two
graphs that overlap each other are unrelated. Because of that, "overlaps" and
"related-to" are exclusive such that they can not be both.

<!-- ======================================================================= -->
## union (+, or, union)

Graph `G := (V,E)` is said to be the **union** graph `G := (S + X)` of two
graphs `S := (T,U)` and `X := (Y,Z)`, if its vertex-set is the union of both
vertex sets, and if its edge-set is the union of both edge sets.

* `G := (S + X) := (V,E)`, where
* `V := (T + Y)` and `E := (U + Z)`
* associative - `(A + B + C) == ((A + B) + C) == (A + (B + C))`
* commutative - `(A + B) == (B + C)`

Note that `S` and `X` are not required to be disjoint.

<!-- ======================================================================= -->
## intersection (&, and, isect)

Graph `G := (V,E)` is said to be the **intersection** graph `G := (S & X)`
of two graphs `S := (T,U)` and `X := (Y,Z)`, if `G` was formed by taking
all vertices and edges that are common to both.

* `G := (S & X) := (V,E)`, where
* `V := { (v in T) | (v in Y) }` and `E := { (e in U) | (e in Z) }`
* associative - `(A & B & C) == ((A & B) & C) == (A & (B & C))`
* commutative - `(A & B) == (B & C)`

Note that the intersection graph `G` is a subgraph of `S` and `X`.

* `(G subgraph-of S)` and `(G subgraph-of X)` are both true, if `(G := (S & X))`

Two graphs `S` and `X` are said to **intersect** (each other), if their
intersection graph `(S & X)` is unequal to the empty graph `Ø`.

* `(S intersects X) := ((S & X) != Ø)`
* `(S intersects X) <-> (X intersects S)`
* `(S intersects X) <-> (S coupled-with X)`

<!-- ======================================================================= -->
## remarks on - intersection

As above, two intersecting graphs are not necessarily related to each other.
However, two such graphs are either related, or both overlap each other.

* `(S related-to G) -> (S intersects G)` (i.e. if `S` and `G` are non-empty)
* `(S intersects G) <-> (S related-to G) ex-or (S overlaps G)`

Note that the set of vertices `V` in an intersection graph `G := (S & X)` does
not allow to determine the set of common edges `E` based on one of the input
graphs involved. That is, the intersection graph `G` is **not (necessarily)
an induced subgraph** of one or both of the input graphs (i.e. `(G == S[V])`
and `(G == X[S])` are both not necessarily true).

Example 1: The intersection graph `G := (S & X)` for `S := ({1,2},{(1,2)})`,
`X := ({1,2},{(2,1)})` is `G := ({1,2},{})`. That is, `G` is not an induced
subgraph to any of them (i.e. `(G == S[V])` and `(G == X[V])` are both false).

Example 2/3: The intersection graph `G := (S & X)` for `S := ({1,2},{(1,2)})`,
`X := ({1,2},{})` is `G := ({1,2},{})`. That is, `G` is not an induced subgraph
of `S`, but an induced subgraph of `X` (i.e. in contrary to `(G == S[V])` being
false, `(G == X[V])` is true).

Example 4: The intersection graph `G := (S & X)` for `S := ({1,2},{(1,2)})`,
`X := ({1,2,3},{(1,2)})` is `G := ({1,2},{})`. That is, `G` is an induced
subgraph of `S` and an induced subgraph of `X` (i.e. `(G == S[V])` and
`(G == X[V])` are both true).
