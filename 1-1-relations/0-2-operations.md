
<!-- ======================================================================= -->
# Operations on binary relations

a hunch

* `R := (A,B,G)` if `(A != B)`
* has characteristics of a function, "depth" is 2
* `R := (A,A,G)` if `(A == B)`
* has characteristics of a function, if "depth" is "limited" to 2
* `R := (A,A,G)` i.e. `(A == B)`
* an "order" seems to involve all elements in `A` - "total" in some way

<!-- ======================================================================= -->
## composition

* `R := (A,B,G), S := (B,C,H)`
* `comp(S,R) := { (a,c) : aRb and bSc }`
* right-to-left order of operands - i.e. left-after-right
* `comp(S,R)` similar to `S(R)`

<!-- ======================================================================= -->
## contains

* `(R contains S)` := `aSb` for any `aRb`
* e.g. (<) is contained in (<=)

<!-- ======================================================================= -->
## union (+, or)

* `(R + S), (R or S) := { (a,b) : aRb or aSb }`

<!-- ======================================================================= -->
## intersection (&, and)

* `(R & S), (R and B) := { (a,b) : aRb and aSb }`

<!-- ======================================================================= -->
## reflexive closure

* `S := R + { (a,a) | a in A }`
* requires `R := (A,A,G)`, i.e. `(B == A)`

<!-- ======================================================================= -->
## reflexive reduction

* `S := R \ { (a,a) : a in A }`
* requires `R := (A,A,G)`, i.e. `(B == A)`

<!-- ======================================================================= -->
## transitive closure

* `S` := smallest transitive relation containing `R`

clarification

* essentially continue to add `(a,c)` to `R`
  for any pair `aRb` and `bRc` until `R` is transitive
* allows to answer if `c` can be reached beginning with `a`

clarification

* reflexive transitive closure - smallest preorder containing `R`
* i.e. transitive closure, then reflexive closure
* reflexive transitive symmetric closure - smallest equivalence relation

<!-- ======================================================================= -->
### converse, transpose

* `S := { (b,a) | aRb }`
* (S == R) <-> (is-symmetric R)

clarification

* same as "inv()"?

<!-- ======================================================================= -->
## complement

* `comp(R), S := { (a,b) | !aRb }`
* `comp(R) := S` is the complement relation to `R`

clarification

* same as "converse"?
* similar to sets `comp(A) = U \ A`
* `(comp(inv(R)) == inv(comp(R)))`

clarification, if `(A == B)`

* `R` is symmetric -> `comp(R)` is symmetric
* `R` is reflexive <-> `comp(R)` is irreflexive
* `R` is a strict weak order <-> `comp(R)` is a total preorder

<!-- ======================================================================= -->
## restriction

* `restrict(R), limit(R) := (R) -> S`
* `limit(R) := (B,B,G)` such that `aRb` where `a, in B`
* i.e. restrict `R := (A,A,G)` to `B subset-of A`

clarification

* if `R` is ... (or-combined)
* ..., reflexive, irreflexive, symmetric, asymmetric, transitive, total, ...
* ..., trichotomous, partial order, total order, strict weak order, ...
* ..., total preorder (weak order), equivalence relation,
* then `limit(R)` is too
 
