
# Sequence Algebra

<!-- ======================================================================= -->
## operators

* The letter `x` represents the cross product operator.

### (e1 x e2), and (e2 x e1)

`e1 x e2 := (e1,e2)`
`e2 x e1 := (e2,e1)`

* `(e1 x e2) != (e2 x e1)`

### axe, exa

`axe := (a1,...,ai,e)`,
`exa := (e,a1,...,ai)`
for sequence `a`, `(#a = i)` and some element `e`

* The result is a sequence.
* `(axe != exa)`

### axb, bxa

`axb := (a1,...,ai,b1,...,bj)`,
`bxa := (b1,...,bj,a1,...,ai)`
for sequences `a` and `b`, `(#a = i)`, `(#b = j)` and `i,j in [0,+Inf)`

* The result is a sequence gained from appending sequence `b` to sequence `a`.
* synonymous - concatenate, add, append
* `(axb != bxa)`

### (A = B), (A != B)

`(A = B) := (b in A, for any b from B) and (a in B, for any a from A)`
`(A != B) := not (A = B)`

* The usual definition for equality/inequality of sets of elements.

### axB, Axb

`axB := { axb | b in B }`,
`Axb := { axb | a in A }`
for sequences `a` and `b`, sets of sequences `A` and `B`

* The result is a set of sequences.
* In `axB`, any sequence in `B` is prefixed with sequence `a`.
* In `Axb`, any sequence in `A` is suffixed with sequence `b`.
* `(axB != Axb)`

### AxB, BxA

`AxB := { axb | a in A, b in B }`
`BxA := { bxa | a in A, b in B }`

* The result is a set of sequences.
* `(AxB != BxA)`

This is unlike the Cartesian product!

* `A X B := { (a,b) | a in A, b in B }`
* `(a,b)` is a sequence of sequences, but `axb` a flattened sequence

### miscellaneous

* `axbxC = (axb)xC = ax(bxC)`
* `axBxC = (axB)xC = ax(BxC)`
* `AxbxC = (Axb)xC = Ax(bxC)`
* `AxBxC = (AxB)xC = Ax(BxC)`

Any sequence `s` is the product of its elements `e1,...,eN`

* `s = (e1,...,eN) := e1 x e2 x ... x eN`

<!-- ======================================================================= -->
## infix, subsequence

* `t subsequence-of s`, if sequences `a` and `b` exist such that `axtxb = s`.

<!-- ======================================================================= -->
## prefix

* `a prefix-of b`, if a sequence `c` exists such that `axc = b`
* `a prefix-of B`, if `a prefix-of b` is true for any `b in B`
* `s = axb`, then `a prefix-of s`

<!-- ======================================================================= -->
## suffix

* `a suffix-of b`, if a sequence `c` exists such that `cxa = b`
* `a suffix-of B`, if `a suffix-of b` is true for any `b in B`
* `s = axb`, then `b suffix-of s`
