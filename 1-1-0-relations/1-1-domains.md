
<!-- ======================================================================= -->
# Sets related to functions

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
* image < range < codomain
* `f : dom(f) -> rng(f)`

inverse image

* `img(Y,f) = { a : (f(a) == b), (a in A), (b in Y), (Y subset-of B) }`
* i.e. all elements in `A` that are mapped into `Y`
* synonymous - inverse image, pre-image
