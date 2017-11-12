
# Relations

<!-- ======================================================================= -->
## n-ary relation

* `S,S1,...,Sn` represent sets of sorts
* `R = (S1,...,Sn,G)`
* e.g. `Si := Nat`, `G := {(1,2), (2,3), ...}`
* `n` is the number of slots, places
* `n` is the arity or dimension of relation `R`
* `R` is itself a (n+1)-tuple (aka. correspondence)
* `Si` are the domains of `R`
* `G(R) subset-of XSi` is the relation's graph
* `XSi <=> xSi` if all sets are sets of atomic values
* `G(R) subset-of XS^n` if `Si := S` for any `i in [1,*]` -
  aka. an n-ary relation over `S`
* `chi(XSi), R(XSi) := (S1,...,Sn) -> boolean`
* `R(XSi)` returns true, if `s in XSi` is in the relation `R`
* `R(XSi)` is the characteristic function of `R` -
  aka. indicator function, n-place predicate
* `s in R` is a tuple, aka. an individual

clarifictaion

* `Ra` denotes an unary relation, aka. a property
* `Rab` or `aRb` a binary relation
* `Rabc` a ternary relation

functional perspective

* some relation `R` can be seen to define a function
* e.g. `R := (A X B)` => `f : A -> B`
* e.g. `R := xT^n` => `f: xT^(n-1) -> Tn`
* a function `f` is a special kind of relation
* however, this perspective is of no interest
* of interest is that `R` represents a set of tuples/sequences

<!-- ======================================================================= -->
domain of R

* non-standard, `dom(R) := S1,...,Sn = XSi`

other

* `V` and any `Vi` are sets of values
* `V1xV2`/`V1xV2xV3`/`V1x...xVN` - binary/ternary/n-ary domain
* `R subset-of V1x...xVN` is an n-ary relation
* `(#r == N)` for any `r in R`

<!-- ======================================================================= -->
## inverse relation

* `R = (S1,...,Sn,G)`
* `R', (R)', inv(R) := (Sn,...,S1,inv(G))`
* `inv(inv(R)) <=> R`

<!-- ======================================================================= -->
## binary relation

* `G(R) subset-of (A X B)`
* "a is R-related to b", if `(a,b) in R` for `(a in A) and (b in B)`

clarification

* `inv(a parent-of b) -> (b child-of a)`
* `inv(a contains b) -> (b element-of a)`
