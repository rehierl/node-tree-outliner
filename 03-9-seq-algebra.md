
# Sequence Algebra

<!-- ======================================================================= -->
## operators

* The letter `x` represents the concatenation operator.
* synonymous - concatenate, add, append

### (v x w)

`vxw = (v,w)`

* for two elements `v` and `w`
* signature - `value x value -> sequence`
* `vxw != wxv`

### axe, exa

`axe = (a1,...,ai,e)`

* for sequence `a`, `(#a = i)` and some element `e`
* signature - `sequence, value -> sequence`

`exa = (e,a1,...,ai)`

* for sequence `a`, `(#a = i)` and some element `e`
* signature - `value x sequence -> sequence`

### axb, bxa

`axb = (a1,...,ai,b1,...,bj)`,

* for sequences `a` and `b`, `(#a = i)`, `(#b = j)` and `i,j in [0,+Inf)`
* signature - `sequence x sequence -> sequence`
* `axb != bxa`

### axB, Axb

`axB = { axb | b in B }`

* for sequence `a` and a set of sequences `B`
* Any sequence in `B` is prefixed with sequence `a`.
* signature - `sequence x set -> set`

`Axb = { axb | a in A }`

* for sequence `b` and a set of sequences `A`
* Any sequence in `A` is suffixed with sequence `b`.
* signature - `set x sequence -> set`

### AxB, BxA

`AxB = { axb | a in A, b in B }`

* for sets of sequences `A` and `B`
* signature - `set x set -> set`
* `AxB != BxA`

This is unlike the Cartesian product:

* `A X B = { (a,b) | a in A, b in B }`
* `A X B` is a sequence of two sequences
* `axb` is a flattened sequence of elements

### (A = B), (A != B)

`(A = B) = (b in A, for any b from B) and (a in B, for any a from A)`

* for two sets of elements `A` and `B`
* signature - `set x set -> bool`

`(A != B) = not (A = B)`

* for two sets of elements `A` and `B`
* signature - `set x set -> bool`

### summary

* `axbxC = (axb)xC = ax(bxC)`
* `axBxC = (axB)xC = ax(BxC)`
* `AxbxC = (Axb)xC = Ax(bxC)`
* `AxBxC = (AxB)xC = Ax(BxC)`

Any sequence `s` is the product of its elements `e1,...,eN`

* `s = (e1,...,eN) = e1 x e2 x ... x eN`

<!-- ======================================================================= -->
## infix, subsequence

* `t subsequence-of s`, if sequences `a` and `b` exist such that `axtxb = s`.
* `(t = s)`, if and only if `axtxb = s` for `a,b = []`

<!-- ======================================================================= -->
## prefix

* `a prefix-of b`, if a sequence `c` exists such that `axc = b`
* `a prefix-of B`, if `a prefix-of b` is true for any `b in B`
* All sequences in `B` have sequence `a` as a common prefix.
* `s = axb`, then `a prefix-of s`

<!-- ======================================================================= -->
## suffix

* `a suffix-of b`, if a sequence `c` exists such that `cxa = b`
* `a suffix-of B`, if `a suffix-of b` is true for any `b in B`
* All sequences in `B` have sequence `a` as a common suffix.
* `s = axb`, then `b suffix-of s`
