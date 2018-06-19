
<!-- ======================================================================= -->
# Sequences

* `s` represents a sequence of elements (aka. slots)
* `s = [si] = [e1,e2,...,eN] = [e:1,...,e:N]` for `N in [0,*]`
* or, alternatively `s = (si) = (e1,e2,...,eN)`

tuple vs. sequence

* tuple - an ordered list of anything - e.g. `(1, 'a')`
* sequence - an ordered list of something - e.g. `(1, 2, 3, ...)`
* in general, a rule exists such that subsequent elements in a sequence can be
  calculated from presequent ones - e.g. `an := a(n-2) + a(n-1)` (Fibonacci)
* here, the meaning of "sequence" will shift from the notion of a tuple towards
  the notion of a mathematical sequence. that is, the term "sequence" will be
  used for both constructs, regardless of their exact characteristics.

clarification

* `dom(ei) := Vi` - any element has its own domain
* different elements may belong to (1) the same domain, or (2) different domains
* e.g. `dom(e2) := V2`, but `V2 := V1` is possible, as is `(e2 == e1)`

clarification

* changing the value of an element results in a different sequence
* `s[i] = v` (changing an element) is not allowed
* `e = s[i]` (extraction) is allowed
* any sequence is itself a value - `e = s` is allowed

set of values

* a set of values `V` contains basic values only
* `(is-set v)` is false for any `v in V`
* `(is-sequence v)` is false for any `v in V`
* the elements of such a set appear to be atomic
* an atomic set -or- a set of atomic values

set of sequences

* a set of sequences `S` contains sequences only
* `(is-sequence s)` is true for any `s in S`
* any sequence `s in S` may have any length - i.e. `#s in [0,*]`
* `(#si != #sj)` may be true for any two sequences `(si !== sj)`

<!-- ======================================================================= -->
## is-sequence

* `(is-sequence s), isSequence(s)` are true, if `s` is a sequence
* i.e. `s` has the characteristics of a sequence
* signature - (anything) -> boolean

<!-- ======================================================================= -->
## length-of

* `#s, #(s), lengthOf(s), s.length, (length-of s) := N`
* `(#s is-length-of s)` is always true

<!-- ======================================================================= -->
## is-empty

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
* the elements of a sequence themselves cannot be changed or accessed
* i.e. sequences appear as sequences of values
* the elements of a sequence and the values they have are used synonymously

<!-- ======================================================================= -->
## is-unique

* `(is-unique s), isUnique(s)` are true, if `(s(i) != s(j))`
  for any combination of indexes `i,j in [1,#s]` such that `(i != j)`
* `s` is itself unique, if all elements have different/unique values

<!-- ======================================================================= -->
## equality (==, !=)

* `(s == t)` is true, if `(#s == #t)` and `(s(i) == t(i))` for any `i in [1,#s]`
* in general, the test for equality by value must also take the domains into
  account - e.g. `(+2 != +2.0)`
* `(s != t)` => both differ in length and/or corresponding elements/values

<!-- ======================================================================= -->
## inverse sequence (s')

* `s', (s)', inv(s) := (f1=eN,...,fN=e1)`, if `s = (e1,...,eN)`
* `(s'(i) == s(N-i+1)` for any `i in [1,N]`
* synonymous - inverse, reversed, transposed, etc.
* `inv(inv(s)) <=> s`

inverted set of sequences (S')

* `S', (S)', inv(S) := { inv(s) : s in S }`
* `inv(inv(S)) <=> S`

palindrome

* `s` is a palindromic sequence, if `(s == inv(s))`

<!-- ======================================================================= -->
## infix, subsequence

```
t = [ t(1),     t(2),     ..., t(N-1),   t(N) ]     // default notation
t = [ t(l),     t(l+1),   ..., t(l+k-2), t(l+k-1) ] // left-bound notation
t = [ t(r-k+1), t(r-k+2), ..., t(r-1),   t(r) ]     // right-bound notation
```

left-bound <=> right-bound

* (left-bound, offset-based notation)
  `t = [e(l),e(l+1),...,e(l+k-1)]`
  for `l = 1` and `k in [1,(N-1)]` -
  `l` is the (l)eft border,  (o)ffset `o = l`.
* (right-bound notation)
  `t = [e(r-k+1),...,e(r-1),e(r)]`
  for some `r = N` and `k in [1,N]` -
  `r` is the (r)ight border.

```
s = [ s(1), s(2), ..., s(o), s(o+1), ..., s(o+n), s(o+n-1), ..., s(N) ]
t = [                  t(1), t(2),   ..., t(n-1), t(n)                ]
```

Note that this definition of "subsequence" deviates from the mathematical
definition in such a way that a subsequence must represent an exact pattern
within the other sequence (i.e. no gaps allowed). As such this definition
is more strict and needs to be understood with the notion of "substring".

sequence `t` is **an infix/subsequence of** sequence `s`

* `t infix-of s`, if `(s(o+j-1) = t(j))`
  for `o in [1,N]`, `n in [1,(N-o+1)]` and all `j in [1,n]`
* `(t subsequence-of s) := (t infix-of s)`
* signature - (sequence,sequence) -> boolean

sequence `t` is **a strict infix/subsequence of** sequence `s`

* `t strict-infix-of s`, if `(t infix-of s)` and `(t != s)`
* `(t strict-subsequence-of s) := (t strict-infix-of s)`

clarification

* "subsequence" can have the following meaning:
* `s = [1, (2, 3), 4]`, `t = [2, 3]` => `s = [1, t, 4]`
* i.e. a single element of `s` has `t` as its value
* here, "subsequence" has the following meaning:
* `s = [1, 2, 3, 4]`, `t = [2, 3]`
* that is, based on `t infix-of s` being true

clarification

* a sequence is a subsequence, but not a strict subsequence to itself
* `(t == s)` => `t infix-of s` and `(#t = #s)`
* an empty sequence has no subsequence (`s(i)` is undefined)
* `(s == s)` and `s infix-of s` are both always true

<!-- ======================================================================= -->
## prefix

sequence `t` is **a prefix of** sequence `s`

* `t prefix-of s`, if `t infix-of s` and offset `(o = 1)`
* `t` is bound to the 1st entry of `s`
* `s prefix-of s` is always true
* a sequence is a prefix to itself

sequence `t` is **a strict prefix of** sequence `s`

* `t strict-prefix-of s`, if `(t prefix-of s)` and `(t != s)`

sequence `t` is **the n-th prefix of** sequence `s`

* `t n-prefix-of s`, if `t prefix-of s` and `(#t == n)`
* `prefix(s,n) = t`, if `(t n-prefix-of s)`
* the n-th prefix of a sequence is the sequence itself

sequence `u` is **a common prefix of** sequence `s` and sequence `t`

* `u prefix-of s,t`, if `(u prefix-of s)` and `(u prefix-of t)`
* `s` and `t` share the common prefix `u`
* `#u in [1,min(#s,#t)]`
* for any common prefix `u`, there is a `n` such that `u n-prefix-of s,t`

sequence `u` is **the n-th common prefix of** sequences `s` and `t`

* `u n-prefix-of s,t`, if `(u prefix-of s,t)` and `(#u = n)`
* `n in [1,min(#s,#t)]`

sequence `u` is **the common prefix of** sequence `s` and sequence `t`

* `u max-prefix-of s,t`, is true if ...
* `u` is the longest common prefix of both sequences
* if there is no other common prefix `v` such that `(#v > #u)`

<!-- ======================================================================= -->
## suffix

sequence `t` is **a suffix of** sequence `s`

* `t suffix-of s`, if `t subsequence-of s` and `(r == N)`
* `t` is bound to the last entry of `s`
* `t` and `s` have the same order (i.e. `t` is not reversed)
* `s suffix-of s` is always true
* any sequence is a suffix to itself

sequence `t` is **a strict suffix of** sequence `s`

* `t strict-suffix-of s`, if `(t suffix-of s)` and `(t != s)`

sequence `t` is **the n-th suffix of** sequence `s`

* `t n-suffix-of s`, if `t suffix-of s` and `(#t == n)`
* `suffix(s,n) = t`, if `(t n-suffix-of s)`
* the n-th suffix of a sequence is the sequence itself

sequence `u` is **a common suffix of** sequence `s` and sequence `t`

* `u suffix-of s,t`, if `(u suffix-of s)` and `(u suffix-of t)`
* `s` and `t` share the common suffix `u`
* `#u in [1,min(#s,#t)]`
* for any common suffix `u`, there is a `n` such that `u n-suffix-of s,t`

sequence `u` is **the n-th common suffix of** sequences `s` and `t`

* `u n-suffix-of s,t`, if `(u suffix-of s,t)` and `(#u = n)`
* `n in [1,min(#s,#t)]`

sequence `u` is **the common suffix of** sequence `s` and sequence `t`

* `u max-suffix-of s,t`, is true if ...
* `u` is the longest common suffix of both sequences
* if there is no other common suffix `v` such that `(#v > #u)`
