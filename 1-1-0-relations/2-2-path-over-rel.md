
<!-- ======================================================================= -->
# Path (p) over relation (R)

* (/see/ "path of nodes" in "node trees" /)

A path over an endo-relation `R := (V,E)` such that `(E subset-of VxV)` is a
sequence of vertices `p := (v1,v2,...,vk) in ×V^k` such that `(xi in V)`. In
addition to that, any consecutive pair of vertices represents an edge - i.e.
`((vi,vi+1) in E)`.

The length of a path `p := (v1,...,vk)`

* a vertex-based view
* i.e. `(#p := k)`
* i.e. the number of components in `p`
* aka. the vertex-length of `p`
* a hop/pair/edge-based view
* i.e. `(#p := (k-1))`
* i.e. the number of consecutive pairs in `p`
* aka. the edge-length of `p`
* by default, `#p` refers to the vertex-length

Degenerated paths

* even though there are no consecutive pairs, ...
* `p := ()` and `p := (v1)` are both seen as degenerated paths
* a path may in general have any/infinite length
* the definitions for sequences apply to paths
* i.e. subsequence-of, prefix-of, ...

<!-- ======================================================================= -->
## set of paths P over R

The following is an inductive definition of the set of all possible paths that
can be formed based on a given relation `R := (V,E)`:

(0) `P0 := { () }`

That is, the empty sequence of nodes `()` is considered to be the initial path.

(1) `P1 := { (a × b) | (a in P0), (b in V) }`

That is, `P1` holds all 1-node sequences.

(i) `Pi := { (a × b) | (a in P(i-1)), (b in V), ((ak,b) in E), (ak = a[#a]) }`

That is, the next set of paths `Pi` is formed from the previous set of paths
`P(i-1)` by concatenating all those vertices `b` to each path `a`, if there is
an edge `(e in E)` such that `(e == (ak,b))`.

* `P := P0 + P1 + ... + P(i-1) + Pi` for `(i in [0,*])`
* `P := (union-of Pi)` for all `(i in [0,*])`
* i.e. `(E subset-of P)` - i.e. each edge `(e in E)` is a path

Each relation `R` can be understood to have such a set of all possible paths
`P` associated with it. Any relation can therefore be understood to be defined
as a triplet of sets: `R := (V,E,P)`.

<!-- ======================================================================= -->
## in, contains

A sequence of vertices can be understood to represent a path `p` in relation
`R`, if `p` is an element of the relation's set of all possible paths `P`.
That is, relation `R` can be understood to contain path `p`.

* `(p in R)` := `p` is a path in `P`
* `(R contains p) := (p in R)`

<!-- ======================================================================= -->
## aPb, p(a,b)

The following selector functions can be defined:

* `(p: V×V -> P(P) )`
* `p(a,b) := { p | (p := (a,...,b)) where (p in R) }`
* `p(a,b) := { (a) }` iff `(a == b)`
* i.e. the set of paths in `R` that begin in `a` and end in `b`

Note that, in cases where a relation has exactly one such path, `p(a,b)` is
understood to return a single path `p := (a,...,b)` instead of a set of paths.

* `(p: V×P(V) -> P(P) )`
* `p(a,B) := { p(a,b) | for all (b in B) and (p in R) }`
* i.e. the set of paths in `R` that being in `a` and end in a vertex of `B`

Indicator function

* `aPb := (p(a,b) != {})` or
* `aPb := (p(a,b) in R)` if only one such path is possible
* i.e. a path `p` exists in `R` that begins in `a` and ends in `b`

Notational inaccuracy

* `aPb` may also be used instead of `p(a,b)`
* i.e. `aPb` may refer to the corresponding set of paths

<!-- ======================================================================= -->
## loops, cycles

* in this discussion, loops and cycles are considered to be excluded
* hint: trees have by definition neither loops nor cycles

cycles

* `p` is a cycle, if `(p == p(v,v))` for some `(v in V)`
* i.e. `p` begins and ends in the same vertex `v`
* i.e. `p` contains a vertex more than once - i.e. `(#E(p) < #p)`
* `p` is cyclic, if `(#E(p) < #p)`
* `p` is acyclic, if `(#E(p) == #p)`
* `R` is cyclic, if `R` has one or more cyclic paths `(p in P)`
* `R` is acyclic, if `R` has no cyclic path `(p in P)`

Note that a path is cyclic if a vertex in it is
presequent and subsequent to itself.

loops

* `p` is a loop, if `(p == (v,v))` for some `(v in V)`
* i.e. `p` is a cycle of vertex-length 2 (aka. edge-length 1)
* i.e. `p` is a 1-cycle

Note that an acyclic relation has no loops.

<!-- ======================================================================= -->
## direction/orientation

With each edge `(e in E)` in an endo-relation `R := (V,E)`, a statement (i.e.
semantics) is associated. The edges therefore support a notion of **direction**
and/or **orientation**, if the vertices of an edge are considered to be unequal.

However, that sense of orientation is broken, if two vertices are connected
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

* covered-by := strictly-connected-to

(a connected-to b)

* `(a connected-to b)`, if `aPb` and/or `bPa`
* `a` is connected-to `b` and/or `b` is connected-to `a`
* synonymous - related-to, comparable-to
* note - connected-to is undirected

(a not-connected-to b)

* `(a not-connected-to b)`, if neither `aPb` nor `bPa`
* synonymous - disconnected-from, unrelated-to, incomparable-to

(a strictly-connected-to b)

* `(a strictly-connected-to b)`, if `aEb` and/or `bEa`
* `a` is directly connected-to `b` and/or `b` is directly connected-to `a`
* synonymous - strictly-related-to, covered-by

(a loosely-connected-to b)

* `(a loosely-connected-to b) := (a connected-to b) and !(a strictly-connected-to b)`
* i.e. there are vertices in between `a` and `b` - i.e. `(#p > 2)`
* i.e. connected-to <-> (strictly- or loosely-connected-to)
* synonymous - loosely-related-to

(a simply/strongly-connected-to b)

* simply, if `aPb` ex-or `bPa`
* strongly, if `aPb` and `bPa`

<!-- ======================================================================= -->
## sequence-based

* **TODO** - remove this?

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
