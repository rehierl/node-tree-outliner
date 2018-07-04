
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
* i.e. only one income - only one way to get to `c`

### right-unique, functional

* if `aRc` and `aRd`, then `(c == d)`
* i.e. there is no `a` such that `aRc` and `aRd` for `(c != d)`
* i.e. only one outcome

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

### reflexive

* `aRa` for all `a in A`
* i.e. there is no `a` such that `!aRa`
* i.e. any `a` is strictly related to itself
* e.g. "is equal to"

### irreflexive, strict

* `!aRa` for any `a`
* i.e. there is no `a` such that `aRa`
* i.e. no `a` is related to itself
* e.g. "greater than"

clarification

* if `aRa` xor `!aRa` for some, but not all `a`
* then neither reflexive nor irreflexive

### coreflexive

* if `aRb`, then `(a == b)`

### symmetric

* if `aRb`, then also `bRa`
* i.e. no strict orientation/direction
* e.g. "is equal to"

clarification

* symmetric => `(inv(R) == R)` => palindromic

### anti-symmetric

* if `aRb` for `(a != b)`, then `!bRa`
* if `aRb` and `bRa`, then `(a == b)`
* note - `aRa` is allowed, but not required
* note - `aRa` does not count towards `aRb` and `bRa`
* e.g. "greater or equal"

### a-symmetric

* if `aRb`, then `!bRa`
* e.g. "greater than"

### transitive

* if `aRb` and `bRc`, then also `aRc`
* e.g. "is ancestor of"

### connex

* if `aRb` or `bRa` or both
* i.e. any pair is comparable (i.e. total?)
* also implies reflexivity

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

### right-euclidean, euclidean

* if `aRc` and `aRd`, then also `cRd`
* unclear - and also `bRa` ?
* e.g. "equality"

### left-euclidean

* if `aRc` and `bRc`, then also `aRb`
* unclear - and also `bRa` ?
