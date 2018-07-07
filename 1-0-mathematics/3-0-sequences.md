
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
## which term is to use?

tuples

* `t := [1, 'a']`
* an ordered list of "anything"
* in general of finite length

sequences

* `s := [1, 2, 3, ...]`
* an enumerated collection of "something"
* of finite or infinite length
* in general a rule exists such that subsequent elements
  in a sequence can be calculated from presequent ones
* e.g. `an := a(n-2) + a(n-1)` (Fibonacci)

strings

* `s := ['a', 'b', 'a', 'c', ...]`
* traditionally a sequence of characters
* elements are selected from an alphabet
* in computing generalized into a sequence of binary data of sorts
* depending on the context, a mutable/immutable sequence

vectors

* `v := [1.0, 2.0, 3.0]`
* in general an element of the real coordinate space (R^n)

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
## index-of

* `indexOf(s,e)` := the 1-based index of element `e` in sequence `s`
* `idx(s,e), index(s,e) := indexOf(s,e)`

Note that the index of an element is undefined, if that element turns out to
be not an element of the input sequence.

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
## inverse sequence (s')

* `s', inv(s) := [f1=eN,...,fN=e1]`, if `s = [e1,...,eN]`
* `(s'[i] == s[N-i+1])` for any `i in [1,N]`
* synonymous - inverse, reversed, transposed, etc.
* `inv(inv(s)) <-> s`

palindrome

* `s` is a palindromic sequence, if `(s == inv(s))`

<!-- ======================================================================= -->
## linear sequence

* `(is-linear s), (is-linear s) := isLinear(s)`
* `isLinear(s)` := `(s[i] != s[j])` for any `i,j in [1,#s]` and `(i != j)`

A sequence is said to be linear, if the sequence holds unique/distinct elements
only. That is, a linear sequence contains none of its elements more than once.
As such, a linear sequence can be understood to define a simple set of elements.

In addition to that, a linear sequence defines an ordered set (see relations),
if the order of positions is understood to correspond with the set's order of
elements. Depending on the respective context, the semantics of the element
order may therefore be:

* `(s[i] before s[i+1])`, `(s[i] presequent-to s[i+1])`
* `(s[i+1] after s[i])`, `(s[i+1] subsequent-to s[i])`

The word "linear" therefore needs to be understood
with regards to the "linear order" it defines.

Note that set-based operators can be used in combination with linear sequences.
