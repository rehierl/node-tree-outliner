
<!-- ======================================================================= -->
# Relations

* `S,S1,...,Sn` represent sets of sorts
* `R = (S1,...,Sn,G)`
* e.g. `Si := Nat`, `G := {(1,2), (2,3), ...}`
* `n` is the number of slots, places
* `n` is the arity or dimension of relation `R`
* `R` is itself a (n+1)-tuple (aka. correspondence)
* `R` is an n-ary relation
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

clarification

* `Ra` denotes an unary relation, aka. a property
* `Rab` or `aRb` a binary relation
* `Rabc` a ternary relation

definitions

* sequence `r in R`, if `r in G(R)`
* `Rab` or `aRb` is true, if `(a,b) in R`
* `!Rab` or `!aRb` is true, if `(a,b) not in R`
* relation `R subset-of X`, if `r in X` for any `r in R`
* as a matter of simplification `R in X` if `R subset-of X`
* relation `R` contains sequence `r`, if `r in G`
* similar definitions for `sequence-of`, etc.

clarification

* all sequences have the same length -
  i.e. `(#r == N)` for any `r in R`

homogenous, heterogenous relation

* homogenous <=> `(Si == Sj)` for any `i,j in [1,n]`
* heterogenous <=> `(Si != Sj)` for some or any `i,j in [1,n]`
* (not homogenous => heterogenous), but (not heterogenous !> homogenous)

<!-- ======================================================================= -->
## domain, type

* for `R = (S1,...,Sn,G)`
* `dom(R) := G`
* `type(R) := xSi` such that `G in xSi`
* `dom(R) subset-of type(R)`

<!-- ======================================================================= -->
## semantics

* without any meaning, a relation is just a set of sequences

semantics

* `sem(R) := <statement>` or simply `R := <statement>`
* these kind of expressions state, that
  "statement" applies to all `r in R`
* the relation has no meaning under a given statement, if
  that statement does not apply to some `s in R`

examples for `R in (A X B)`

* `a` knows `b`
* `a` is smaller than `b`
* `a` is presequent to `b`
* `a` contains `b`
* `a` is an element of `b`
* `a` is a subset of `b`

examples for `R in (A X B X C)`

* `a` and `b` are the biological parents of `c`
* `c` is the sum of `a` and `b` - `R: (A,B) -> C` 
* `a` is the sum of `b` and `c` - `R: (A) -> (B,C)`

the order of elements is relevant for the semantics of a relation

* `R in (A X B X C)` := `c` is the sum of `a` and `b`
* i.e. the 3rd element is the sum of the 1st and 2nd elements
* not - `inv(R) in (C X B X A)` := `a` is the sum of `c` and `b`
* but - `inv(R) in (C X B X A)` := `c` is the sum of `a` and `b`
* i.e. the 1st element is the sum of the 2nd and 3rd elements
* e.g. `(1,2,3)` vs. `(3,2,1)`

<!-- ======================================================================= -->
## inverse relation

* `R := (S1,...,Sn,G)`
* `R', (R)', inv(R) := (Sn,...,S1,inv(G))`

clarification

* `inv(inv(R)) <=> R`
* this does not state anything about the semantics
* it merely states that the tuples are turned upside down

<!-- ======================================================================= -->
## palindromic relation

palindromic relation

* `sem(R)` := (`a` is identical to `b`)
* `R` and `inv(R)` both have a the exact same semantics

<!-- ======================================================================= -->
## antonymous relations

relation `S` is antonymous to `R`

* `S := ant(R)`, if `(S == inv(R))` and
* `sem(S)` is antonymous to `sem(R)`

if `S` is antonymous to `R`, then `R` is also antonymous to `S`

* `(S == ant(R)) <=> (R == ant(S))`

examples for `R,S in AxB` that have antonymous semantics

* assume `R:=(A,B,G)` and `S:=(B,A,G')`
* `R` := (`a` is a subset of `b`), and
  `S` := (`b` is a superset of `a`)
* `R` := (`a` contains `b`), and
  `S` := (`b` is an element of `a`)
* `R` := (`a` divides `b` without remainder), and
  `S` := (`b` is a multiple of `a`)

examples for `R,S in AxBxC` that have antonymous semantics

* assume `R:=(A,B,C,G)` and `S:=(C,B,A,G)`
* `R` := (`a` and `b` are the biological parents of `c`), and
  `S` := (`c` is a biological child of `b` and `a`)

`R` and `inv(R)` are not necessarily antonymous to each other

* assume `R:=(A,B,C,G)` and `T:=(C,B,A,G):=inv(R)`
* `R` := (set `c` is the intersection of sets `a` and `b`) =: `T`
* where `R: (A,B) -> C` and `T: (C) -> (B,A)`
* an antonymous relation requires antonymous semantics

<!-- ======================================================================= -->
## a functional perspective

* some relation `R` can be seen to define a function
* e.g. `G(R) = (A X B)` => `f : A -> B`
* e.g. `G(R) = xT^n` => `f: xT^(n-1) -> Tn`
* a function `f` is a special kind of relation
* however, this perspective is of no interest here
* of interest is, that `R` represents a set of tuples/sequences

standard perspective

* `f : A -> B`
* `A` is said to be the function's domain
* `B` is said to be the function's codomain, aka. target set
* `f(a) = b`, `(a in A) and (b in B)`, `f(a)` evaluates to `b`
* here, `a` represents the function's argument and
  `f(a)` the function's value for argument `a`

domain

* the domain of a function `dom(f)` is
  the set of input/argument values for which the function is defined
* for each `a in dom(f)`, `f(a)` evaluates to some `b in B`
* `a` is mapped onto `b` under `f`
* `b` is `a`'s image under `f`
* however, `dom(f)` is not necessarily the same as `A` -
  i.e. `dom(f)` can be a strict subset of `A`
* there does not seem to be a dedicated name for `A`

codomain

* `B` is said to be the function's codomain
* an image is a subset of a function's codomain - i.e. `img(f) subset-of B`
* `f` is surjective - `a in A` exists for any `b in B` such that `f(a)=b`
* surjective => `(img(f) == B)`

image

* `img(X,f) = { f(a) : (a in X), (X subset-of A) }` -
  i.e. the set of values that contains all possible output/result values
* subset `X` of `A` => image of `X` under `f`
* `img(f) := img(dom(f),f)` is referred to as the function's image

inverse image

* `img(Y,f) = { a : (f(a) == b), (a in A), (b in Y), (Y subset-of B) }` -
  i.e. all elements in `A` that are mapped into `Y`
* synonymous - inverse image, pre-image

range

* refers to either the codomain or the image of `f`
* the latter is the more strict use of the word "range"
* codomain > range > image
* `f : dom(f) -> rng(f)`
