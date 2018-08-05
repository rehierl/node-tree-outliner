
<!-- ======================================================================= -->
# Core terms used

* term "sequence" will be used in the course of this discussion

tuples

* `t := [1, 'a'] := (1,a)`
* an ordered list of "anything"
* in general of finite length

sequences

* `s := [1, 2, ...] := (1,2, ...)`
* an enumerated collection of "something"
* of finite or infinite length
* in general a rule exists such that subsequent elements
  in a sequence can be calculated from presequent ones
* e.g. `an := a(n-2) + a(n-1)` (Fibonacci)

strings

* `s := ['a', 'b', 'a', 'c', ...] := "abac..."`
* traditionally a sequence of characters
* elements are selected from an alphabet
* in computing generalized into a sequence of binary data of sorts
* depending on the context, a mutable/immutable sequence

vectors

* `v := [1.0, 2.0, 3.0] := < 1, 2, 3 >`
* in general an element of the real coordinate space (R^n)

<!-- ======================================================================= -->
## wikipedia, tuples

* a finite ordered list of elements
* n-tuple - a list of `n` elements, where `(n in [0,*])`
* 0-tuple - null-tuple, an empty list - i.e. `()`
* 1-tuple - singleton - i.e. `(a)`
* 2-tuple - ordered pair - i.e. `(a,b)`
* 3-tuple - triple, triplet - i.e. `(a,b,c)`
* used as an abstraction of sequences

definition

* `(a1,...,an) = (b1,...,bn)` iff `(ai=bi)` for any `(i in [1,n])`
* both tuples must have the same length - i.e. `n`
* `(ai = aj)` may be true for some `(i,j in [1,n])`
* `(a,b) != (b,a)` if `(a != b)` - i.e. ordered
* tuples always have finite length

tuples as functions

* domain X is the implicit set of element indexes
* codomain Y is the tuple's set of elements/values
* i.e. `(f: [1,*] -> Y)` - i.e. `t := (f(1),...,f(n))`

tuples as nested ordered pairs

* 0-tuple - `()` or `Ø`
* n-tuple - `t := (a1,...,((an-1),(an,{}))...)`
* n-tuple - `t := (...((Ø,a1),a2),...,an)`

tuples as nested sets

* Kuratowski's definition
* `(x -> y) := {{x},{x,y}}`
* 0-tuple - `()` => `Ø`
* 1-tuple - `(a)` => `(Ø -> a)` => `{{Ø},{Ø,a}}`
* 2-tuple - `(a,b)` => `{ (a), {(a),b} }`
* 2-tuple - `(a,b)` => `{ {{Ø},{Ø,a}}, { {{Ø},{Ø,a}}, b } }`
* 3-tuple - `(a,b,c)` => `{ (a,b), {(a,b),c} }`
* note - a linear subset-of relationship

implementations

* directly as (ordered) product types
* i.e. accessed by indexes
* alternatively as (unordered) record types
* i.e. accessed by labels

<!-- ======================================================================= -->
## wikipedia, unordered pair

* a (multi-)set of the form {a,b}
* i.e. no particular relation between (a) and (b)
* aka. 2-set, binary set, etc.
* aka. an unordered n-tuple
* i.e. {a1,a2,...,an}
* i.e. {a,b} == {b,a}

remarks

* unordered tuples - aka. multisets

<!-- ======================================================================= -->
## wikipedia, ordered pair

* a pair of objects in which the order of an object is significant
* i.e. has first and second/last element/component/coordinate
* `(a1,b1) = (a2,b2)` iff `(a1=a2)` and `(b1=b2)`
* (a,b) in (A × B) - Cartesian product
* several formal definitions possible
* e.g. Kuratowski's definition

<!-- ======================================================================= -->
## wikipedia, product type

* in programming languages and type theory
* a product of types is a compounded type in a structure
* multiple types -> compound/combined/complex/tuple type
* A × B × ... -> (A,B,...)
* i.e. retains the fixed order
* instances - (a,b,...)
* e.g. a vector in a vector space

<!-- ======================================================================= -->
## wikipedia, record type

* aka. record, structure, compound
* a collection of fields fixed in number and sequence
* fields "addressed" via labels - i.e. "unordered"
* a record type describes such compound values

<!-- ======================================================================= -->
## wikipedia, sequences

<!-- ======================================================================= -->
## wikipedia, strings

* a sequence of characters or more general a list of some other data
* formal - a finite sequence of symbols over the non-empty alphabet (A)
* no assumption is made about the nature of the symbols within A
* `#s`, `|s|`, length := the number of symbols within the string
* A{n} := the set of strings of length `n`
* A* := the countably infinite set of strings of any length
* A* - aka. Kleene closure of A
* B is a formal language over A, if (B subset-of A*)

concatenation: (A*,A*) -> A*

* synonymous - concatenation, concat, add, append, &, +
* associative, non-commutative
* e, eps, epsilon, "" - the empty string, the identity element
* `(s × e) = (e × s) = s`
* i.e. append and A* form a monoid
* length() defines a monoid homomorphism from A* to [0,*]
* `t` is a substring-of `s`, iff `u` and `v` exist such that `s = (u × t × v)`
* substring-of defines a partial order on A*
* i.e. the least element element is eps

prefix, suffix

* `t` is a prefix-of `s`, iff `u` exists such that `s = (t × u)`
* `t` is a suffix-of `s`, iff `u` exists such that `s = (u × t)`
* strict/proper prefix/suffix if (u != eps)
* any prefix/suffix is also a substring
* prefix-of and suffix-of form prefix-orders

remarks

* rotation - `t = uv` is a rotation of `s = vu`
* reversal - `t = abc` is reverse to `s = cba`

**SKIPPED** - implementation-specific aspects

<!-- ======================================================================= -->
## wikipedia, infix

<!-- ======================================================================= -->
## wikipedia, prefix

<!-- ======================================================================= -->
## wikipedia, suffix
