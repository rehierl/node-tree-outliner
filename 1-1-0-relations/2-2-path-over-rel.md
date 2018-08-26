
<!-- ======================================================================= -->
# Path (p) over relation (R)

* (/see/ "path of nodes" /)

a relation-based definition of "path"

* given a binary relation `R := (A,B,G)`
* a path over `R` is a sequence `p := (x1,x2,...,xn)`
* such that `(xi in (A or B))` and
* where `(ei in R)` for `ei := (xi,xi+1)`
* and all `(i in [1,#p-1])`
* i.e. `(x1 in A)` and/or `(x1 in B)`

the length of a path `(#p == n)`

* a sequence-based path/definition/view
* i.e. `(#p == n)` if `p := (x1,...,xn)`
* a hop/pair/edge-based path/definition/view
* i.e. `(#p == #{ (xi,xi+1) })`, i.e. `(#p == (n-1))`
* a degenerated path if `p in { [], [x1] }`

clarification

* if `(A disjoint-to B)`, then `(#p == 2)`
* i.e. for no `aRb` there is a `c` such that `bRc`
* if `((A isect B) != {})`, then `(#p in [2,*])`
* i.e. `p` may even have infinite length

as sequences of elements

* a path `p` over relation `R` is a sequence of vertices
* i.e. all definitions for sequences of elements can be used
* e.g. sub-sequence <-> sub-path

<!-- ======================================================================= -->
## loops, cycles

* in this discussion, loops and cycles are not taken into account
* hint - trees are by definition loop-less and acyclic

cyclic vs. acyclic

* `p` is cyclic, if `p` has repetitions
* i.e. `([y,...,y] subpath-of p)` where `(y in (A or B))`
* `p` is cyclic, if `(#E(p) < #p)`
* `p` is acyclic, if `(#E(p) == #p)`
* `p` has loops, if `([y,y] subpath-of p)`

Put differently, a path is cyclic if an element in it is
presequent and subsequent to itself.

<!-- ======================================================================= -->
## direction/orientation

With each edge `(e in E)` of an endo-relation `R := (V,E)`, a statement (i.e.
semantics) is associated. The edges therefore support a sense of **direction**
and/or **orientation**, if the vertices of an edge are considered to be unequal.

However, that notion of orientation is broken, if two vertices are connected
in both ways (i.e. `aEb` and `bEa`). `R` must therefore be anti-symmetric and
irreflexive (i.e. asymmetric). In general, `R` must be **acyclic**.

With that in mind, any path `p=[v1,v2,...]` over such a relation `R` can be
understood to be **uni-directional**, if `((vi,vi+1) in R)` for any pair of
consecutive vertices.

A path may be referred to as being **multi-directional**, if a path contains
pairs such that `(vi,vi+1)` or `(vi+1,vi)` in `R`. Put differently, if the
path contains pairs in `R` ex-or `ant(R)` (i.e. inverted/antonymous relation).

A path may be referred to as **consistent with**, or **in the direction of**
`R`, if each pair `(vi,vi+1)` is an element of `R` (aka. connected in `R`).
In contrary to that, a path may be referred to as being **inverted**, or
**antonymous**, if each pair `(vi,vi+1)` is an element of `ant(R)`.

<!-- ======================================================================= -->
## reachability-based

* covered-by is synonymous to strictly-connected-to

(p in R), (R contains p)

* any edge `(e in G)` represents a path `p`
* i.e. `aRb` => `p:=(a,b)` => `(p in G)`
* `R` is said to contain path `p:=(a,b)`
* i.e. R can be extended to contain any path over its edges
* i.e. `(p in R)` if `p=(x1,...,xn)` and `((xi,xi+1) in G)`

extended notation

* `P := { p | (p in R) }`
* i.e. the set of all (possible) paths in `R`
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

(a sequent-to b)

* `(a sequent-to b)`, if `aPb` and/or `bPa`
* i.e. equivalent to connected/related/comparable
* antonym - not sequent, i.e. not "insequent"

(a insequent-to b)

* `(a insequent-to b)`, if neither `aPb` nor `bPa`
* i.e. equivalent to disconnected/unrelated/incomparable
* **TODO** - a path-based definition - interesting
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
