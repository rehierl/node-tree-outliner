
<!-- ======================================================================= -->
# Inner/outer subset of a set

```
       |-oss(s)=s--------------|
       | |-css(s)-| |-iss(s)-| |
A(s) <---| { .. } | | { .. } |---> D(s)
       | |--------| |--------| |
       |-----------------------|
```

Any set in a strict hierarchy `H := (V,P)` is the union of disjoint sets:

* for any (s in P), the following subsets can be defined:
* `oss(s) := s` - the set's **outer subset**
* `iss(s) := E(D(s))` - the set's **inner subset**
* `css(s) := (s - iss(s))` - the set's **characteristic subset**

Note that any set is the union of its css(s) with its iss(s). Both subsets
are obviously disjoint by definition. Furthermore, css(s) binds (s) to its
ancestors in A(s) and iss(s) binds (s) to its descendants in D(s).

* `(iss(s) != {})` if `(s in LS)`
* `(css(s) in P)` iff `(s in LS)`
* `(iss(s) == {})` if `(s in LS)`

In contrary to CSS(h), ISS(h) is a union of related sets. However, ISS(h) is
not a hierarchy of sets because iss(l) is empty for any leaf set (l in LS).
Even though ISS(h) is itself not a hierarchy of sets, the (disjoint ex-or
strictly related) rule still applies. If it would not, then that rule could
also not apply to hierarchy (h).

* `OSS(h) := P = { oss(s) | (s in h) }`
* `CSS(h) := { css(s) | (s in h) }`
* `ISS(h) := { iss(s) | (s in h) }`
