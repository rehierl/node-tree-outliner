
# Domain of a sequence

* `A : B` is a typing judgment, i.e. expression `A` has type/domain `B`
* the universe type (in general `U`) contains all types, but not itself

<!-- ======================================================================= -->
## element types

* `t = (x1:T1,...,xn:Tn)` where `(Ti == dom(xi))`
* `t = (x1,...,xn) : T1 x ... x Tn` (in type theory)
* `t = (x1,...,xn) : xTi`
* `t = (x1,...,xn) : xT^n = (ti:T)` if `(Ti == T)` for any `i in [1,n]`

<!-- ======================================================================= -->
## domain of a sequence

* `dom(t) := xTi` if `(Ti == dom(xi))` for any `i in [1,n]`
* `dom(t) subset-of xTi` if `(Ti != dom(xi))` for some `i in [1,n]`

<!-- ======================================================================= -->
## domain of a set of sequences

* `S` is a set of sequences
* `s = (s1:S1,...,sn:Sn)` for any `s in S`
* i.e. `(#si == #sj)` for any `i,j in [1,#S]`
* `dom(S) := xSi`

in general

* `dom(s) := D` if `dom(s) in D` for any `s in S`

<!-- ======================================================================= -->
**TODO** - `dom(S) <!> S` ?!?

* usually, a domain is limited to valid values/sequences only!
* or - see "domain" as some sort of type description?
