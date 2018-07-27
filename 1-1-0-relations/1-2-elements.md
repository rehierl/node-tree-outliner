
<!-- ======================================================================= -->
# Function - elements

<!-- ======================================================================= -->
## wikipedia, magma

* a magma `(M,*)` is a set `M` equipped with a binary operation `*`

<!-- ======================================================================= -->
## wikipedia, idempotence

* element `x` is idempotent, if `(x * x = x)`
* `*` is idempotent, if `(a * a = a)` for any `(a in M)`
* an idempotent operation can be applied multiple times
* it won't change the result beyond the initial application

<!-- ======================================================================= -->
## wikipedia, identity element

* aka. neutral element
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

<!-- ======================================================================= -->
## wikipedia, absorbing element

* aka. annihilating/zero element
* `e` is a left zero element, if `(e * a = e)` for any `(a in M)`
* `e` is a right zero element, if `(a * e = e)` for any `(a in M)`
* `e` is a zero element, if left- and right zero element

clarification

* `e1 = e1 * e2 = e2`
* if `M` has a left- (e1) and a right zero element (e2), then (e1 = e2)
