
<!-- ======================================================================= -->
# Definitions related to relations and graph theory

* relevant standard and non-standard, relation-based definitions
* the focus is on endo-relations `R := (V,E)`

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
relation). That is, each relation in the context of this discussion is an
endo-relation.

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
## related graph-based terminology

Due to the focus on endo-relations, graph theoretical terminology can be used
in combination with the above relations. That is, relations are understood to
represent graphs.

* `R := (V,E)`, where `(E subset-of V×V)`
* `V` is the set of vertices, `E` the set of edges `e`
* `xRy := xEy := R(x,y)` is true, if `((x,y) in E)`
* `e` is incident to `x` and `y`, if `e := (x,y)` and `xEy`
* `x` is adjacent to `y`, if `xEy` is true
* `x` and `y` are both endpoints of `e`
* (see graph theory for more even terms)

Each edge `e := (x,y)` in the set of edges `E` is an element of the Cartesian
product `V×V` over the set of vertices `V`. Because of that, each edge has `x`
as its first and `y` as its last vertex. Hence, the edges in a relation are
directed, which is why relations can be understood to represent directed graphs.

* `x` is the source, and `y` the sink of `e`
* `x` is a source of `y` and `y` a sink of `x`

Each endpoint of an edge `(e in E)` must be an element of the set of vertices
`V`. Put differently, the set of endpoints of each edge must be a subset to
the vertex set. Obviously, `R` would otherwise not satisfy the definition of
a relation, if `E` would contain some `e` that had an element outside of the
vertex set (i.e. `(v !in V)`).

* if `(e in E)`, then `(E(e) subset-of V)`

Recall that each element in the Cartesian product `×Si` is an ordered tuple.
That is, each tuple has a 1st (`S1`) and a last element (`Sn`).

The set of vertices `V` is in general not required to hold vertices that have
common characteristics. That is, the vertices in a relation may in general be
arbitrary elements. However, in the context of this discussion, all vertices
are by default expected to represent elements of some sort, which is why all
vertices in a relation are required to share some common characteristics.

Similar to that, some reason is associated with each edge `(e in E)` which
provides an explanation as to why two vertices are adjacent to each other.
This reason will be referred to as **the semantics of an edge** `sem(e)`.

In general, 

A relation that only has an empty set of vertices (i.e. `(V == {})`) and no
edge in `E` (i.e. `(E == {})`), will be referred to as the **null relation**,
or as the "empty relation" `Ø`. That is, the null relation is a binary tuple
of empty sets (i.e. `Ø := ({},{})`).

In contrary to that, a relation that has a set of `n` vertices and an edge
for every pair of vertices, will be referred to as the **complete relation**
`Rn`. That is, the set of edges of a complete relation is equal to the
Cartesian product over its set of vertices (i.e. `(E == V×V)`). (Note that
complete relations may be used similar to concept of the universal set `U`).
