
<!-- ======================================================================= -->
# Infix, prefix, suffix

Note that ...

* The following definitions will be referred to as "concatenation-based".
* An infix/prefix/suffix `t` represents a distinct/exact pattern
  in the corresponding sequence `s`.
* An infix may also be a prefix and/or a suffix.
* The empty sequence `[]` is an infix/prefix/suffix of any sequence.
* Any sequence, including `[]`, is an infix, prefix and suffix to itself.

<!-- ======================================================================= -->
## infix/substring

(t infix-of s)

* `(t infix-of s)`, if sequences `a` and `b` exist such that `s = (a x t x b)`.
* `(t == s)`, if `s = (a x t x b)` for `a,b = []`
* note - `[]` is an infix to any sequence

(t infix-of S)

* `(t infix-of S)`, if `(t infix-of s)` for any `(s in S)`
* all sequences `(s in S)` have sequence `t` as an infix
* `t` is a common infix of all sequences `(s in S)`

(T infix-of S)

* `(T infix-of S)`, if `(t infix-of S)` for any `(t in T)`
* any `(t in T)` is a infix of any sequence `(s in S)`

<!-- ======================================================================= -->
## prefix

(t prefix-of s)

* `(t prefix-of s)`, if a sequence `u` exists such that `s = (t x u)`
* `(t == s)`, if `s = (t x u)` for `(u = [])`
* note - `[]` is a prefix to any sequence

(t prefix-of S)

* `(t prefix-of S)`, if `(t prefix-of s)` for any `(s in S)`
* all sequences `(s in S)` have sequence `t` as prefix
* `t` is a common prefix of all sequences `s in S`

(T prefix-of S)

* `(T prefix-of S)`, if `(t prefix-of S)` for any `(t in T)`
* any `(t in T)` is a prefix of any sequence `(s in S)`

<!-- ======================================================================= -->
## suffix/postfix

(t suffix-of s)

* `(t suffix-of s)`, if sequence `u` exists such that `s = (u x t)`
* `(t == s)`, if `s = (u x t)` for `(u = [])`
* note - `[]` is a suffix to any sequence

(t suffix-of S)

* `(t suffix-of S)`, if `(t suffix-of s)` for any `(s in S)`
* all sequences `s in S` have sequence `t` as suffix
* `t` is a common suffix of all sequences `s in S`

(T suffix-of S)

* `(T suffix-of S)`, if `(t suffix-of S)` for any `(t in T)`
* any `(t in T)` is a suffix of any sequence `(s in S)`
