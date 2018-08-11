
<!-- ======================================================================= -->
# Sequences

```
sequences
----------------------
order:      o1 o2
            |  |  - linear
components: c1 c2
            | /
elements:   v1
```

* see "sequences" for further details
* "sequence" is the term that will be used throughout this discussion

<!-- ======================================================================= -->
## core concept

* values may be grouped into sequences of elements
* sequences are complex values

`s = [si] = [v1,v2,...,vN]` for `N in [0,*]`

* or the more mathematical notation `s = (si) = (v1,v2,...,vN)`
* the array-oriented notation is in general used throughout this discussion

`s := [c1,c2,...,cN] := [e1,e2,...,eN]`

* a sequence can be understood to hold one component per element
* the number of components in a sequence is referred to as its "length"
* the components within a sequence are ordered
* i.e. sequences have a first/last component
* any component may hold the element of another component
* i.e. in general no restriction of which element a component may hold
* i.e. a `1:N` relationship between elements and components
* `(vi != vj) -> (ei !== ej)`, but not vice versa

Note that, with regards to sequences, there are no operators that correspond
with the set-based operators (i.e. union, intersection, etc).

clarification

* throughout the course of this discussion, the term "sequence" refers to
* a constant/immutable list of elements - i.e. fixed in length and elements
* not necessarily a list of elements of the same kind
* a list of any length (finite or infinite)

clarification

* any sequence `s` is itself a value
* the expressions `(v = s)`, `{s}`, `[s]` are all valid expressions

<!-- ======================================================================= -->
## is-sequence

* `isSequence(s)` are true, if `s` is a sequence of values
* i.e. `s` has the characteristics of a sequence
* `(is-sequence s) := isSequence(s)`

Note that `isMultiSet(s)` is understood to be true for sequences.

<!-- ======================================================================= -->
## sequences are specialized multisets

* "specialized" such that the components within a sequence are ordered
* i.e. the order of components may carry over to its elements
* i.e. the components are ordered, not the elements

a sequence adopts the following definitions:

* a sequence of X, a sequence of atomic elements, etc.
* a homogenous/heterogenous sequence of elements
* multiplcitiyOf(), isEmpty()
* lengthOf() := cardinalityOf()
* `()` and `[]` both represent empty sequences
* (v in S), oneElementOf()

<!-- ======================================================================= -->
## (consistent) iteration

```
traceOf(s) begin
  t = ()
  for c in s begin
    t = (t × c.value)
  end
  return t
end

s = [ 1, 2, 2, 3 ]
s1 = traceOf(s) //- e.g. [ 1, 2, 2, 3 ]
s2 = traceOf(s) //- e.g. [ 1, 2, 2, 3 ]
```

* (×) represents the concatenation operator for sequences
* any sequence of elements allows to consistently iterate over its components
* the iteration will visit the components in order - i.e. from first to last
* subsequent iterations will visit the components in the exact same order
* i.e. `s1` is guaranteed to always be identical to `s2`

<!-- ======================================================================= -->
## add, remove

* e.g. `s := [ 1, 2, 3, 2 ]`

add(x,s)

* `add(v,s) := (s append v) := (s × v)`
* i.e. append value `v` to the end of sequence `s`
* e.g. `add(4,s) = [ 1, 2, 3, 2, 4 ]`

remove(x,s)

* `remove(x,s)` := remove the first component that holds value `x`
* i.e. subsequent components will shift by one "place" to maintain the order
* i.e. remove() will not return a "gapped" sequence
* e.g. `remove(2,s) = [ 1, 3, 2 ]`

note that ...

* the basic semantics of add() with regards to multisets is maintained
* i.e. add() will increase the multiplicity of `x` in `s` by `1`
* the basic semantics of remove() with regards to multisets is maintained
* i.e. remove() will decrease the multiplicity of `x` in `s` by `1`

<!-- ======================================================================= -->
## index-of

```
firstIndexOf(v,seq) begin
  index = 1
  for c in seq begin
    if (c.value == v) return index
    index = index + 1
  end
  return 0
end
```

* `indexOf(v,s) := firstIndexOf(v,s)`
* note the 1-based indexes

Note that the index of a value is undefined (i.e. zero/0),
if its multiplicity within `s` is zero/0.

<!-- ======================================================================= -->
## (v in s), element-of

* (v in s) := (indexOf(v,s) > 0)
* (v element-of s), elementOf(v,s) := (v in s)
* (s contains v), (v belongs-to s) := (v in s)

<!-- ======================================================================= -->
## n-th element of

```
elementAt(index,seq) begin
  if (index < 1) or (index > #seq) then
    throw new IndexOutOfRangeException()
  end if
  for c in seq begin
    if (index <= 1) return c.value
    index = index - 1
  end
end
```

* `s[i] := ei` for `i in [1,#s]`
* `s := [e1, e2, ..., eN] = [s[1], s[2], ..., s[N]]`
* `s[i] := undefined` if `not (i in [1,#s])`
* e.g. `s[i]` is undefined if `(s == [])`
* synonymous - entry, element, item

clarification

* the first index in a sequence is `1`
* the last index in a sequence is `#s`
* i.e. one/1-based, not zero/0-based indexes

clarification

* `[si]` refers to sequence `si`
* `s[i]` refers to element `si` of sequence `s`

<!-- ======================================================================= -->
## get/set access

get: (sequence, index) -> element

* `x = s[i]` assigns element `si` to `x`

set: (sequence, index, element) -> new-sequence

* it is in general not possible to "change/replace/remove" any element
* the set-operation must be understood to return a new sequence
* i.e. `set(s,i,v) := prefix(s,1,i-1) × [v] × suffix(s,i+1,#s)`

<!-- ======================================================================= -->
## equality (==, !=)

(==)

* `(s == t)` is true, if `(#s == #t)` and `(s[i] == t[i])` for any `i in [1,#s]`
* i.e. implicitly compares the elements of the corresponding components
* in general, the test for equality by element must also take the domains
  into account, because `(+2 == +2.0)` is from a strict perspective `false`
* i.e. integer values aren't identical to floating point values

(!=)

* `(s != t)` is true, if both sequences differ in length and/or elements

<!-- ======================================================================= -->
## subsequences

subsequence - the generalized, removal-based definition

* `(t subsequence-of s)` := `t` is derived from `s` removing elements
* given sequence `s=[a,b,c,d,e]`, then `t=[b,d]` is a subsequence of `s`
* `s` is referred to as the "super-sequence" and `t` as the "sub-sequence"
* note - the empty sequence `[]` is a subsequence to any sequence
* note - any sequence is a subsequence to itself

substring - the concatenation-based definition

* (×) represents the concatenation operator
* `(t,u,v substring-of s)`, if `s = (t × u × v)`
* `s` is referred to as the "super-string" and `t,u,v` as "sub-strings"
* note - subsequences are not required to be non-empty
* `(t infix-of s)`, if `s == (u × t × v)` for some `u,v`
* `(t prefix-of s)`, if `s == (t × u)` for some `u`
* `(t suffix-of s)`, if `s == (u × t)` for some `u`
* note - the empty string `""` or `[]` is a substring to any string
* note - any string is a substring to itself

Note that the focus of this discussion is on substrings rather than the general,
removal-based subsequences. That is, the exact pattern of a substring appears
within a given super-string. In addition to that, and because characters are
not the focus of this discussion, the term "subsequence" is used as if it were
defined using the concatenation operation.

* synonymous - subsequence, substring, infix

<!-- ======================================================================= -->
## inverse sequence (°)

* `s°, inv(s) := [f1=eN,...,fN=e1]`, if `s = [e1,...,eN]`
* `(s°[i] == s[N-i+1])` for any `(i in [1,N])`
* synonymous - inverse, reversed, transposed, etc.
* `(s == inv(inv(s)))`

remarks

* `s` is a palindromic sequence, if `(s == inv(s))`
* involution - s=(s°)°
