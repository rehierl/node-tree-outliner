
<!-- ======================================================================= -->
# Non-standard definitions

* mixed, non-standard, relation-based definitions

<!-- ======================================================================= -->
## domain (D) of relation (R)

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
