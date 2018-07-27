
<!-- ======================================================================= -->
# Sequences

```
sequences
------------------------
order:    o1 o2
          |  |  - linear
elements: e1 e2
          | /
values:   v1
```

* see "sequences" for in-depth discussions on sequences
* note - (&) represents the concatenation operator

<!-- ======================================================================= -->
## core concept

* values may be grouped into sequences of values
* sequences are complex values

`s = [si] = [v1,v2,...,vN]` for `N in [0,*]`

* or the more mathematical notation `s = (si) = (v1,v2,...,vN)`
* the array-oriented notation is in general used throughout this discussion

`s := [e1,e2,...,eN]`

* a sequence can be understood to hold one element/slot per value
* the number of elements in a sequence is referred to as its "length"
* the elements within a sequence are ordered
* i.e. sequences have a first/last element/value
* any element may hold the value of another element
* i.e. in general no restriction of which value an element may hold
* i.e. a `1:N` relationship between values and elements
* `(vi != vj) -> (ei !== ej)`, but not vice versa

Note that, with regards to sequences, there are no operators that correspond
with the set-based operators (i.e. union, intersection, etc).

clarification

* throughout the course of this discussion, the term "sequence" refers to
* a constant/immutable list of values - i.e. fixed in length and values
* a list of elements/values of the same kind
* a list of any length (finite or infinite)

clarification

* any sequence is itself a value
* the expressions `(e = s)`, `{ s }`, `[ s ]` are all valid expressions

<!-- ======================================================================= -->
## which term to use?

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

* `s := ['a', 'b', 'a', 'c', ...] := "abac..."`
* traditionally a sequence of characters
* elements are selected from an alphabet
* in computing generalized into a sequence of binary data of sorts
* depending on the context, a mutable/immutable sequence

vectors

* `v := [1.0, 2.0, 3.0]`
* in general an element of the real coordinate space (R^n)

<!-- ======================================================================= -->
## is-sequence

* `isSequence(s)` are true, if `s` is a sequence of values
* i.e. `s` has the characteristics of a sequence
* `(is-sequence s) := isSequence(s)`

Note that `isMultiSet(s)` is understood to be true for sequences.

<!-- ======================================================================= -->
## a sequence is a specialized multiset

* "specialized" such that the elements within a sequence are ordered

a sequence adopts the following definitions:

* a sequence of X, a sequence of atomic values
* a homogenous/heterogenous sequence of values
* multiplcitiyOf()
* lengthOf() := cardinalityOf()
* isEmpty(), `[]` represents an empty sequence
* (v in S), oneElementOf()

<!-- ======================================================================= -->
## add, remove

* e.g. `s := [ 1, 2, 3, 2 ]`

add(x,s)

* `add(v,s) := (s & v)`
* i.e. append value `v` to the end of sequence `s`
* e.g. `add(4,s) = [ 1, 2, 3, 2, 4 ]`

remove(x,s)

* `remove(x,s)` := remove the first element that holds value `x`
* i.e. subsequent elements will shift by one "place" to maintain the order
* i.e. remove() will not return a "gapped" sequence
* e.g. `remove(2,s) = [ 1, 3, 2 ]`

note that ...

* the basic semantics of add() with regards to multisets is maintained
* i.e. add() will increase the multiplicity of `x` in `s` by `1`
* the basic semantics of remove() with regards to multisets is maintained
* i.e. remove() will decrease the multiplicity of `x` in `s` by `1`

<!-- ======================================================================= -->
## (consistent) iteration

```
traceOf(s) begin
  t = new sequence()
  for e in s begin
    t.add(e.value)
  end
  return t
end

s = < 1, 2, 2, 3 >
s1 = traceOf(s) //- e.g. [ 1, 2, 2, 3 ]
s2 = traceOf(s) //- e.g. [ 1, 2, 2, 3 ]
```

* any sequence of values allows to iterate over its elements
* the iteration will visit the elements in order - i.e. from first to last
* subsequent iterations will visit the elements in the exact same order
* i.e. `s1` is guaranteed to be identical to `s2`

<!-- ======================================================================= -->
## index-of

```
firstIndexOfValue(x,seq) begin
  index = 1
  for e in seq begin
    if (e.value == x) begin
      return index
    end
    index = index + 1
  end
  return 0
end
```

* `indexOf(x,s) := firstIndexOfValue(x,s)`
* note the 1-based index of a value, not of an element

Note that the index of a value is undefined (i.e. zero/0),
if its multiplcitiy within `s` is zero/0.

<!-- ======================================================================= -->
## n-th element/value of

```
elementAt(pos,seq) begin
  index = 1
  for e in seq begin
    if (index == pos) begin
      return e
    end
    index = index - 1
  end
  throw new ElementNotFoundException()
end
```

* `s[i] := ei` for `i in [1,#s]`
* `s := [e1, e2, ..., eN] = [s[1], s[2], ..., s[N]]`
* `s[i] := undefined` for `i !in [1,#s]`
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

* `x = s[i]` assigns the value of element `si` to `x`
* i.e. it is not possible to directly access an element of a complex value
* i.e. `s[i]` implicitly dereferences element `si`

set: (sequence, index, value) -> new-sequence

* it is in general not possible to "change/replace/remove" any element
* the set-operation must be understood to return a new sequence
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
  account, because `(+2 == +2.0)` is `false` from a strict perspective

(!=)

* `(s != t)` is true, if both sequences differ in length and/or values

<!-- ======================================================================= -->
## inverse sequence (s')

* `s', inv(s) := [f1=eN,...,fN=e1]`, if `s = [e1,...,eN]`
* `(s'[i] == s[N-i+1])` for any `i in [1,N]`
* synonymous - inverse, reversed, transposed, etc.
* `(s == inv(inv(s)))`

palindrome

* `s` is a palindromic sequence, if `(s == inv(s))`
