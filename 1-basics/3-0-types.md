
<!-- ======================================================================= -->
# Types

* a description for `X` is needed that allows to express `x in X`
* `x in X` means that value/element `x` may represent any element in `X`
* occasionally, `X` can contain elements `y` for which `x` is not defined
* there needs to be a balance between (domain := `X` contains no `y` element)
  and (type := `X` may contain `y` elements)

domain

* `domainOf(x)` := the set of all values for which `x` is defined
* `D(x), dom(x), (domain-of x) := domainOf(x)`
* in general, `dom(x)` may be represented by `D`
* that is, `x in D` <-> `x in dom(x)`

type

* `typeOf(x)` := the set of all values for which `x` is (usually) defined
* `T(x), type(x), (type-of x) := typeOf(x)`
* `type(x)` may contain values for which `x` is undefined
* `type(x)` may be understood as a best-effort description of `dom(x)`
* a type is used as a loose/general description of its elements
* in general, `type(x)` may be represented by `T`
* that is, `x in T` <-> `x in type(x)`
* `dom(x) subset-of type(x)`

general syntax, universe type

* `A : B` is a typing judgment
* i.e. expression `A` has type/domain `B`
* i.e. `(type(A) == B)`
* the universe type (in general `U`) contains all types, but not itself
* i.e. `(A : B) <=> (A in B) and (B in U)`

<!-- ======================================================================= -->
## variables, elements

type-of e

* `e.type := V`, if `V == type(e)`
* the value `v` an element `e` may represent is limited to a set of values `V`
* signature - (variable) -> set

clarification

* `dom(v) := { v }`
* a value can not represent any other value
* the smallest type (i.e. domain) of a value is essentially the value itself

V type-of e

* `(V type-of e) := (e.type == V)`
* `V` is said to be the type of element `e`
* however, `(Real type-of e) => (Integer type-of e)`
* signature - (set,variable) -> boolean

clarification

* the smallest set that contains all values of `x` needs to be seen
  to represent the type of `x`

<!-- ======================================================================= -->
## set of values

* the type of a set of values must be a set of sets
* recall that `subset-of <!> element-of`

<!-- ======================================================================= -->
## tuples, sequences

* `t = (x1:T1,...,xn:Tn)` where `(Ti == type(xi))`
* `t = (x1,...,xn) : T1 x ... x Tn` (in type theory)
* `t = (x1,...,xn) : xTi`
* `t = (x1,...,xn) : xT^n` if `(Ti == T)` for any `i in [1,n]`

clarification

* `type(t)` is some `xTi` or `xT^n` if `t` is a tuple/sequence
* `dom(t) subset-of type(t)`

<!-- ======================================================================= -->
## set of sequences

* given a set of sequences `S`
* i.e. `is-sequence(s)` is true for any `s in S`
* if `t` is intended to represent any `s in S`, then `(dom(t) == S)`
* `type(t)` then is a `xTi` description such that `S subset-of xTi`
* this allows to state `t in xTi` or `t:xTi`

<!-- ======================================================================= -->
## n-ary types

* `T1 x ... x Tn` represents some type `xTi`
* `xTi` represents an unary type, if `(n == 1)`
* binary type, if `(n == 2)`
* ternary type, if `(n == 3)`
* `xTi` represents in general an n-ary type
