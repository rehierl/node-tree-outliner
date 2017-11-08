
# Sequences

* `s` represents a sequence of elements (aka. slots)
* `s = [si] = [e1,e2,...,eN] = [e:1,...,e:N]` for `N in [0,*]`
* or, alternatively `s = (si) = (e1,e2,...,eN)`

clarification

* `domainOf(ei) := Vi` - any element has its own domain
* however, different elements may still belong to the same domain -
  e.g. `domainOf(e2), V2 := V1` is possible

clarification

* changing the value of an element results in a different sequence
* `s[i] = v` is not allowed - `e = s[i]` is allowed
* any sequence is itself a value - `e = s` is allowed

<!-- ======================================================================= -->
## is sequence

* `(is-sequence s), isSequence(s)` is true, if `s` is a sequence
* i.e. `s` has the characteristics of a sequence
* signature - (anything) -> boolean

<!-- ======================================================================= -->
## length of

* `#s, #(s), lengthOf(s), s.length, (length-of s) := N`
* `(#s length-of s)` is always true

<!-- ======================================================================= -->
## is empty

* `(is-empty s), isEmpty(s) := (#s == 0)`
* `()` and `[]` represent empty sequences
* i.e. `isEmpty(())` and `isEmpty([])` are always true

<!-- ======================================================================= -->
## n-th element of

* `s(i), s[i] := ei` for `i in [1,#s]`
* `s(i) := undefined` for `i not in [1,#s]`
* synonymous - entry, element, item

clarification

* `(si)` and `[si]` are sequences
* `s(i)` and `s[i]` are elements of a sequences

clarification

* comparison with `s[i]` is done against the element's current value
* `var = s[i]` assigns the value of element `ei` to the given variable
* the elements of a sequence themselves cannot be changed or accessed -
  i.e. sequences appear as sequences of values
* the elements of a sequence and the values they have are used synonymously

<!-- ======================================================================= -->
## is unique

* `(is-unique s), isUnique(s)` are true, if `(s(i) != s(j))`
  for any combination of indexes `i,j in [1,#s]` such that `(i != j)`
* `s` is itself unique, if all elements refer to different/unique values

<!-- ======================================================================= -->
## equality

equal by value (==)

* `(s == t)` is true, if `(#s == #t)` and `(s(i) == t(i))` for any `i in [1,#s]`
* In general, the test for equality by value must also take the domains into
  account - e.g. `(+2 != +2.0)`
* `(s != t)` => both differ in length and/or corresponding elements/values

<!-- ======================================================================= -->
## reversed sequence s'

* `s', (s)' := (f1=eN,...,fN=e1)`, if `s = (e1,...,eN)`
* `(s'(i) == s(N-i+1)` for any `i in [1,N]`

palindrome

* `s` and `s'` are palindromic sequences, if `(s == s')`
* `(s == (s')')` is always true

<!-- ======================================================================= -->
## infix, subsequence

left-bound <=> right-bound

* (left-bound, offset-based notation)
  `t = [e(l),e(l+1),...,e(l+k-1)]`
  for some `l in [1,N]` and `k in [1,(N-l)]` -
  `l` is the left border,  offset `o = l` (letter).
* (right-bound notation)
  `t = [e(r-k+1),...,e(r-k+i),...,e(r)]`
  for some `r in [1,N]`, `k in [1,r]` and `i in [1,k]` -
  `r` is the right border.

Sequence `t` is **an infix of** sequence `s`

* `t infix-of s`, if `(s(o+j) = t(j))`
  for `o in [1,N]`, `k in [1,(N-o)]` and `j in [1,k]`
* `(t subsequence-of s) := (t infix-of s)`
* signature - (sequence,sequence) -> boolean

clarification

* "subsequence" can have the following meaning:
* `s = [1, (2, 3), 4]`, `t = [2, 3]` => `s = [1, t, 4]`
* i.e. a single element of `s` has `t` as its value
* here, "subsequence" has this meaning:
* `s = [1, 2, 3, 4]`, `t = [2, 3]`
* i.e. subsequent elements of `s` match sequence `t`

clarification

* A sequence is a subsequence to itself.
* `(t == s)` => `t infix-of s` and `(#t = #s)`
* An empty sequence has no subsequence.
* `(s == s)` and `s infix-of s` are both always true.

<!-- ======================================================================= -->
## prefix

Sequence `t` is **a prefix of** sequence `s`

* `t prefix-of s`, if `t infix-of s` and offset `(o = 1)` (digit)
* `t` is bound to the 1st entry of `s`
* `s prefix-of s` is always true.
* A sequence is a prefix to itself.

Sequence `t` is **the n-th prefix of** sequence `s`

* `t n-prefix-of s`, if `t prefix-of s` and `(#t == n)`
* `prefix(s,n) = t`, if `(t n-prefix-of s)`
* The N-th prefix of a sequence is the sequence itself.

Sequence `u` is **a common prefix of** sequence `s` and sequence `t`

* `u prefix-of s,t`, if `(u prefix-of s)` and `(u prefix-of t)`
* `s` and `t` share the common prefix `u`
* `#u in [1,min(#s,#t)]`
* For any common prefix `u`, there is a `n` such that `u n-prefix-of s,t`

Sequence `u` is **the n-th common prefix of** sequences `s` and `t`

* `u n-prefix-of s,t`, if `(u prefix-of s,t)` and `(#u = n)`
* `n in [1,min(#s,#t)]`

Sequence `u` is **the common prefix of** sequence `s` and sequence `t`

* If there is no other common suffix `v` such that `(#v > #u)`
* `u max-prefix-of s,t`

<!-- ======================================================================= -->
## suffix

Sequence `t` is **a suffix of** sequence `s`

* `t suffix-of s`, if `t subsequence-of s` and `(r == N)`
* `t` is bound to the last entry of `s`
* `t` and `s` have the same order (i.e. `t` is not reversed)
* `s suffix-of s` is always true
* Any sequence is a suffix to itself.

Sequence `t` is **the n-th suffix of** sequence `s`

* `t n-suffix-of s`, if `t suffix-of s` and `(#t == n)`
* `suffix(s,n) = t`, if `(t n-suffix-of s)`
* The N-th suffix of a sequence is the sequence itself.

Sequence `u` is **a common suffix of** sequence `s` and sequence `t`

* `u suffix-of s,t`, if `(u suffix-of s)` and `(u suffix-of t)`
* `s` and `t` share the common suffix `u`
* `#u in [1,min(#s,#t)]`
* For any common suffix `u`, there is a `n` such that `u n-suffix-of s,t`

Sequence `u` is **the n-th common suffix of** sequences `s` and `t`

* `u n-suffix-of s,t`, if `(u suffix-of s,t)` and `(#u = n)`
* `n in [1,min(#s,#t)]`

Sequence `u` is **the common suffix of** sequence `s` and sequence `t`

* If there is no other common suffix `v` such that `(#v > #u)`
* `u max-suffix-of s,t`
