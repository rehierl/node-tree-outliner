
<!-- ======================================================================= -->
# Path-based, vertex-related definitions

In a graph `G := (V,E)`, "the distance between two vertices" `x` and `y` is the
edge-length of the shortest possible path `p(x,y)` in `UG(G)`. (Note that the
distance between a vertex and itself is `0`, regardless whether `G` contains
reflexive edges or not).

<!-- ======================================================================= -->
## loops, cycles

cycles

* `(p in P)` is a cycle, if `(p == p(v,v))` for some `(v in V)`
* i.e. `p` begins and ends with the same vertex `v`
* `p` is cyclic, if `(#E(p) < #p)`
* i.e. `(p[i] == p[j])` for some `(i != j)`
* i.e. `p` contains repeated vertices
* `p` is acyclic, if `(#E(p) == #p)`
* `G` is cyclic, if `P` contains a cyclic path
* `G` is acyclic, if `P` has no cyclic paths
* i.e. all paths `(p in P)` are acyclic

Note that a path is cyclic, if it contains a vertex more than once.
That is, the corresponding vertex is presequent and subsequent to itself.

loops

* `(p in P)` is a loop, if `(p == (v,v))` for some `(v in V)`
* i.e. `p` is a cycle of edge-length 1
* i.e. `p` is a 1-cycle

Note that an acyclic graph is also loop-less. However, an irreflexive
graph/relation (i.e. no loops) may still have cycles.

<!-- ======================================================================= -->
## reachability-based qualifiers

* covered-by := strictly-connected-to

(a connected-to b)

* `(a connected-to b)`, if `aPb` and/or `bPa`
* `a` is connected-to `b` and/or `b` is connected-to `a`
* synonymous - related-to, comparable-to
* note - connected-to is undirected

(a not-connected-to b)

* `(a not-connected-to b)`, if neither `aPb` nor `bPa`
* synonymous - disconnected-from, unrelated-with, incomparable-to

(a strictly-connected-to b)

* `(a strictly-connected-to b)`, if `aEb` and/or `bEa`
* `a` is directly connected-to `b` and/or `b` is directly connected-to `a`
* synonymous - strictly-related-to, covered-by

(a loosely-connected-to b)

* `(a loosely-connected-to b)` := connected, but not strictly-connected
* i.e. the shortest path between `a` and `b` has more than 2 vertices
* i.e. there are one or more vertices in between `a` and `b`
* i.e. connected <-> (strictly- ex-or loosely-connected)
* synonymous - loosely-related-to

(a simply/strongly-connected-to b)

* simply, if `aPb` ex-or `bPa`
* strongly, if `aPb` and `bPa`

<!-- ======================================================================= -->
## sequence-based qualifiers

(a sequent-to b)

* `(a sequent-to b)`, if `aPb` and/or `bPa`
* i.e. equivalent to connected/related/comparable
* note - "sequent-to" is undirected

(a insequent-to b)

* `(a insequent-to b)`, if neither `aPb` nor `bPa`
* i.e. equivalent to disconnected/unrelated/incomparable
* i.e. "insequent" is antonymous to "sequent"
* **TODO** - an unexpected, path-based perspective
* i.e. could maybe use some additional thought

(a predecessor-of b)

* `(a predecessor-of b)`, if `aPb`
* i.e. predecessor-of is directed
* synonymous - presequent-to
* note - "predecessor-of" is directed

(b successor-of a)

* `(b successor-of a)`, if `bPa`
* i.e. successor-of is directed
* note - `aPb` and `bPa` may both be true
* synonymous - subsequent-to

similar definitions possible for ...

* strict/loose predecessor-of
* strictly/loosely presequent-to
* strict/loose/distant successor-of
* strictly/loosely subsequent-to

Note that, because each edge `((x,y) in E)` is a path of vertex-length 2, two
adjacent vertices can be said to be sequent to each other. That is, `x` is
(strictly) presequent to `y`, and `y` (strictly) subsequent to `x`.
