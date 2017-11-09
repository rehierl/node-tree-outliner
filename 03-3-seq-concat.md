
# Concatenation

* `x` represents the concatenation operator
* synonymous - concatenate, add, append

clarification

* operators that are missing need to be
  thought of as being defined in a similar fashion

clarification

* a set of values `V` contains basic values only
* `(is-set v)` is false for any `v in V`
* `(is-sequence v)` is false for any `v in V`

clarification

* a set of sequences `S` contains sequences only
* `(is-sequence s)` is true for any `s in S`
* any sequence `s in S` may have any length - i.e. `#s in [0,*]`
* `(#si != #sj)` may be true for any two sequences `(si !== sj)`

clarification

* `s = (e1, ..., eN) := e1 x ... x eN`
* a sequence `s` is the concatenation of its elements/values `ei`

<!-- ======================================================================= -->
## Cartesian product

* `A X B = { (a,b) | a in A, b in B }`
* `(#(A X B) == #A * #B)`

clarification

* `A` and `B` are sets of sequences
* any `s in (A X B)` is a sequence of sequences
* `(#s == 2)` for any `s in (A X B)`

<!-- ======================================================================= -->
## (v x w)

`(v x w), (v concat w) := (v,w)`

* for two values `v` and `w`
* signature - (value, value) -> sequence

`v x W := { (v,w) | w in W }`

* for value `v` and set-of-values `W`
* signature - (value, set-of-values) -> set-of-sequences
* `(#s == 2)` for any `s in (v x W)`
* `#(v x W) == #W`

`V x W := { (v,w) | v in V, w in W }`

* for set-of-values `V` and set-of-values `W`
* signature - (set-of-values, set-of-values) -> set-of-sequences
* `(#s == 2)` for any `s in (V x W)`
* `#(V x W) == (#V * #W)`

<!-- ======================================================================= -->
## (s x v)

`s x v := (s1,...,si,v)`

* for sequence `s`, `(#s = i)` and value `v`
* signature - (sequence, value) -> sequence

`v x s := (v,s1,...,si)`

* for sequence `s`, `(#s = i)` and value `v`
* signature - (value, sequence) -> sequence

`s x V := { s x v | v in V }`

* for sequence `s` and set-of-values `V`
* signature - (sequence, set-of-values) -> set-of-sequences
* `(#t == (#s+1))` for any `t in (s x V)`
* `#(s x V) == #V`

`S x v := { s x v | s in S }`

* for set-of-sequences `S` and value `v`
* signature - (set-of-sequences, value) -> set-of-sequences
* in general, sequence `t in (S x v)` may have any length
* `#(S x v) == #S`

`S x V := { s x v | s in S, v in V }`

* for set-of-sequences `S` and set-of-values `V`
* signature - (set-of-sequences, set-of-values) -> set-of-sequences
* in general, sequence `t in (S x V)` may have any length
* `#(S x V) == (#S * #V)`

<!-- ======================================================================= -->
## (s x t), (t x s)

`s x t := (s1,...,si,t1,...,tj)`

* for sequences `s` and `t`, `(#s = i)`, `(#t = j)` and `i,j in [0,*]`
* signature - (sequence, sequence) -> sequence

`t x s := (t1,...,tj,s1,...,si)`

* for sequences `s` and `t`, `(#s = i)`, `(#t = j)` and `i,j in [0,*]`
* signature - (sequence, sequence) -> sequence

`s x T := { s x t | t in T }`

* for sequence `s` and set-of-sequences `T`
* signature - (sequence, set-of-sequences) -> set-of-sequences
* in general, sequence `u in (s x T)` may have any length
* `#(s x T) == #T`

`S x T := { s x t | s in S, t in T }`

* for set-of-sequences `S` and set-of-sequences `T`
* signature - (set-of-sequences, set-of-sequences) -> set-of-sequences
* in general, sequence `u in (S x T)` may have any length
* `#(S x T) == (#S * #T)`

<!-- ======================================================================= -->
## multi-concatenation

for sequences `a,b,c` and sets-of-sequences `A,B,C`

* `axbxC = (axb)xC = ax(bxC)`
* `axBxC = (axB)xC = ax(BxC)`
* `AxbxC = (Axb)xC = Ax(bxC)`
* `AxBxC = (AxB)xC = Ax(BxC)`

clarification

* even here, the result is a sequence, or a set of sequences

<!-- ======================================================================= -->
## infix, subsequence

* `t infix-of s`, if sequences `a` and `b` exist such that `axtxb = s`.
* `(t == s)`, if and only if `axtxb = s` for `a,b = []`

clarification

* `t infix-of S` does not make much sense
* `(offset(t) in s1)` is not necessarily equal to `(offset(t) in s2)`

<!-- ======================================================================= -->
## prefix

* `t prefix-of s`, if sequence `u` exists such that `txu = s`

t prefix-of S

* `t prefix-of S`, if `t prefix-of s` for any `s in S`
* all sequences `s in S` have sequence `t` as prefix
* `t` is a common prefix of all sequences `s in S`

<!-- ======================================================================= -->
## suffix

* `t suffix-of s`, if sequence `u` exists such that `uxt = s`

t suffix-of S

* `t suffix-of S`, if `t suffix-of s` for any `s in S`
* all sequences `s in S` have sequence `t` as suffix
* `t` is a common suffix of all sequences `s in S`
