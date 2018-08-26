
<!-- ======================================================================= -->
# Operations on binary relations

* (/see/ "wikipedia, binary relations" /)

an impression, a hunch

* `R := (A,B,G)` if `(A != B)`
* has characteristics of a function, "depth" is 2
* `R := (A,A,G)` if `(A == B)`
* has characteristics of a function, if "depth" is "limited" to 2
* `R := (A,A,G)` i.e. `(A == B)`
* an "order" seems to involve all elements in `A` - "total" in some way

<!-- ======================================================================= -->
## contains

* (R contains S) := aSb for all aRb
* e.g. (<) is contained in (<=)

<!-- ======================================================================= -->
## wikipedia, composition (¤)

* for R:=(A,B,G) and S:=(B,C,H)
* (S ¤ R), comp(S,R) := { (a,c) | aRb and bSc }
* i.e. in right-to-left order, right-before-left, left-after-right
* i.e. same order as in the composition of functions

<!-- ======================================================================= -->
## union (+, or)

* `(R + S), (R or S) := { (a,b) : aRb or aSb }`

<!-- ======================================================================= -->
## intersection (&, and)

* `(R & S), (R and B) := { (a,b) : aRb and aSb }`

<!-- ======================================================================= -->
## reflexive closure

* `S := R + { (a,a) | (a in A) }`
* requires R:=(A,A,G), i.e. (A == B)

<!-- ======================================================================= -->
## reflexive reduction

* `S := R \ { (a,a) | (a in A) }`
* requires R := (A,A,G), i.e. (A == B)

<!-- ======================================================================= -->
## wikipedia, transitive closure

* S is the transitive closure of R, if
* S is the smallest transitive relation containing R

remarks

* essentially continue to add `(a,c)` to `R`
  for any pair `aRb` and `bRc` until `R` is transitive
* allows to answer if `c` can be reached from `a`
* e.g. the "less than or equal" relation on a linearly ordered set

reflexive transitive closure

* reflexive transitive closure - smallest preorder containing `R`
* note - first the transitive closure, then the reflexive closure
* reflexive transitive symmetric closure - smallest equivalence relation

<!-- ======================================================================= -->
## wikipedia, transitive reduction

* transitive reduction R of a directed graph D
* same vertices and as few edges as possible
* for each (u,..,v) path in D, there is a (u,..,v) path in R
* i.e. R and D have the same reachability relation

directed (acyclic) graphs

* R of a DAG is unique and a subgraph of D
* i.e. R is not necessarily a subgraph of a non-DAG (cycles)
* i.e. if D has cycles, then R is not unique

<!-- ======================================================================= -->
## wikipedia, converse/transpose/inverse (°)

* `S, conv(R), inv(R) := { (b,a) | aRb }`
* i.e. the order of vertices of each edge is flipped
* analogous to inverse functions
* note - every relation has a unique converse
* (S == R) <-> (is-symmetric R)

clarification

* if `R` is ... (or-combined)
* ..., reflexive, irreflexive, symmetric, antisymmetric, asymmetric, ...
* ..., transitive, total, trichotomous, partial order, total order, ...
* ..., strict weak order, total preorder, equivalence relation,
* then `conv(R)` is too

inverses

* for I being the identity relation
* R is right-invertible, if X exists such that (R ¤ X) = I
* R is left-invertible, if Y exists such that (Y ¤ R) = I
* X and Y are referred to as right/left inverses of R
* R is invertible if X and Y exist

inverses for homogenous relations

* X and Y coincide - i.e. are identical
* for an endo-relation R:=(X,X,G), R° is its inverse
* i.e. transpose = inverse

related to functions

* a function is invertible, iff its converse relation is a function
* i.e. only then is the function's converse also its inverse

<!-- ======================================================================= -->
## complement

* `comp(R)` := is the complement relation to R
* `comp(R) := { (a,b) | !aRb }`
* comp(inv(R)) = inv(comp(R))

if (A == B)

* R is symmetric -> comp(R) is symmetric
* R is reflexive <-> comp(R) is irreflexive
* R is a strict weak order <-> comp(R) is a total preorder

clarification

* similar to sets: comp(A) = (U \ A)
* universal relation U:=(A × B)

<!-- ======================================================================= -->
## restriction

* `restrict(R), limit(R) := (R) -> S`
* `limit(R) := (B,B,G)` such that `aRb` where `(a in B)`
* i.e. restrict `R := (A,A,G)` to `(B subset-of A)`

clarification

* if `R` is ... (or-combined)
* ..., reflexive, irreflexive, symmetric, asymmetric, transitive, total, ...
* ..., trichotomous, partial order, total order, strict weak order, ...
* ..., total preorder (weak order), equivalence relation,
* then `limit(R)` is too
