
<!-- ======================================================================= -->
# Inner/outer subset of a set

```
       |-oss(s)=s--------------|
       | |-css(s)-| |-iss(s)-| |
A(s) <---| { .. } | | { .. } |---> D(s)
       | |--------| |--------| |
       |-----------------------|
```

Any set in a hierarchy `H := (V,P)` is the union of two disjoint subsets:

* for any set `(s in P)`, the following subsets can be defined:
* the set's **outer subset**: `oss(s) := s`
* the set's **inner subset**: `iss(s) := E(D(s))`
* the set's **characteristic subset**: `css(s) := (s \ iss(s))`

Note that any set is the union of its characteristic subset with its inner
subset. Also, both subsets are by definition disjoint. Furthermore, css(s)
binds (s) to its ancestors in A(s) and iss(s) binds (s) to its descendant
sets in D(s).

* `(css(l) in P)` iff `(l in LS)`
* `(css(l) != {})` if `(l in LS)`
* `(iss(l) == {})` iff `(l in LS)`

Note that css(s) and iss(s) may both be empty.
However, both subsets can not be empty at the same time.

* `(css(s) != {}) or (iss(s) != {})` for any `(s in P)`

In contrary to CSS(h), ISS(h) is a union of related sets. However, ISS(h) is
not a hierarchy of sets since iss(l) is empty for any leaf set (l in LS).
Put differently, iss(s) may have more no or more than one root set. However,
the "disjoint ex-or strictly related" rule also applies ot ISS(h).

* `OSS(h) := P = { oss(s) | (s in h) }`
* `CSS(h) := { css(s) | (s in h) }`
* `ISS(h) := { iss(s) | (s in h) }`
