
<!-- ======================================================================= -->
# Relations

<!-- ======================================================================= -->
## finitary relations

(the set-theoretic notion of "relation")

* `R := (S,S2,...,Sn,G)`
* e.g. `Si := Nat`, `G := {(1,2), (2,3), ...}`
* `S1,...,Sn` represent sets of some sorts
* `n in [1,*]` is the number of slots/places
* `n` is the arity/adicity/dimension of relation `R`
* `R` is itself a (n+1)-tuple (aka. correspondence)
* `R` is said to be a n-ary/n-adic/n-dimensional relation
* `R` is finitary, if `n` is finite, otherwise `R` is infinit-ary
* the sets `Si` are the domains of `R`

graph `G` of relation `R`

* `G` is the relation's set of tuples/sequences
* `×` is the Cartesian product of all sets involved
* `(G(R) subset-of ×Si)` is the graph of `R`
* `(G(R) subset-of ×S^n)` if `Si := S` for any `i in [2,*]`
* an "n-ary relation over `S`", or an "n-ary relation over a set"
* note - all tuples in `G` have the exact same length

characteristic function

* `chi(×Si), R(×Si) := (S1,...,Sn) -> boolean`
* `R(×Si)` returns true, if `s in ×Si` is in the relation `R`
* `R(×Si)` is the characteristic function of `R`
* aka. indicator function, n-place predicate
* `s in R` is a tuple/individual in/of `R`/`G`
* `s in R` is true, if `R(×Si)` returns true

clarification

* `Ra` denotes an unary relation - a property
* `Rab` or `aRb` - a binary relation
* `Rabc` - a ternary relation
* `Ra...` is true, if `(a,...) in R`

clarification

* `Rab` or `aRb` is true, if `(a,b) in R`
* `!Rab` or `!aRb` is true, if `(a,b) not in R`
* `R` is in general used synonymous to `G`
* e.g. `(r in R)` rather than `(r in G)`
* e.g. `(R subset-of ×Si)` rather than `(G subset-of ×Si)`
* similar definitions for `sequence-of`, etc.

<!-- ======================================================================= -->
## binary relations

(correspondence, dyadic relation, 2-place relation)

* short - "bin-rel"
* binary relation := `R = (A, B, G)`
* a binary relation is an element of the powerset `P(A × B)`

homogenous, heterogenous

* homogenous := `(Si == Sj)` for any `i,j in [1,n]`
* heterogenous := `(Si != Sj)` for one or more `i,j in [1,n]`

related-to

* `(a related-to b)`, if `aRb` and/or `bRa`
* `a` is related to `b`, and `b` is related to `a`
* synonymous - strictly related, directly related

domain - a type-based view

* `dom(R) := G` for some `G in P(A × B)`
* `type(R) := (A × B)`
* `dom(R) subset-of type(R)`

domain - a function-based view (default)

* set of departure `A`
* set of destination `B` (codomain)
* `dom(R) := { x | xRy for at least one y in B }`
* `range(R) := { y | xRy for at least one x in A }`
* `field(R) := (dom(R) + range(R))`