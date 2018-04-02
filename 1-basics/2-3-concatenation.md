
<!-- ======================================================================= -->
# Concatenation

* `x` represents the concatenation operator
* note: the lower-case letter 'x'
* synonymous - concatenate, add, append

clarification

* cartesian product <!> concatenation
* main difference: concatenation is associative, the cartesian product is not

clarification

* some `x` operator definitions that are missing
* think of those as being defined in a similar fashion

clarification

* `XVi <=> xVi` if `Vi` are all sets of values
* `XV^N <=> xV^N` if `V` is a set of values
* `XV^{a,b} <=> xV{a,b}` if `V` is a set of values

clarification

* `s = (e1, ..., eN) := e1 x ... x eN`
* a sequence `s` is the concatenation of its elements/values `ei`

<!-- ======================================================================= -->
## (v x w)

`(v x w), (v concat w) := (v,w)`

* for two values `v` and `w`
* signature - (value, value) -> sequence

`v x W := { (v,w) : (w in W) }`

* for value `v` and set-of-values `W`
* signature - (value, set-of-values) -> set-of-sequences
* `(#s == 2)` for any `s in (v x W)`
* `#(v x W) == #W`

`V x W := { (v,w) : (v in V) and (w in W) }`

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

`s x V := { s x v : (v in V) }`

* for sequence `s` and set-of-values `V`
* signature - (sequence, set-of-values) -> set-of-sequences
* `(#t == (#s+1))` for any `t in (s x V)`
* `#(s x V) == #V`

`S x v := { s x v : (s in S) }`

* for set-of-sequences `S` and value `v`
* signature - (set-of-sequences, value) -> set-of-sequences
* in general, sequence `t in (S x v)` may have any length
* `#(S x v) == #S`

`S x V := { s x v : (s in S) and (v in V) }`

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

`s x T := { s x t : (t in T) }`

* for sequence `s` and set-of-sequences `T`
* signature - (sequence, set-of-sequences) -> set-of-sequences
* in general, sequence `u in (S x T)` may have any length - i.e. `#u in [0,*]`
* also, `u1,u2 in (S x T) !> (#u1 == #u2)`
* `#(s x T) == #T`

`S x T := { s x t : (s in S) and (t in T) }`

* for set-of-sequences `S` and set-of-sequences `T`
* signature - (set-of-sequences, set-of-sequences) -> set-of-sequences
* in general, sequence `u in (S x T)` may have any length - i.e. `#u in [0,*]`
* also, `u1,u2 in (S x T) !> (#u1 == #u2)`
* `#(S x T) <= (#S * #T)`

clarification

* `(s1 x t1) == (s2 x t2)` is possible
* e.g. `([1]x[2,3]) == ([1,2]x[3]) == [1,2,3]`
* `s1 prefix-of s2` and `t2 suffix-of t1`
* i.e. `f(x1,y1) == f(x2,y2) == z` for `f(a,b) := (a x b)`

<!-- ======================================================================= -->
## clarifications

clarification

* `v x ()` or `() x v` => `(v)`
* `v x {}` or `{} x v` => `{}`
* `s x ()` or `() x s` => `s`
* `s x {}` or `{} x s` => `{}`
* `() x ()` => `()`
* `{} x {}` => `{}`

clarification

* `axbxc = (axb)xc = ax(bxc)`
* `axbxC = (axb)xC = ax(bxC)`
* `axBxC = (axB)xC = ax(BxC)`
* `AxbxC = (Axb)xC = Ax(bxC)`
* `AxBxC = (AxB)xC = Ax(BxC)`

* for sequences `a,b,c` and sets-of-sequences `A,B,C`
* the result always is a sequence or a set of sequences

<!-- ======================================================================= -->
## multi-concatenation

n-ary concatenation product (xAi)

* `xA1 := A1` and `xAi := xA(i-1) x Ai`
* for `s in xAi`, `#s` is not necessarily equal to `N`

n-ary concatenation power (xA^N)

* `xA^1 := A` and `xA^N := xA^(N-1) x A`
* `xA^N := xAi` for `(Ai == A)` and `i in [1,N]`

clarification

* `xAi <=> (A1 x A2 x ...)`
* `xA^N <=> (A x A x ...)`

variable concatenation power (xA{a,b})

* see - regular expression like patterns
* `xA{a,b}, xA^{a,b} := +(xA^i)` for `i in [a,b] in [1,*]`
* `xA{a,b} = (xA^a + xA^(a+1) + ... + xA^b)`
* (+) is the union operator for sets
* `xA{1,4} = (xA^1 + xA^2 + xA^3 + xA^4)`
* `xA{a} = xA^{a,a} = xA^a`
* `xA{+} = (xA^1 + xA^2 + ...)`

<!-- ======================================================================= -->
## infix, subsequence

* `t infix-of s`, if sequences `a` and `b` exist such that `axtxb = s`.
* `(t == s)`, if and only if `axtxb = s` for `a,b = []`

clarification

* `t infix-of S` does not make sense, because ...
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