
<!-- ======================================================================= -->
# A functional perspective

A functional perspective of relations:

* some relations can be understood to define functions
* e.g. `G(R) = (A X B)` => `f : A -> B`
* e.g. `G(R) = XT^n` => (e.g.) `f: XT^(n-1) -> Tn`
* functions `f` are special kinds of relations

<!-- ======================================================================= -->
## sets related to functions

* `f : A -> B`
* `A` is said to be the function's domain
* `B` is said to be the function's codomain, aka. target set
* `f(a) = b`, `(a in A) and (b in B)`, `f(a)` evaluates to `b`
* `a` represents the function's argument
* `f(a)` the function's value for argument `a`

domain

* the domain of a function `dom(f)` is ...
* the set of input/argument values for which the function is defined
* for each `a in dom(f)`, `f(a)` evaluates to some `b in B`
* `a` is mapped onto `b` under `f`
* `b` is `a`'s image under `f`
* however, `dom(f)` is not necessarily the same as `A` -
  i.e. `dom(f)` can be a strict subset of `A`
* there does not seem to be a dedicated name for `A`

codomain

* `B` is said to be the function's codomain
* an image is a subset of a function's codomain - i.e. `img(f) subset-of B`
* `f` is surjective - `a in A` exists for any `b in B` such that `f(a)=b`
* surjective => `(img(f) == B)`

image

* `img(X,f) = { f(a) | (a in X), (X subset-of A) }` -
  i.e. the set of values that contains all possible output/result values
* subset `X` of `A` => image of `X` under `f`
* `img(f) := img(dom(f),f)` is referred to as the function's image

range

* refers to either the codomain or the image of `f`
* the latter is the more strict use of the word "range"
* codomain > range > image
* `f : dom(f) -> rng(f)`

inverse image

* `img(Y,f) = { a : (f(a) == b), (a in A), (b in Y), (Y subset-of B) }`
* i.e. all elements in `A` that are mapped into `Y`
* synonymous - inverse image, pre-image

<!-- ======================================================================= -->
## characteristics

* function - right-unique and left-total
* injective - unique and left-total
* surjective - right-unique and total
* bijection - unique and total

partial, total

* partial function - `f` is undefined for some `a in A`
* total function - `f` is defined for any `a in A`
* if partial, then total with regards to some strict-subset-of `A`
* surjective -> (image == codomain)

monotonic function

* a function between ordered sets ...
* such that it preserves or reverses the given order
* if `(x <= y)`, then `f(x) <= f(y)` - increasing
* if `(x <= y)`, then `f(x) >= f(y)` - decreasing
* monotonically increasing/decreasing

<!-- ======================================================================= -->
## particular elements

* a magma `(M,*)` is a set `M` equipped with a binary operation `*`

## idempotent element

* element `x` is idempotent, if `(x * x = x)`
* `*` is idempotent, if `(a * a = a)` for any `(a in M)`
* an idempotent operation can be applied multiple times
* it won't change the result beyond the initial application

## identity/neutral element

* `e` is a left identity, if `(e * a = a)` for any `(a in M)`
* `e` is a right identity, if `(a * e = a)` for any `(a in M)`
* `e` is a (two-sided) identity, if left- and right-identity

clarification

* there can be several left/right identities
* but only if there is no two-sided identity
* two-sided identity => one left (a) and one right (b) identity, and (a = b)

examples

* `a + 0 = a` - additive identity
* `a * 1 = a` - multiplicative identity

## absorbing/annihilating/zero element

* `e` is a left zero element, if `(e * a = e)` for any `(a in M)`
* `e` is a right zero element, if `(a * e = e)` for any `(a in M)`
* `e` is a zero element, if left- and right zero element

clarification

* `e1 = e1 * e2 = e2`
* if `M` has a left- (e1) and a right zero element (e2), then (e1 = e2)
