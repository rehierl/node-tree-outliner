
<!-- ======================================================================= -->
# Subsequence

Note that the definition of "subsequence" in the context of this discussion
deviates from the mathematical definition in such a way that a subsequence
represents an exact pattern that can be located within another sequence (i.e.
contiguous/ consecutive/ no gaps). In general, the definition used here is
more strict and needs to be understood to be similar to the definition of
"substring".

Note that the definition of "subsequence" is similar to, but more complex than
the definition of "subset". The additional complexity is a result of the element
order, which does not have to be taken into account in the context of sets of
elements.

<!-- ======================================================================= -->
## functions

* function `f: A -> B`

input set

* domain of a function - `A`
* the set of all values for which `f` is defined
* the domain of `f` does not include values for which `f` is undefined

output set, range

* range of a function - the function's codomain, or its image
* codomain of a function - `B` where `(I subset-of B)`
* image of a function - `I := { f(x) | x in A }`

region

* in general an open subset of `R^N` or `C^N` (real/complex numbers)
* "open" in the context of intervals?
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

* an interval is a set of numbers
* such that any number in between its endpoints is included

endpoint-related terms

* left/right endpoint - minimum/maximum
* finite, infinite intervals
* bounded, left-bounded, right-bounded, half-bounded
* closed, left-closed, right-closed - has a minimum/maximum or both
* open, left-open, right-open - has a minimum/maximum or neither
* synonymous - bounded, closed

terminology

* diameter - the absolute difference between both endpoints
* synonymous - diameter, length, width, size, measure
* center/midpoint (i.e. (a+b)/2) - radius (i.e. |a-b|/2)
* interior - the set of points that are no endpoints (an open interval)
* closure of I - the smallest closed interval that contains I

segment vs. interval

* partially used with the exact opposite meaning
* (1) interval (open, no endpoints) - segment (closed, with endpoints)
* (2) interval (closed) - segment (open)

context-related knowledge

In order to "know" what is in between both endpoints, there needs to
knowledge of the corresponding set of elements and the order of elements:

* `[c, f]` represents an interval of characters
* one needs to know that the set of elements is a known set of characters
* e.g. latin-1, utf-8, or even a custom mapping of symbols to code points
* `S := {a, z, x, f, h, i, ...}`
* one needs to know that the elements in `S` are ordered in some way
* e.g. alphabetically first-to-last, ordered in reverse, etc.
* note - the "order" is implied by the interval `[c,f]` => `(c <= f)`
* `A := { char | (a <= char) }, B := { char | (char <= b) }`
* `A := { c, d, e, f, ... }, B := { f, e, d, c, ... }`
* the set of elements of an interval is the intersection of both sets
* `I := [c, f] = (A & B) = { c, d, e, f }`

Because of that, an interval of indexes can be understood to define a substring
in the context of a known ordered set of elements. That is, if the borders are
understood to index the endpoints (e.g. `I:=[1,3]` defines substring `s:=[a,b,c]`
with regards to the above ordered set of lower-case letters).

multi-dimensional

Multi-dimensional intervals are subsets of `(I1 X I2 X ...X IN)`. These define
squares/rectangles for `(N=2)`, cubes for `(N=3)`, or in general N-dimensional
hypercubes.

<!-- ======================================================================= -->
## subsequence

In mathematics, sequence `t` is a subsequence of sequence `s`, if `t` was
derived from `s` by simply removing elements. That is, without changing the
order of these values.

Based on that definition alone, it can be stated that the empty sequence `[]`
is a subsequence to any sequence. That is, even though the empty sequence
has no clear offset within the initial sequence. And because `[]` has no effect
on the result of a concatenation, `[]` can be said to be an infix, prefix and
suffix to any non-empty sequence.

```
s = [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
t = [          3,    5, 6,         ]
u = [          3, 4, 5, 6,         ]
```

* `t` and `u` are both subsequences of `s`
* that is, even though `t` "has gaps"

With regards to `s`, the elements in `u` can be said to be consecutive,
contiguous, and/or strictly subsequent. In contrary to that, the elements
in `t` are said to be (merely) loosely subsequent.

**CLARIFICATION**
In the context of this discussion, a sequence `t` is said to be a subsequence
of sequence `s`, if `t` can be created from `s` by removing elements, and if
`t` is a sequence of consecutive elements.

Note that, in case of repetitions, it is possible to create the exact same
subsequence by removing different elements:

* `(s x t x u) := [a, b, c, b, e]`
* if subsequence `t` is assumed to be `[b]`, then
* `s` may be `[a]` or `[a,b,c]`

In cases where explicit clarity is needed, such a sequence may be referred
to as a "consecutive subsequence" or as a "subsequence of strictly subsequent
elements".

Note the following similarities with the set-based `subset-of` definition.

<!-- ======================================================================= -->
## subsequence-of

* `(s subsequence-of t)` := "s is a consecutive subsequence of t"

Note that, if `(s subsequence-of t)` is true,
then `s` may be referred to as "the subsequence"
and `t` as "the super-sequence".

Note that sequences have no operators like the ones defined for sets of
elements (e.g. union, intersection, etc).

clarification

* The empty sequence `[]` is a subsequence to any sequence.
* Any sequence, including `[]`, is a subsequence to itself.

clarification

* `(s subsequence-of t) -> (#s <= #t)`
* `subsequence-of` implies an order (<=)

<!-- ======================================================================= -->
## strict-subsequence-of

* `(i strict-subsequence-of t) := (i subsequence-of t) and (i != t)`
* some non-empty prefix `p` and/or suffix `s` exists such that `t = (p x i x s)`
* synonymous - proper-subsequence-of, true-subsequence-of

Note that, if `(s strict-subsequence-of t)` is true,
then `s` may be referred to as "the (strict) subsequence"
and `t` as "the (strict) super-sequence".

clarification

* The empty sequence `[]` is a strict subsequence to any non-empty sequence.
* No sequence, including `[]`, is a strict subsequence to itself.

clarification

* `(s strict-subsequence-of t) -> (#s < #t)`
* `strict-subsequence-of` implies an order (<)
