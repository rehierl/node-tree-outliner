
<!-- ======================================================================= -->
# Operations on sets

* (/see/ "operations on groups" /)

<!-- ======================================================================= -->
## wikipedia, union (+, or, union)

* `(A union B) := { x | (x in A) or (x in B) }`
* `(A or B), (A + B) := (A union B)`

likewise

* `(A + b) := (A + {b})`
* `(a + B) := ({a} + B)`
* `(a + b), ({a} + {b}) := {a, b}`

clarification

* identity element {} - `(A + {}) = A`
* finite union - the union over a finite number of sets
* i.e. the union set may still be infinite

commutative, associative

* `(A + B) = (B + A)`
* `((A + B) + C) <-> (A + (B + C))`

multi-set operation - +(), E()

* if `S` is a set of sets, then ...
* `+(S)` or `E(S)` is the union over all sets in `S`
* i.e. `(x in +(S))`, iff `(x in s)` for one or more `(s in S)`
* note - `+({}) := {}`

<!-- ======================================================================= -->
## wikipedia, intersection (&, and, isect)

* `(A isect B) := { x | (x in A) and (x in B) }`
* `(A & B), (A and B) := (A isect B)`

intersect, disjoint

* intersect - `(A & B) != {}`
* disjoint - `(A & B) == {}`

commutative, associative

* `(A & B) = (B & A)`
* `((A & B) & C) = (A & (B & C))`

distributive

* `A & (B + C) = (A & B) + (A & C)`
* `A + (B & C) = (A + B) & (A + C)`

multi-set operation - &()

* if `S` is a set of sets, then ...
* `&(S)` is the intersection over all sets in `S`
* i.e. `(x in &(S))`, iff `(x in s)` for all `(s in S)`
* note - `&({}) := U` - i.e. the universal set

One way of putting it would be that there is no `s` in `S` such that `x`
could not be an element, i.e. the "requirement" can not be violated by
any possible element.

* `&(S) subset-of U` is obviously true
* use `+(S)` as a replacement for `U`
* `&(S) subset-of +(S)` is also true
* `&(S) := { (x in +(S)) | (x in s) for all (s in S) }`

<!-- ======================================================================= -->
## wikipedia, complement (*)

* all sets are understood to be subsets of a universal set U
* (absolute) complement - A* := (U \ A)
* i.e. remove all elements of A from U
* relative complement - (B \ A)
* i.e. remove all element of A from B
* i.e. the relative complement of A in regards to B

properties

* (A + B)* = A* & B*
* (A & B)* = A* + B*
* (A & B) = (A* + B*)*
* U = (A + A*)
* {} = (A & A*)
* {}* = U
* U* = {}
* A = (A*)* - aka. involution
* (A strict-subset-of B) => (B* strict-subset-of A*)

<!-- ======================================================================= -->
## set difference (\, sub, diff)

* `(A diff B) := { x | (x in A) and (x !in B) }`
* `(A \ B), (A sub B), (A - B) := (A diff B)`

note that ...

* there doesn't seem to be a wikipedia page dedicated to the set difference
* this operation is however also known as the "relative complement" (see below)

<!-- ======================================================================= -->
## wikipedia, symmetric difference (^, xor, ex-or)

* `(A ex-or B) := { x | x in (A\B or B\A) }`
* `(A ^ B), (A xor B) := (A ex-or B)`

clarification

* `(A xor B) := (A \ B) or (B \ A)`
* `(A xor B) := (A or B) \ (A & B)`
* `(A ^ {}) = A`
* `(A ^ A) = {}`

commutative, associative

* `(A ^ B) = (B ^ A)`
* `((A ^ B) ^ C) = (A ^ (B ^ C))`
