
<!-- ======================================================================= -->
# Concatenation

* `x` represents the concatenation operator
* synonymous - concatenate, add, append
* note the lower-case letter `x`

Note that any sequence is in principle the concatenation of its elements.

* `s = [e1, ..., eN] := e1 x ... x eN`

Note that the result of the concatenation operation is in general a set of
sequences. Depending on the input parameters, all sequences within the result
of the concatenation operation is in principle **a set of flat sequences** (i.e.
no added nesting). That is in contrast to the base definition of the Cartesian
product.

Note that, in general, there is no statement possible about the lengths of the
sequences in the resulting set-of-sequences. Likewise, the number of sequences
in the resulting set can not be determined in general. However, such statements
still can be made under special circumstances: If no input set is a set of
sequences, then the length of each sequence within the resulting set is
identical to the number of sets involved. In contrary to that, the sequences
in the result set of the Cartesian product always have the exact same length.

Note that, because the result of the concatenation is in general a set of
sequences, the concatenation operation can be used to specify types/domains.

<!-- ======================================================================= -->
## (v x w)

* combining values with values

`(v x w), (v concat w) := (v,w)`

* for two values `v` and `w`
* signature - (value, value) -> sequence

`v x W := { (v,w) | (w in W) }`

* for value `v` and set-of-values `W`
* signature - (value, set-of-values) -> set-of-sequences
* note that - `(#s == 2)` for any `s in (v x W)`
* note that - `#(v x W) == #W`

`V x W := { (v,w) | (v in V) and (w in W) }`

* for set-of-values `V` and set-of-values `W`
* signature - (set-of-values, set-of-values) -> set-of-sequences
* note that - `(#s == 2)` for any `s in (V x W)`
* note that - `#(V x W) == (#V * #W)`

similar definitions for

* `V x w := { (v,w) | (v in V) }`

<!-- ======================================================================= -->
## (s x v)

* combining sequences with values

`s x v := [s1,...,si,v]`

* for sequence `s`, `(#s = i)` and value `v`
* signature - (sequence, value) -> sequence
* note that - value `v` is added to the end of sequence `s`
* note that - `#(s x v) = (#s + 1)`

`v x s := [v,s1,...,si]`

* for sequence `s`, `(#s = i)` and value `v`
* signature - (value, sequence) -> sequence
* note that - value `v` is added to the beginning of sequence `s`
* note that - `#(v x s) = (1 + #s)`

`s x V := { s x v | (v in V) }`

* for sequence `s` and set-of-values `V`
* signature - (sequence, set-of-values) -> set-of-sequences
* note that - `(#t == (#s+1))` for any `t in (s x V)`
* note that - `#(s x V) == #V`

`S x v := { s x v | (s in S) }`

* for set-of-sequences `S` and value `v`
* signature - (set-of-sequences, value) -> set-of-sequences
* note that - sequence `t in (S x v)` may have any length
* note that - `#(S x v) == #S`

`S x V := { s x v | (s in S) and (v in V) }`

* for set-of-sequences `S` and set-of-values `V`
* signature - (set-of-sequences, set-of-values) -> set-of-sequences
* note that - sequence `t in (S x V)` may have any length
* note that - `#(S x V) == (#S * #V)`

similar definitions for

* `V x s := { v x s | (v in V) }`
* `v x S := { v x s | (s in S) }`

<!-- ======================================================================= -->
## (s x t)

* combining sequences with sequences

`s x t := [s1,...,si,t1,...,tj]`

* for sequences `s` and `t`, `(#s = i)`, `(#t = j)` and `i,j in [0,*]`
* signature - (sequence, sequence) -> sequence
* note that - `#(s x t) = (#s + #t)`

`s x T := { s x t | (t in T) }`

* for sequence `s` and set-of-sequences `T`
* signature - (sequence, set-of-sequences) -> set-of-sequences
* note that - sequence `u in (S x T)` may have any length
* note that - `#(s x T) == #T`

`S x T := { s x t | (s in S) and (t in T) }`

* for set-of-sequences `S` and set-of-sequences `T`
* signature - (set-of-sequences, set-of-sequences) -> set-of-sequences
* note that - sequence `u in (S x T)` may have any length
* note that - `#(S x T) <= (#S * #T)`

clarification

* `(s1 x t1) == (s2 x t2)` is possible
* if `s1 prefix-of s2` and `t2 suffix-of t1`
* e.g. `([1]x[2,3]) == ([1,2]x[3]) == [1,2,3]`
* i.e. `f(x1,y1) == f(x2,y2)`

<!-- ======================================================================= -->
## summary

* `axbxc = (axb)xc = ax(bxc)` - one sequence
* `axbxC = (axb)xC = ax(bxC)` - set of sequences
* `axBxC = (axB)xC = ax(BxC)` - set of sequences
* `AxbxC = (Axb)xC = Ax(bxC)` - set of sequences
* `AxBxC = (AxB)xC = Ax(BxC)` - set of sequences

Note that, for sequences `a,b,c` and sets-of-sequences `A,B,C`,
the result is in general a set of non-nested sequences.

<!-- ======================================================================= -->
## multi-concatenation

n-ary concatenation product (xAi)

* `xA1 := A1` and `xAN := xA(N-1) x AN`
* `xAi <=> (A1 x A2 x ...)`

n-ary concatenation power (xA^N)

* `xA^1 := A` and `xA^N := xA^(N-1) x A`
* `xA^N := xAi` for `(Ai == A)` and `i in [1,N]`
* `xA^N <=> (A x A x ...)`

variable concatenation power (xA{a,b})

* see - regular expression like patterns
* (+) is the union operator for sets
* `xA{a,b}, xA^{a,b} := +(xA^i)` for `i in [a,b] in [1,*]`
* `xA{a,b} = (xA^a + xA^(a+1) + ... + xA^b)`
* `xA{1,4} = (xA^1 + xA^2 + xA^3 + xA^4)`
* `xA{a} = xA^{a,a} = xA^a`
* `xA{+} = (xA^1 + xA^2 + ...)`

<!-- ======================================================================= -->
## infix

* `t infix-of s`, if sequences `a` and `b` exist such that `axtxb = s`.
* `(t == s)`, if and only if `axtxb = s` for `a,b = []`

clarification

* `t infix-of S` does not make sense, because ...
* `(offset(t) in s1)` is not necessarily equal to `(offset(t) in s2)`
* ... could be generalized to allow any offset.

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
