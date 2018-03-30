
<!-- ======================================================================= -->
# Operations on binary relations

<!-- ======================================================================= -->
## contained-in

* `R,S := (A,B,G)`
* `(R contained-in S)` := `aSb` for any `aRb`
* signature - (relation,relation) -> boolean

clarification

* so similar to the definition of "subset"?

<!-- ======================================================================= -->
## inverse (',inv)

* `R := (A,B,G)`
* `R', inv(R) := (B,A,H)` such that `H := { (b,a) : aRb }`
* signature - (relation) -> relation

clarification

* `(R == R')` if `R` is symmetric

<!-- ======================================================================= -->
## union (+, or)

* `(R + S), (R or S) := { (a,b) : aRb or aSb }`
* signature - (relation,relation) -> relation

<!-- ======================================================================= -->
## intersection (&, and)

* `(R & S), (R and B) := { (a,b) : aRb and aSb }`
* signature - (relation,relation) -> relation

<!-- ======================================================================= -->
## transitive closure

* `R+, +(R), trans(R) := S` such that it contains `R` and is transitive
* `R := (A,A,G) -> S := (A,A,G)`
* signature - (relation) -> relation

clarification

* essentially continue to add `(a,c)` to `R`
  for any pair `aRb` and `bRc` until `R` is transitive
* allows to answer if `c` can be reached starting from `a`

<!-- ======================================================================= -->
## reflexive closure

* `S := R + { (a,a) : a in A }`
* requires `R := (A,A,G)`, i.e. `(B == A)`
* signature - (relation) -> relation

<!-- ======================================================================= -->
## reflexive reduction

* `S := R \ { (a,a) : a in A }`
* requires `R := (A,A,G)`, i.e. `(B == A)`
* signature - (relation) -> relation

<!-- ======================================================================= -->
## composition

* `R := (A,B,G), S := (B,C,H)`
* `comp(S,R) := { (a,c) : aRb and bSc }`
* `comp(S,R)` similar to `S(R)`
* signature - (relation,relation) -> relation

clarification

* `comp(parent-of, mother-of)` -> `maternal-grandparent-of`
* `comp(mother-of, parent-of)` -> `grandmother-of`

<!-- ======================================================================= -->
## complement

* `comp(R) := (R) -> S`
* `R:=(A,B,G) => S:=(A,B,H)` such that if `!aRb` then `aSb`
* `comp(R) := S` is the complement relation to `R`
* `(comp(inv(R)) == inv(comp(R)))`
* signature - (relation) -> relation

clarification, if `(A == B)`

* `R` is symmetric => `comp(R)` is symmetric
* `R` is reflexive <=> `comp(R)` is irreflexive

<!-- ======================================================================= -->
## restriction

* `restrict(R), limit(R) := (R) -> S`
* `R := (A,B,G)` and `B subset-of A`
* `limit(R) := (B,B,G)` such that `aRb` where `a in B`
* signature - (relation) -> relation

clarification

* if `R` is ...
* ..., reflexive, irreflexive, symmetric, asymmetric, transitive, total, ...
* ..., trichotomous, partial order, total order, strict weak order, ...
* ..., total preorder (weak order), equivalence relation,
* then `limit(R)` is too
 
