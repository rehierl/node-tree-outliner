
<!-- ======================================================================= -->
# Properties of binary relations

* note - "a, b" is short for "a and b"

implications

* strict <-> irreflexive
* transitive, symmetric, serial -> reflexive
* transitive, asymmetric -> irreflexive
* transitive, irreflexive -> asymmetric

a-symmetric vs. irreflexive, anti-symmetric

* a-symmetric -> irreflexive, anti-symmetric
* a-symmetric <?- irreflexive, anti-symmetric
* i.e. (<->) or only (->) ?

a relation has only on set of tuples and one "semantics" only

* tuples manifest the semantics of relation `R`
* a relation has one semantics/statement only
* e.g. "<" xor "<=" xor "==" xor ">=" xor ">"
* if (sem(R) := "<") and ((a,b) !in R), then (a,b) is undecided - a tie
* i.e. not automatically ">=" - in that R, ">=" is "undefined"

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

<!-- ======================================================================= -->
## properties

* `R := (A,A,G)`
* must be homogenous?
* endo-relation - binary and homogeneous
* universal relation U - `(A x A)` or `{ aRb | (a,b in A) }`
* identity relation I - `{ aRa | (a in A) }`

### reflexive

* `aRa` for all `(a in A)`
* i.e. there is no `a` such that `!aRa`
* i.e. any `a` is strictly related to itself
* e.g. "is equal to"

### irreflexive, strict

* no `aRa` for any `(a in A)`
* i.e. there is no `a` such that `aRa`
* e.g. "greater than"

clarification

* if `aRa` or `!aRa` for some `(a in A)`,
* then neither reflexive nor irreflexive

### coreflexive

* if `aRb`, then `(a == b)`
* i.e. no `aRb` such that `(a != b)`
* `(R subset-of I)` if `R` is coreflexive
* e.g. "identical to"

### quasi-reflexive

* if `aRb`, then `aRa` and `bRb`

### symmetric

* if `aRb`, then also `bRa`
* i.e. no strict orientation/direction
* e.g. "is equal to"

clarification

* symmetric => `(inv(R) == R)` => palindromic

### anti-symmetric

* if `aRb` and `bRa`, then `(a == b)`
* `aRa` is allowed, but not required
* if `aRb` and `(a != b)`, then `!bRa`
* e.g. "greater or equal"

### a-symmetric

* if `aRb`, then `!bRa`
* `aRa` is no longer allowed
* e.g. "greater than"

### transitive

* if `aRb` and `bRc`, then also `aRc`
* e.g. "is ancestor of"

### connex

* for any pair it holds that `aRb` or `bRa` or both
* i.e. any pair is related/comparable - i.e. total ?
* also, any connex relation is reflexive
* originates from order theory

### semi-connex

* for any pair `(a != b)` it holds that `aRb` or `bRa`
* note - `(!a -> b)` <=> `(a or b)` <=!=> `(a -> !b)`
* `aRa` is allowed, but not required

### trichotomous

* if `aRb` xor `bRa` xor `(a == b)`
* i.e. if `(a == b)`, then `!aRb` and `!bRa`
* i.e. `!aRa` for any `a` => irreflexive
* e.g. "greater than"

### serial

* for any `a`, there is a `b` such that `aRb`
* e.g. intervals (open or closed) combined with (<) or (<=)
* e.g. in `[*,1]` there is no `n` such that `(1 < n)`
* e.g. in `[1,*]` there is no `n` such that `(n < 1)` - not required?

<!-- ======================================================================= -->
## "euclidean" property

```
right-euclidean   left-euclidean
---------------   --------
  c               a
 /                 \
a |               | c
 \                 /
  d               b
```

right-euclidean, euclidean

* if `aRc` and `aRd`, then also `cRd`
* e.g. "equality"

left-euclidean

* if `aRc` and `bRc`, then also `aRb`

<!-- ======================================================================= -->
## set-like/local relation

* relation over a set X
* for every (x in X), the class of all (y in X) such that yRx is a set
* e.g. the usual ordering < on the class of ordinal numbers is set-like

<!-- ======================================================================= -->
## well-founded relation

* relation over a set X
* a well-founded relation on a class X is a binary relation R
* if every non-empty subset (S subset-of X) has a minimal element in R
* i.e. an element m not related by sRm
