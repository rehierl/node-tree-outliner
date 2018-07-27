
<!-- ======================================================================= -->
# Properties of binary relations (1)

* note - notes taken from "wikipedia, binary relations"
* note - "a, b" is short for "a and b"

implications

* strict <-> irreflexive
* a-symmetric <-> irreflexive, anti-symmetric
* transitive, symmetric, serial -> reflexive
* transitive, asymmetric -> irreflexive
* transitive, irreflexive -> asymmetric

a relation has only one set of tuples and one "semantics"

* tuples manifest the semantics of a relation
* e.g. "<" xor "<=" xor "==" xor ">=" xor ">"
* if (sem(R) := "<") and (!aRb and !bRa), then (a,b) is undecided - a tie
* i.e. not automatically "==" because "==" is "undefined"

<!-- ======================================================================= -->
## types

* `R := (A,B,G)`
* not necessarily heterogenous

```
not           not            not          not
left-unique   right-unique   left-total   right-total
-----------   ------------   ----------   -----------
 a               c            a -- c       a -- c
  \             /
   c           a              b                 d
  /             \
 b               d
```

* `a,b in A` and `c,d in B`

### left-unique, injective

* if `aRc` and `bRc`, then `(a == b)`
* i.e. there is no `c` such that `aRc` and `bRc` for `(a != b)`
* i.e. no two elements have the same outcome `y`
* i.e. each `y` has no more than one income `x`

### right-unique, functional

* if `aRc` and `aRd`, then `(c == d)`
* i.e. there is no `a` such that `aRc` and `aRd` for `(c != d)`
* i.e. no two elements that have the same income `x`
* i.e. each `x` has no more than one outcome `y`

### left-total

* for any `a`, there is a `c` such that `aRc`
* i.e. each `a` has an outcome

### right-total, surjective, onto

* for any `c`, there is an `a` such that `aRc`
* i.e. any `b` has an income - can be reached

### combinations of uniqueness and totality

* unique, one-to-one, 1:1 - left-unique and right-unique
* total - left-total and right-total
* bijective - unique and total

<!-- ======================================================================= -->
## properties

* `R := (A,A,G)`
* must be homogenous?
* endo-relation - binary and homogeneous
* universal relation U - `(A × A)` or `{ aRb | (a,b in A) }`
* identity relation I - `{ aRa | (a in A) }`

### reflexive

* "all loops"
* `aRa` for all `(a in A)`
* i.e. there is no `a` such that `!aRa`
* i.e. any `a` is strictly related to itself
* e.g. "is equal to"

### irreflexive, strict

* "no loops"
* no `aRa` for any `(a in A)`
* i.e. there is no `a` such that `aRa`
* e.g. "greater than"

clarification

* if `aRa` or `!aRa` for some `(a in A)`,
* then neither reflexive nor irreflexive

### coreflexive

* "only loops"
* if `aRb`, then `(a == b)`
* i.e. no `aRb` such that `(a != b)`
* `(R subset-of I)` if `R` is coreflexive
* e.g. "identical to"

### quasi-reflexive

* "related with loops"
* if `aRb`, then `aRa` and `bRb`

### symmetric

* "undirectional, non-strict - possible loops"
* if `aRb`, then also `bRa`
* i.e. no strict orientation/direction
* e.g. "is equal to"

clarification

* symmetric => `(inv(R) == R)` => palindromic

### anti-symmetric

* "directional, non-strict - possible loops"
* if `aRb` and `bRa`, then `(a == b)`
* `aRa` is allowed, but not required
* if `aRb` and `(a != b)`, then `!bRa`
* e.g. "greater or equal"

### a-symmetric

* "directional, strict - no loops"
* if `aRb`, then `!bRa`
* `aRa` is no longer allowed
* e.g. "greater than"

### transitive

* if `aRb` and `bRc`, then also `aRc`
* e.g. "is ancestor of"

### connex

* "all related - all loops"
* for any pair it holds that `aRb` or `bRa` or both
* i.e. any pair is related/comparable - i.e. total ?
* also, any connex relation is reflexive
* originates from order theory

### semi-connex

* "all related, non-strict - possible loops"
* for any pair `(a != b)` it holds that `aRb` or `bRa`
* note - `(!a -> b)` <=> `(a or b)` <=!=> `(a -> !b)`
* `aRa` is allowed, but not required

### trichotomous

* "all related, strict - no loops"
* if `aRb` xor `bRa` xor `(a == b)`
* i.e. `!aRa` for any `a` => irreflexive
* e.g. "greater than"

<!-- ======================================================================= -->
## serial

* for any `a`, there is a `b` such that `aRb`
* e.g. intervals (open or closed) equipped with (<) or (<=)
* e.g. `R := ([1,*],<)` - serial - there always is a greater element
* e.g. `R := ([1,*],>)` - not serial - no `n` such that `(n < 1)`
