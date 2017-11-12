
# Cartesian product

* `X` represents the Cartesian product operator

<!-- ======================================================================= -->
## binary product

* `A X B = { (a,b) : a in A, b in B }`
* `(#(A X B) == #A * #B)`

clarification

* `A` and `B` are sets of sequences
* any `s in (A X B)` is a sequence of sequences
* `(#s == 2)` for any `s in (A X B)`

<!-- ======================================================================= -->
## associative

* `A X (A X A) = {(1,(1,1))} != {((1,1),1)} = (A X A) X A` for `A := {1}`
* `A X (B X C) <!> (A X B) X C`

clarification

* `A X B X C X ...` is essentially undefined

<!-- ======================================================================= -->
## multi cartesian product

n-ary cartesian product (XAi)

* `XAi := A1 X ... X AN = {(a1,...,aN) : (ai in Ai)}` - for any set `Ai`
* not equivalent to concatenation as defined below
* issue - one or more `Ai` is a set of tuples
* `(#s == N)` for any `s in XAi`

n-ary cartesian power (XA^N)

* `XA^N := A X ... X A = {(a1,...,aN) : (ai in A)}` - for set `A`
* `XA^N := XAi` for `(Ai == A)` and `i in [1,N]`

clarification

* `XAi <!> (A1 X A2 X ...)`
* `XA^N <!> (A X A X ...)`
* even if parenthesis were used in some specific order

variable cartesian power (XA{a,b})

* see - regular expression like patterns
* `XA{a,b}, XA^{a,b} := +(XA^i)` for `i in [a,b] in [1,*]`
* `XA{a,b} := (XA^a + XA^(a+1) + ... + XA^b)`
* (+) is the union operator for sets
* `XA{1,4} = (XA^1 + XA^2 + XA^3 + XA^4)`
* `XA{a} = XA^{a,a} = XA^a`
* `XA{+} = (XA^1 + XA^2 + ...)`
