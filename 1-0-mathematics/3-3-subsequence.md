
<!-- ======================================================================= -->
# Subsequence

Note that the definition of "subsequence" in the context of this discussion
deviates from the mathematical definition in such a way that a subsequence
represents an exact pattern within the another sequence (i.e. contiguous/
consecutive/ no gaps). In general, the definition used here is more strict
and needs to be understood with the notion of "substring".

Note that a "subsequence" is similar to, but more complex than "subset".
The additional complexity is a result of the element order, which a set
of elements does not have.

<!-- ======================================================================= -->
## functions

* function `f: A -> B`

range

* domain of a function - `A`
* image of a function - `I := { f(x) | x in A }`
* codomain of a function - `B` where `(I subset-of B)`
* range of a function - the function's codomain, or its image

region

* in general an open subset of `R^N` or `C^N` (real/complex numbers)
* often used as domains of functions

<!-- ======================================================================= -->
## substring

```
s = [ a, b, c, d, e, f, g, h, i, ... ]
t = [          d, e, f,    h         ]
u = [          d, e, f, g            ]
```

* `u` is a substring of `s`
* with regards to `s`, `u` is said to be **consecutive**
* `t` is not a substring of `s`
* with regards to `s`, `t` is said to **have gaps**

clarification

* an infix/prefix/suffix is a substring
* a super-string is said to contain its substrings
* a substring is a sequence of contiguous/consecutive elements

<!-- ======================================================================= -->
## interval

* a set of numbers such that any number in between is included
* (almost) synonymous - interval, segment

terminology

* bounded, left-bounded, right-bounded, half-bounded intervals
* finite, infinite intervals
* diameter - the absolute difference between both endpoints
* synonymous - diameter, length, width, size, measure
* center/midpoint (i.e. (a+b)/2) - radius (i.e. |a-b|/2)
* closed, left-closed, right-closed - has a minimum/maximum or both
* interior - the set of points that are no endpoints (open)
* closure of I - the smallest closed interval that contains I

segment vs. interval

* interval (open, no endpoints) - segment (closed, with endpoints)
* but, also used with opposite meaning
* interval (closed) - segment (open)

Note that, in order to "know" what is in between both borders,
you need to know the corresponding set and the order of elements:

* `[c, f]` represents an interval of characters
* one needs to know that the corresponding set is the set of characters
* `S := {a, z, x, f, h, i, ...}`
* one needs to know that the elements in `S` are ordered alphabetically
* note - the "order" is implied by the interval `[c,f]` => `(c <= f)`
* `A := { char | (a <= char) }, B := { char | (char <= b) }`
* `A := { c, d, e, f, ... }, B := { f, e, d, c, ... }`
* the set of elements of an interval is the intersection of both sets
* `I := [c, f] = (A & B) = { c, d, e, f }`

Note that an interval of indexes can be understood to define a substring
in the context of a known ordered set of values. That is, if the borders
are understood to index the endpoints (e.g. `I:=[1,3]` defines substring
`s:=[a,b,c]` with regards to the above ordered set of lower-case letters).

Multi-dimensional intervals are subsets of `(I1 X I2 X ...X IN)`. These define
squares/rectangles for `(N=2)`, cubes for `(N=3)`, or in general N-dimensional
hypercubes.

<!-- ======================================================================= -->
## subsequence

* in mathematics, sequence `t` is a subsequence of sequence `s`,
  because it was derived from `s` by removing one or more values
* i.e. without changing the order of these values
* based on that definition, `[]` is a subsequence to any sequence

```
s = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
t = [          3,    5, 6,         ]
u = [          3, 4, 5, 6,         ]
```

* `t` and `u` are both subsequences of `s`
* that is, even though `t` "has gaps"

Note that, with regards to `s`, the elements in `u` are said to be consecutive
or strictly subsequent. In contrary to that, the elements in `t` are said to be
(merely) loosely subsequent.

<!-- ======================================================================= -->

* `(t subsequence-of s) := (t infix-of s)`
* `t strict-infix-of s`, if `(t infix-of s)` and `(t != s)`
* `(t strict-subsequence-of s) := (t strict-infix-of s)`

element-of vs. subsequence-of

* `s = [1, [2, 3], 4]`, `t = [2, 3]`
* `t` is an element of `s = [1, t, 4]`
* that is, an element in `s` has `t` as its value
* `s = [1, 2, 3, 4]`, `t = [2, 3]`
* `t` is an infix/subsequence of `s`

clarification

* a sequence is a subsequence, but not a strict subsequence to itself
* `(t == s)` => `(t infix-of s)` and `(#t == #s)`
* `(s == s)` and `(s infix-of s)` are both always true

**TODO** -
clarification

* the empty sequence has no subsequence (`s[i]` is undefined)
* the empty sequence is no subsequence to any sequence
