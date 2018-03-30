
<!-- ======================================================================= -->
# Binary Relations

* binary relation := `R = (A, B, G)`
* `G subset-of (A X B)`
* `(#r == 2)` for any `r in R`, i.e. `(n == 2)`
* `dom(R) := G`, `type(R) := (A X B)`
* "homogenous" if `(A == B)`, otherwise "heterogenous"

clarification

* a binary relation always has two sets of values
* note that both sets may be identical, i.e. `(A == B)`

<!-- ======================================================================= -->
## related-to

* `a related-to b`, if `aRb` or `bRa`
* `a` is related to `b`, and `b` is related to `a`
* synonymous - strictly, directly

clarification

* `a` and `b` are strictly related to each other, if `(a,b) in (R or inv(R))`
* both are related, even if the relation has no specific semantics

<!-- ======================================================================= -->
## semantics

antonymous semantics

* `parent-of` <-> `child-of`
* `contains` <-> `element-of`
* `superset-of` <-> `subset-of`
