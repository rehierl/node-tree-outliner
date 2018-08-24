
<!-- ======================================================================= -->
# Non-standard definitions

<!-- ======================================================================= -->
## domain of relation (R)

domain - a type-based view

* `dom(R) := G` for some `(G in P(A × B))`
* `type(R) := (A × B)`
* `dom(R) subset-of type(R)`

domain - a function-based view (default)

* set of departure `A`
* set of destination `B` (codomain)
* `dom(R) := { x | xRy for at least one y in B }`
* `range(R) := { y | xRy for at least one x in A }`
* `field(R) := (dom(R) + range(R))`

<!-- ======================================================================= -->
## path (p) over relation (R)

a relation-based definition of "path":

* given a binary relation `R := (A,B,G)`
* a path over `R` is a sequence `p := (x1,x2,...,xn)`
* such that `(xi in (A or B))` and
* where `(ti in R)` for `ti := (xi,xi+1)`
* and all `(i in [1,(#p-1)])`
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
* if `((A & B) != {})`, then `(#p in [2,*])`
* i.e. `p` may even have infinite length

as sequences of elements

* a path `p` over relation `R` is a sequence of vertices
* i.e. all definitions for sequences of elements can be used
* e.g. sub-sequence <-> sub-path

<!-- ======================================================================= -->
## reachability

(p in R), (R contains p)

* any edge `(e in G)` represents a path `p`
* i.e. `aRb` => `p:=(a,b)` => `(p in G)`
* `R` is said to contain path `p:=(a,b)`
* i.e. R can be extended to contain any path over R
* i.e. `(p in R)` if `p=(x1,...,xn)` and `((xi,xi+1) in G)`

extended notation

* `P := { p | (p in R) }`
* i.e. the set of all (possible) paths in `R`
* `aPb := (p in R)` where `p := (a,...,b)`
* i.e. a path `p` exists in `R` that connects `a` with `b`

(a connected-to b)

* `(a connected-to b)`, if `aPb` and/or `bPa`
* `a` is connected-to `b` and/or `b` is connected-to `a`
* synonymous - connected-to, related-to, comparable-to
* note - connected-to is undirected

(a not-connected-to b)

* `(a not-connected-to b)`, if neither `aPb` nor `bPa`
* synonymous - not-connected-to, unrelated-to, incomparable-to

(a strictly-connected-to b)

* `(a strictly-connected-to b)`, if `aRb` and/or `bRa`
* `a` is directly connected-to `b` and/or `b` is directly connected-to `a`
* synonymous - strictly-connected-to, strictly-related-to

(a loosely-connected-to b)

* `(a loosely-connected-to b)`, if connected, but not strictly connected
* i.e. there are vertices in between `a` and `b`
* synonymous - loosely-connected-to, loosely-related-to
* i.e. connected-to <-> (strictly- or loosely-connected-to)

(a simply/strongly-connected-to b)

* simply, if `aPb` ex-or `bPa`
* strongly, if `aPb` and `bPa`

(a predecessor-of b)

* `(a predecessor-of b)`, if `aPb`
* i.e. predecessor-of is directed

(a successor-of b)

* `(b successor-of a)`, if `bPa`
* i.e. successor-of is directed
* note - `aPb` and `bPa` may both be true

<!-- ======================================================================= -->
## loops, cycles

* in this discussion, loops and cycles are not taken into account
* hint - trees are acyclic

cyclic vs. acyclic

* `p` is cyclic, if `p` has repetitions
* i.e. `([y,...,y] subpath-of p)` where `(y in (A or B))`
* `p` is cyclic, if `(#E(p) < #p)`
* `p` is acyclic, if `(#E(p) == #p)`
* `p` has loops, if `([y,y] subpath-of p)`
