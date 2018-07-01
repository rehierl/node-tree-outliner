
<!-- ======================================================================= -->
# Types/Domains

a type/domain-based view on "x in X"

* `x in X` means that value/element `x` may represent any element in `X`
* `X` however might contain element `y` for which `x` is not defined,
  or which will trigger an error if `x` evaluates to `y`

domain-based view

* `domainOf(x)` := a set of values for which `x` is defined
* `D(x), dom(x), (domain-of x) := domainOf(x)`
* a domain is a strict definition of the values x may have
* it is however not always possible to exactly specify all valid values

type-based view

* `typeOf(x)` := a set of values for which `x` is (usually) defined
* `T(x), type(x), (type-of x) := typeOf(x)`
* `type(x)` may contain values for which `x` is undefined
* a type may be seen as the upper boundary (best effort) of a domain
* a type is used as a less strict definition of the values x may have
* `(dom(x) subset-of type(x))` is true by definition

general syntax, universe type

* `A : B` => `(type(A) == B)` => a typing judgment
* a typing judgment is used to express that `A` has type/domain `B`
* the universal type (`U`) contains all types, but not itself
* `(A : B)` => `(A in B) and (B in U)`

<!-- ======================================================================= -->
## variables, elements

type-of e

* `e.type := V`, if `V == type(e)`
* the value `v` an element `e` may represent is limited to a set of values `V`

clarification

* `dom(v) := { v }`
* a value can not represent any other value
* the smallest type/domain of a value is essentially the value itself

V type-of e

* `(V type-of e) := (e.type == V)`
* `V` is said to be the type of element `e`
* however, `(Real type-of e) => (Integer type-of e)`

clarification

* the "smallest" set (i.e. Integer, not Real) that contains
  all valid values of `x` needs to be used as the type of `x`

<!-- ======================================================================= -->
## set of values

* in general, any set represents a type/domain
* the type of a set is however a set of sets
* hint: `subset-of <=!=> element-of`

<!-- ======================================================================= -->
## sequences

* `t = (x1:T1,...,xn:Tn)` where `(Ti == type(xi))`
* `t = (x1,...,xn) : T1 x ... x Tn` (in type theory)
* `t = (x1,...,xn) : xTi`
* `t = (x1,...,xn) : xT^n` if `(Ti == T)` for any `i in [1,n]`
* `type(t)` := `xTi` or `xT^n`

<!-- ======================================================================= -->
## set of sequences

* given a set of sequences `S`
* if `t` is intended to represent any `s in S`, then `(dom(t) == S)`
* `type(t)` is then a `xTi` description such that `S subset-of xTi`
* this then allows to state `t in xTi`

clarification (???)

* sequences in `S` all have the same length?
* in mathematics in general true
* but, that is not what we need
* e.g. a set of node sequences of any length

<!-- ======================================================================= -->
## n-ary types/domains

* `T1 x ... x Tn` represents some type `xTi`
* `xTi` represents an unary type, if `(n == 1)`
* binary type, if `(n == 2)`
* ternary type, if `(n == 3)`
* `xTi` represents in general an n-ary type
