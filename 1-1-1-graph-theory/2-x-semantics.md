
<!-- ======================================================================= -->
# Semantics of a relation

* without any meaning, a relation is just another set of sequences/tuples
* the semantics of a relation defines its orientation/direction and meaning
* put differently, the semantics of a relation adds meaning to its tuples

examples

* parent-of <=> child-of
* contains <=> element-of
* super-set-of <=> sub-set-of
* super-sequence-of <=> sub-sequence-of

<!-- ======================================================================= -->
## inverse (°,inv)

* `R := (S1,...,Sn,G)`
* `R°, inv(R) := (Sn,...,S1,inv(G))`
* `R°, inv(R) := (B,A,H)` such that `H := { (b,a) | aRb }`

clarification

* `inv(inv(R)) <=> R`
* this does not state anything about the semantics
* it merely states that the tuples are flipped (upside down)

clarification

* inverting a relation usually drops the initial semantics
* the inverted relation has no meaning under the initial semantics
* that is because the order of elements has changed

<!-- ======================================================================= -->
## palindromic

palindromic relation

* `sem(R)` := (`a` is identical to `b`)
* `R` and `inv(R)` both have a the exact same semantics

<!-- ======================================================================= -->
## semantics

semantics

* `sem(R) := <statement>` or simply `R := <statement>`
* a relation has no meaning under a given statement,
  if that statement does not apply to some `(s in R)`
* a statement must apply to all `(r in R)`

examples for `R in (A × B)`

* `a` knows `b`
* `a` is smaller than `b`
* `a` is pre-sequent to `b`
* `a` contains `b`
* `a` is an element of `b`
* `a` is a subset of `b`

examples for `R in (A × B × C)`

* `a` and `b` are the biological parents of `c`
* `c` is the sum of `a` and `b` - `R: (A,B) -> C` 
* `a` is the sum of `b` and `c` - `R: (A) -> (B,C)`

the order of elements is relevant to the semantics of a relation

* `R in (A × B × C)` := `c` is the sum of `a` and `b`
* i.e. the 3rd element is the sum of the 1st and 2nd element
* not - `inv(R) in (C × B × A)` => `a` is the sum of `c` and `b`
* but - `inv(R) in (C × B × A)` => `c` is the sum of `a` and `b`
* i.e. the 1st element is the sum of the 2nd and 3rd element
* e.g. `(1,2,3)` vs. `(3,2,1)`

<!-- ======================================================================= -->
## antonymous relation

relation `S` is antonymous to `R`

* `S := ant(R)`, if `(S == inv(R))` and
* `sem(S)` is antonymous to `sem(R)`

if `S` is antonymous to `R`, then `R` is also antonymous to `S`

* `(S == ant(R)) <=> (R == ant(S))`

examples for `R,S in (A × B)` that have antonymous semantics

* assume `R:=(A,B,G)` and `S:=(B,A,G°)`
* `R` := (`a` is a subset of `b`), and
  `S` := (`b` is a superset of `a`)
* `R` := (`a` contains `b`), and
  `S` := (`b` is an element of `a`)
* `R` := (`a` divides `b` without remainder), and
  `S` := (`b` is a multiple of `a`)

examples for `R,S in (A × B × C)` that have antonymous semantics

* assume `R := (A,B,C,G)` and `S := (C,B,A,G)`
* `R` := (`a` and `b` are the biological parents of `c`), and
  `S` := (`c` is a biological child of `b` and `a`)

`R` and `inv(R)` are not necessarily antonymous to each other

* assume `R := (A,B,C,G)` and `T := (C,B,A,G) := inv(R)`
* `R` := (set `c` is the intersection of sets `a` and `b`) =: `T`
* where `(R: (A,B) -> C)` and `(T: C -> (B,A))`

**Memory hook**
Antonymous relations require antonymous semantics.
