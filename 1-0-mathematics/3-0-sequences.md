
<!-- ======================================================================= -->
# Sequences

* `s` represents a sequence of elements/slots
* `s = [si] = [e1,e2,...,eN] = [e:1,...,e:N]` for `N in [0,*]`
* or the more mathematical notation `s = (si) = (e1,e2,...,eN)`
* the array-oriented notation is used throughout this discussion

Note that, with regards to sequences, there are no operators similar to
the set-based operators (i.e. union, intersection, etc).

clarification

* throughout the course of this discussion, the term "sequence" refers to
* a constant list of elements (fixed in length and values, immutable)
* a list of elements/values of the same kind
* a list of any length (finite or infinite)

clarification

* any sequence is itself a value
* the expressions `(e = s)`, `{ s }`, `[ s ]` are all valid

<!-- ======================================================================= -->
## is-sequence

* `(is-sequence s), isSequence(s)` are true, if `s` is a sequence
* i.e. `s` has the characteristics of a sequence

<!-- ======================================================================= -->
## length-of

* `#s, #(s), lengthOf(s), s.length, (length-of s) := N`
* `(#s is-length-of s)` is always true

<!-- ======================================================================= -->
## is-empty

* `(is-empty s), isEmpty(s) := (#s == 0)`
* `[]` represents the empty sequence
* `isEmpty([])` are always true

<!-- ======================================================================= -->
## n-th element of

* `s[i] := ei` for `i in [1,#s]`
* `s[i] := undefined` for `i not in [1,#s]`
* synonymous - entry, element, item

clarification

* the first index in a sequence is `1`
* the last index in a sequence is `#s`

clarification

* `[si]` refers to sequence `si`
* `s[i]` refers to element `si` of sequence `s`

<!-- ======================================================================= -->
## get/set access

get: (sequence, index) -> value

* `x = s[i]` assigns the value of element `si` to `x`
* it is in general not possible to directly "access/extract" any element
* i.e. `s[i]` implicitly dereferences element `si`

set: (sequence, index, value) -> sequence

* `s[i] = x` changes the value of element `si` to hold `x` as its value
* it is in general not possible to "change/replace/remove" any element
* the set-operation must be understood to create a new sequence
* i.e. `set(s,i,v) := prefix(s,1,i-1) & [v] & suffix(s,i+1,#s)`

clarification

* sequences appear as sequences of values
* the elements of a sequence and the values they hold are used synonymously

<!-- ======================================================================= -->
## equality (==, !=)

(==)

* `(s == t)` is true, if `(#s == #t)` and `(s[i] == t[i])` for any `i in [1,#s]`
* `(s == t)` compares the values of the corresponding elements
* in general, the test for equality by value must also take the domains into
  account, because `(+2 != +2.0)` is from a strict perspective true

(!=)

* `(s != t)` is true, if both sequences differ in length and/or values

<!-- ======================================================================= -->
## linear sequence

* `(is-linear s), (is-linear s) := isLinear(s)`
* `isLinear(s)` := `(s[i] != s[j])` for any `i,j in [1,#s]` and `(i != j)`

Note that a sequence is said to be linear, if the sequence holds unique/distinct
elements/values only. That is, a linear sequence contains none of its elements
more than once. As such, a linear sequence can be understood to define a simple
set of elements.

Note that a linear sequence defines an ordered set (see relations), if the
order of the elements within that sequence is understood to define the order
of elements/values within the corresponding ordered set. Depending on the
respective context, the semantics of the element order may therefore be:
e.g. `(s[i+1] subsequent-to s[i])` or `(s[i] presequent-to s[i+1])`.

Note that the word "linear" needs to be understood
in the context of a "linearly ordered set".

<!-- ======================================================================= -->
## inverse sequence (s')

* `s', inv(s) := [f1=eN,...,fN=e1]`, if `s = [e1,...,eN]`
* `(s'[i] == s[N-i+1])` for any `i in [1,N]`
* synonymous - inverse, reversed, transposed, etc.
* `inv(inv(s)) <-> s`

palindrome

* `s` is a palindromic sequence, if `(s == inv(s))`

<!-- ======================================================================= -->
## which term is appropriate?

tuples

* `t := [1, 'a']`
* an ordered list of "anything"
* in general, of finite length

sequences

* `s := [1, 2, 3, ...]`
* an enumerated collection of "something"
* of finite or infinite length
* in general, a rule exists such that subsequent elements
  in a sequence can be calculated from presequent ones
* e.g. `an := a(n-2) + a(n-1)` (Fibonacci)

strings

* `s := ['a', 'b', 'a', 'c', ...]`
* traditionally a sequence of characters
* elements are selected from an alphabet
* fixed, or allows to change its elements

vectors

* `v := [1.0, 2.0, 3.0]`
* in general, an element of the real coordinate space (R^n)
