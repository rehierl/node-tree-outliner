
<!-- ======================================================================= -->
# Classification of binary relations

* assume - `R := (A,B,G)`

<!-- ======================================================================= -->
## unique, total

* `(A == B)` is allowed, but not required
* i.e. `A` and `B` may be different sets

clarification

* functional and left-total => a function
* a function and injective => injective function
* a function and right-total => surjective function (also surjection)
* function, surjective, injective => bijection (also 1:1 correspondence)

### injective

* if `aRc` and `bRc`, then `(a == b)`
* i.e. there is no `c` such that `aRc` and `bRc` for `(a != b)`
* i.e. no `b` has two or more predecessors
* also - left-unique

### functional

* if `cRa` and `cRb`, then `(a == b)`
* i.e. there is no `c` such that `cRa` and `cRb` for `(a != b)`
* i.e. no `a` has two or more successors
* also - univalent, right-unique, right-definite

clarification

* partial function - `f` is undefined for some `a in A`
* total function - `f` is defined for any `a in A`
* if partial, then total with regards to some strict-subset-of `A`

### one-to-one, 1:1

* if injective and functional, then 1:1

### left-total

* for any `a`, there is a `b` such that `aRb`
* i.e. any `a` has at least one successor `b`

### right-total, surjective

* for any `b`, there is an `a` such that `aRb`
* i.e. any `b` has at least one predecessor `a`
* not surjective => `img(f) strict-subset-of B`, i.e. (image != codomain)
* also - right-total, onto

<!-- ======================================================================= -->
## properties

* `(A == B)` is required

clarification

* reflexive, antisymmetric, transitive => partial order
* partial order, total => simple order (also linear order, chain)
* reflexive, symmetric, transitive => equivalence relation
* symmetric, transitive, serial => reflexive
* symmetric, transitive => partial equivalence relation

### reflexive

* `aRa` for all `a in A`
* i.e. there is no `a` such that `(a,a) not in R`
* i.e. any `a` is also strictly related to itself

### irreflexive

* `!aRa` for any `a`
* i.e. there is no `a` such that `aRa`
* i.e. no `a` is strictly related to itself
* also - strict

clarification

* `aRa` or `!aRa` for some, but not all `a`
* is neither reflexive nor irreflexive

### coreflexive

* if `aRb`, then `(a == b)`

### symmetric

* if `aRb`, then also `bRa`
* i.e. if `r in R`, then also `inv(r) in R`
* i.e. no strict direction

clarification

* symmetric => `(inv(R) == R)` => palindromic

### antisymmetric

* if `aRb` and `bRa`, then `(a == b)`
* i.e. has no pair `aRb` and `bRa` such that `(a != b)`
* e.g. (>=)

### asymmetric

* if `aRb`, then `!bRa`
* i.e. asymmetric => antisymmetric, irreflexive
* e.g. (>)

### transitive

* if `aRb` and `bRc`, then also `aRc`
* transitive, asymmetric => irreflexive

### total, complete

* for any pair (`aRb` or `bRa` (or both)) is true
* i.e. any two elements are strictly related
* not the same as - `aRb` for any pair of values

### trichotomous

* for any pair (`aRb` xor `bRa` xor `(a == b)`) is true
* i.e. if `(a == b)`, then neither `aRb` nor `bRa` is true
* i.e. `!aRa` for any `a` => irreflexive

### right-euclidean

* if `cRa` and `cRb`, then also `aRb`
* unclear - and also `bRa` ?

### left-euclidean

* if `aRc` and `bRc`, then also `aRb`
* unclear - and also `bRa` ?

### euclidean

* if left- and right-euclidean

### serial

* for any `a`, there is a `b` such that `aRb`
* ?!? so similar to left-total ?!?
