
# Cartesian product

* `X` represents the Cartesian product operator

<!-- ======================================================================= -->
## binary product

* `A X B = { (a,b) | a in A, b in B }`
* `(#(A X B) == #A * #B)`

clarification

* `A` and `B` are sets of sequences
* any `s in (A X B)` is a sequence of sequences
* `(#s == 2)` for any `s in (A X B)`

<!-- ======================================================================= -->
## associative

* `A X (B X C) <!> (A X B) X C`
* `A X (A X A) = {(1,(1,1))} != {((1,1),1)} = (A X A) X A` for `A := {1}`
* `A X B X C X ...` is essentially undefined

<!-- ======================================================================= -->
## n-ary, variable product

n-ary cartesian product (XAi)

* `XAi := A1 X ... X AN = {(a1,...,aN), ai in Ai}` - for any set `Ai`
* not equivalent to concatenation as defined below
* issue - one or more `Ai` is a set of tuples
* `(#s == N)` for any `s in XAi`
* `(A X B X ...) <!> XAi`

n-ary cartesian power (XA^N)

* `XA^N := A X ... X A = {(a1,...,aN), ai in A}` - for set `A`
* `XA^N := XAi` for `(Ai == A)` and `i in [1,N]`
