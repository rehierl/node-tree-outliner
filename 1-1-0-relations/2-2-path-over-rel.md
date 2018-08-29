
<!-- ======================================================================= -->
# Path (p) over relation (R)

* (/see/ "path of nodes" in "node trees" /)

A path over an endo-relation `R := (V,E)` such that `(E subset-of VxV)` is a
sequence of vertices `p := (v1,v2,...,vk) in ×V^k` such that `(xi in V)`. In
addition to that, any consecutive pair of vertices represents an edge in `R`
- i.e.  `((vi,vi+1) in E)`.

the length of a path `(#p == k)`

* a vertex-based view
* i.e. `(#p := k)` if `p := (v1,...,vk)`
* i.e. the number of components in `p`
* aka. the vertex-length of a path
* a hop/pair/edge-based view
* i.e. `(#p := #{ (vi,vi+1) })`, i.e. `(#p == (k-1))`
* i.e. the number of consecutive pairs in `p`
* aka. the edge-length of a path

clarification

* `p := ()` and `p := (v1)` are both degenerated paths
* a path may have in general infinite length
* the definitions for sequences apply to paths
* i.e. subsequence-of, prefix-of, ...

<!-- ======================================================================= -->
## loops, cycles

* in this discussion, loops and cycles are not taken into account
* hint - trees are by definition loop-less and acyclic

cyclic vs. acyclic

* `p` is cyclic, if `((v,...,v) subsequence-of p)`
* i.e. `p` is cyclic, if `(#E(p) < #p)`
* i.e. `p` is acyclic, if `(#E(p) == #p)`
* `p` has loops, if `((v,v) subsequence-of p)`
* i.e. loops count as cycles that have edge-length 1 - aka. 1-cycle

Put differently, a path is cyclic if a vertex in it is
presequent and subsequent to itself.

<!-- ======================================================================= -->
## direction/orientation

With each edge `(e in E)` of an endo-relation `R := (V,E)`, a statement (i.e.
semantics) is associated. The edges therefore support a sense of **direction**
and/or **orientation**, if the vertices of an edge are considered to be unequal.

However, that notion of orientation is broken, if two vertices are connected
in both ways (i.e. `aEb` and `bEa`). In order for all edges to have consistent
orientation, `R` must be anti-symmetric and irreflexive (i.e. asymmetric).
In general, `R` must be **acyclic**.

With that in mind, any path `p=(v1,v2,...)` over such a relation `R` can be
understood to be **uni-directional**, if `((vi,vi+1) in R)` for any pair of
consecutive vertices.

A path may be referred to as being **multi-directional**, if it contains
pairs such that `(vi,vi+1)` or `(vi+1,vi)` in `R`. Put differently, if the
path contains pairs in `R` and `ant(R)` (i.e. inverted/antonymous relation).

A path may be referred to as **consistent with**, or **in the direction of**
`R`, if each pair `(vi,vi+1)` is an edge in `R`. In contrary to that, a path
may be referred to as being uni-directional but **inverted**, or **antonymous**,
if each pair `(vi,vi+1)` is an edge in `ant(R)`.

<!-- ======================================================================= -->
## reachability-based

* covered-by is synonymous to strictly-connected-to

(p in R), (R contains p)

* any edge `(e in E)` represents a path `p`
* i.e. `aRb` => `p:=(a,b)` => `(p in E)`
* `R` is said to contain path `p:=(a,b)`, if `aRb`
* i.e. `R` can be understood to contain any possible path
* i.e. `(p in R)`, if `p=(v1,...,vn)` and `((vi,vi+1) in E)`

extended notation

* `P := { p | (p in R) }`
* i.e. the set of all possible paths in `R`
* `aPb := (p in R)` where `p := (a,...,b)`
* i.e. a path `p` exists in `R` that connects `a` with `b`

(a connected-to b)

* `(a connected-to b)`, if `aPb` and/or `bPa`
* `a` is connected-to `b` and/or `b` is connected-to `a`
* synonymous - related-to, comparable-to
* note - connected-to is undirected

(a not-connected-to b)

* `(a not-connected-to b)`, if neither `aPb` nor `bPa`
* synonymous - disconnected-from, unrelated-to, incomparable-to

(a strictly-connected-to b)

* `(a strictly-connected-to b)`, if `aRb` and/or `bRa`
* `a` is directly connected-to `b` and/or `b` is directly connected-to `a`
* synonymous - strictly-related-to, covered-by

(a loosely-connected-to b)

* `(a loosely-connected-to b)`, if connected, but not strictly connected
* i.e. there are vertices in between `a` and `b`
* i.e. connected-to <-> (strictly- or loosely-connected-to)
* synonymous - loosely-related-to

(a simply/strongly-connected-to b)

* simply, if `aPb` ex-or `bPa`
* strongly, if `aPb` and `bPa`

<!-- ======================================================================= -->
## sequence-based

* **TODO** - rethink - keep or remove?

(a sequent-to b)

* `(a sequent-to b)`, if `aPb` and/or `bPa`
* i.e. equivalent to connected/related/comparable
* antonym - not sequent, i.e. not "insequent"

(a insequent-to b)

* `(a insequent-to b)`, if neither `aPb` nor `bPa`
* i.e. equivalent to disconnected/unrelated/incomparable
* **TODO** - an unexpected, path-based perspective
* it could use some additional thought

(a predecessor-of b)

* `(a predecessor-of b)`, if `aPb`
* i.e. predecessor-of is directed
* synonymous - presequent-to

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
