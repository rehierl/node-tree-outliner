
<!-- ======================================================================= -->
# A functional perspective

* functions looked at as being "ordered pairs with unique first components"

function-based view

* function - right-unique and left-total
* injective function - unique and left-total
* surjective function - right-unique and total
* bijection - unique and total

clarification

* partial function - `f` is undefined for some `a in A`
* total function - `f` is defined for any `a in A`
* if partial, then total with regards to some strict-subset-of `A`
* not surjective -> `img(f) strict-subset-of B`, i.e. (image != codomain)

<!-- ======================================================================= -->

* some relation `R` can be seen to define a function
* e.g. `G(R) = (A X B)` => `f : A -> B`
* e.g. `G(R) = xT^n` => `f: xT^(n-1) -> Tn`
* a function `f` is a special kind of relation
* however, this perspective is of no interest here
* of interest is, that `R` represents a set of tuples/sequences

standard perspective

* `f : A -> B`
* `A` is said to be the function's domain
* `B` is said to be the function's codomain, aka. target set
* `f(a) = b`, `(a in A) and (b in B)`, `f(a)` evaluates to `b`
* here, `a` represents the function's argument and
  `f(a)` the function's value for argument `a`

domain

* the domain of a function `dom(f)` is
  the set of input/argument values for which the function is defined
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

* `img(X,f) = { f(a) : (a in X), (X subset-of A) }` -
  i.e. the set of values that contains all possible output/result values
* subset `X` of `A` => image of `X` under `f`
* `img(f) := img(dom(f),f)` is referred to as the function's image

inverse image

* `img(Y,f) = { a : (f(a) == b), (a in A), (b in Y), (Y subset-of B) }` -
  i.e. all elements in `A` that are mapped into `Y`
* synonymous - inverse image, pre-image

range

* refers to either the codomain or the image of `f`
* the latter is the more strict use of the word "range"
* codomain > range > image
* `f : dom(f) -> rng(f)`
