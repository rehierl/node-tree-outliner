
<!-- ======================================================================= -->
# E() - Set of elements

* the basic notion of the E() operator is as follows:
* E(x) := "the set of elements within the supplied atomic/complex value"

Note that the E() operation is basically the union of a given set/sequence
of elements. That is, if `S` is a given set/sequence, then `E(S)` is the
union set over all elements in `S`.

* if `S := {}`, then ...
* `E(S), +(S) := {}`
* `&(S) := U`

<!-- ======================================================================= -->
## definition of E()

**atomic values**

* E(v) := { v }

**complex values of atomic values**

* E(c) := { v | (v in c) }
* a multiset (ms) is a simple set, iff (#E(ms) == #ms)
* i.e. all multiplicities are reduced to 1
* a sequence (s) is an "ordered set", iff (#E(s) == #s)
* (E(s) == s) is true iff (s) is a simple set

**complex values of complex values**

* the recursive definition:
* E(c) := union of all E(v) for (v in c)
* i.e. (E(s) == s) is never true

If E(c) is defined recursively, and if all complex values only hold atomic
ex-or complex values, then E(c) will only hold atomic values. That is, E(c)
would completely resolve all complex values. This however is not intended.

* the non-recursive definition (i.e. default):
* E(c) := { w | for all (v in c) and all (w in E(v)) }
* i.e. (E(s) == s) is never true

The intention of the E(c) operator with regards to complex values is for it to
be used in combination with "sets of sets" or "sets of sequences". The intended
purpose is therefore to only resolve the complex elements within the given set.
That is, to create a set of all those elements that are elements of the complex
values within the given set. Hence, only the 1st level is to be resolved.

**example**

* c := { ({a},{b}), ({b},{c}) }
* E(c) := { {a}, {b}, {c} } - the intended result
* E(c) := { a, b, c } - not the intended result
