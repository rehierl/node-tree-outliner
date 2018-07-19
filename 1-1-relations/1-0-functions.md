
<!-- ======================================================================= -->
# A functional perspective

A functional perspective of relations:

* some relations can be understood to define functions
* e.g. `G(R) = (A X B)` => `f : A -> B`
* e.g. `G(R) = XT^n` => (e.g.) `f: XT^(n-1) -> Tn`
* functions `f` are special kinds of relations

<!-- ======================================================================= -->
## characteristics

* function - right-unique and left-total
* injective - unique and left-total
* surjective - right-unique and total
* bijection - unique and total

partial, total

* partial function - undefined for some (a in A)
* total function - defined for any (a in A)
* if partial, then total with regards to some strict-subset-of A
* surjective -> (image == codomain)

<!-- ======================================================================= -->
## wikipedia, monotonic functions

* aka. monotone function
* an order-preserving or order-reversing function between two ordered sets
* increasing, monotonically increasing, non-decreasing - order-preserving
* if `(x <= y)`, then `f(x) <= f(y)`
* monotonically decreasing, decreasing, non-increasing - order-reversing
* if `(x <= y)`, then `f(x) >= f(y)` - decreasing
* strictly increasing if (<) instead of (<=)
* strictly decreasing if (>) instead of (<= and >=)
* if strictly increasing/decreasing, then one-to-one

in order theory

* isotone - i.e. order-preserving
* antitone, anti-monotone - i.e. order-reversing
* the composite of two monotone mappings is monotone
* a constant function is both monotone and antitone
* e.g. order-embeddings, order-isomorphisms (surjective order-embeddings)

<!-- ======================================================================= -->
## particular elements

* a magma `(M,*)` is a set `M` equipped with a binary operation `*`

### idempotent element

* element `x` is idempotent, if `(x * x = x)`
* `*` is idempotent, if `(a * a = a)` for any `(a in M)`
* an idempotent operation can be applied multiple times
* it won't change the result beyond the initial application

### identity/neutral element

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

### absorbing/annihilating/zero element

* `e` is a left zero element, if `(e * a = e)` for any `(a in M)`
* `e` is a right zero element, if `(a * e = e)` for any `(a in M)`
* `e` is a zero element, if left- and right zero element

clarification

* `e1 = e1 * e2 = e2`
* if `M` has a left- (e1) and a right zero element (e2), then (e1 = e2)
