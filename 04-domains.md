
# Domains
<!-- ======================================================================= -->

* `s = [e1,...,eN]` for `N in [0,+Inf)`
* Each element `e(i)` is an element of some set `E(i)` (i.e. `e(i) in E(i)`).

Set `E` is the **domain** of element `e`

* `E domain-of e` is true, if `e in E`
* synonymous - domain-of, type-of
* `e element-of E` is true, if `e in E`
* synonymous - element-of, belongs-to
* `domainOf(e) = E`

In general, the different elements of a sequence may belong to any domain
(i.e. `(Ei = Ej)` may be false for any `(i != j)`). It is a only special case,
if `(Ei = Ej)` is true for some or any `i and j in [1,N]` (i.e. `E1 = ... = EN`).

An element by itself does not allow to uniquely identify its domain (e.g. the
result of `typeOf(+1)` could be the set of: natural numbers `[1,+Inf)` -
integral numbers `(-Inf,+Inf)` - etc.

* For clarification purposes, a sequence may be written as:
  `s = [s(i):E(i)] = [e1:E1,...,eN:EN]`
* If `E1 = ... = EN`, a sequence may be written as:
  `s = [s(i):E] = [e1:E,...,eN:E]`
