
<!-- ======================================================================= -->
# Definitions related to relations

* standard and non-standard, relation-based definitions
* the focus is on endo-relations `R := (V,E)`

relevant to ...

* (/see/ "graph theory" /)
* (/see/ "order theory" /)

<!-- ======================================================================= -->
## endo-relations

In general, a relation `R` is defined as an ordered tuple of sets which begins
with one or more simple sets of elements `Si` and ends in the relation's graph
`G`, where `G` is defined as a subset of the Cartesian product `×Si` over the
sets of elements `Si`. That is, `G` is an element of the powerset `P(×Si)`.

* `R := (S1,...,Sn,G)`
* `(G subset-of ×Si)` or `(G in P(×Si))`
* where `×Si := (S1 × ... × Sn)`

In addition to the above, each relation `R` is understood to be accompanied by
its characteristic function `R()` which allows to determine whether or not a
given tuple of elements in `×Si` is an element in `G`.

* `(R: (S1,...,Sn) -> Bool)`
* `R(t)` is true, if `(t in G)` for some tuple `(t := (s1,...,sn))`

In the context of this discussion, all relations are binary relations (i.e.
each has only two sets of elements `S1` and `S2`) over a single set of elements
`S` (i.e. `S1` and `S2` are both equal to the same set `S`, i.e. a homogenous
relation). That is, the focus of this discussion is on endo-relations.

* `R := (S1,S2,G) := (S,S,G) := (S,G)`
* `R(s1,s2)` is true, if `((s1,s2) in G)`

<!-- ======================================================================= -->
## domain of relation

* for `R := (A,B,G)`

domain - a type-based view

* `P(X)` refers to the powerset of set `X`
* `D(R), dom(R) := G` for some `(G in P(A × B))`
* `T(R), type(R) := (A × B)`
* `(D(R) subset-of T(R))`

domain - a function-based view (default)

* set of departure `A`
* set of destination `B` (codomain)
* `dom(R) := { x | xRy for at least one (y in B) }`
* `range(R) := { y | xRy for at least one (x in A) }`
* `field(R) := (dom(R) union range(R))`

<!-- ======================================================================= -->
## general context

Due to the focus on endo-relations, graph theoretical terminology will be used
in the context of such relations. That is, endo-relations are understood to
define and represent (directed) graphs.

* `R := (V,E)` where `(E subset-of V×V)`
* `V` is the set of vertices, `E` is the set of edges `e`
* `xRy := xEy := R(x,y)` is true, if `(e in E)` for `(e := (x,y))`
* `x` is adjacent to `y` and `y` adjacent to `x`, if `xEy`
* `e` is incident to `x` and `y`, if `xEy`
* `x` and `y` are both endpoints of `e`

Each endpoint of an edge `(e in E)` must be an element of the set of vertices
`V`. Put differently, the set of endpoints of each edge must be a subset to
the vertex set. Obviously, `R` would otherwise not satisfy the definition of
a relation, if `E` would contain some edge `e` that has one or both of its
endpoints outside of the vertex set `V` (i.e. `(v !in V)`).

* if `(e in E)`, then `(E(e) subset-of V)`

Each edge `e := (x,y)` in `E` is an element of the Cartesian product `V×V`
over the set of vertices `V`. Because of that, each edge `e` has `x` as its
first and `y` as its last vertex. As such, the endpoints of an edge are in
general considered to be unequal, which is why the edges in a relation support
a notion of orientation (i.e. the edges are directed). Hence, endo-relations
are understood to represent and define directed graphs.

* `x` is the source, and `y` the sink of `e`
* `x` is a source to `y` and `y` a sink to `x`

As a simple set of elements, the set of vertices `V` is in general not required
to hold vertices that have common characteristics. That is, the vertices in a
relation may in general represent arbitrary elements. However, in the context
of this discussion, all vertices are expected to represent elements of some
sort, which is why all vertices in a relation are required to share common
characteristics. Put differently, the set of vertices in a relation is expected
to be a homogenous set of elements.

Similar to that, some expression is associated with each edge `(e in E)` that
is understood to provide an explanation as to why two vertices are adjacent to
each other. This reason will be referred to as the semantics of an edge.

* e.g. `sem(e) := (x divisible-by y)` for some edge `e := (x,y)`

The semantics of two edges `e1` and `e2` in a relation are in general not
required to correspond with each other. That is, `(sem(e1) != sem(e2))` may
in general be true for some pair of edges. In such a case, the set of edges
`E` is said to be heterogenous. Because of that, a relation can in general
be understood to hold a set of tuples that provides a mapping between an edge
and its semantics.

* `R := (V,E,S)`, where `S` is defined as follows
* `S := { (e,s) | (e in E) and (s == sem(e)) }`

However, in the context of this discussion, the semantics of each edge is
expected to correspond with the semantics of all the other edges in a relation.
Because of that, the semantics of a relation `sem(R)` can be defined as the
common semantics of its edges.

* `(sem(R) == sem(e))` for all `(e in E)`

Put together, all relations in this discussion are seen as directed graphs and
are expected to be endo-relations based upon a homogenous set of vertices and
a homogenous set of edges.
