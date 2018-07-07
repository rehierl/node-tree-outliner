
<!-- ======================================================================= -->
# Interval

* an interval is a set of numbers, such that ...
* any number in between its endpoints is included

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

* different sources use these terms with the exact opposite meaning
* (1) interval (open, no endpoints) - segment (closed, with endpoints)
* (2) interval (closed) - segment (open)
* in general, i prefer (1) as i read "segment" as being an inner part

<!-- ======================================================================= -->
## context-related knowledge

In order to "know" what is in between both endpoints, there needs to be
knowledge of the corresponding set of elements and the order of elements:

* `[c, f]` represents an interval of characters
* one needs to know that the set of elements is a known set of characters
* e.g. latin-1, utf-8, or some other mapping of symbols to code points
* `S := {a, z, x, f, h, i, ...}`
* one needs to know that the elements in `S` are ordered in some way
* e.g. alphabetically first-to-last, ordered in reverse, etc.
* note - the "order" is implied by the interval `[c,f]` => `(c <= f)`
* `A := { char | (a <= char) }, B := { char | (char <= b) }`
* `A := { c, d, e, f, ... }, B := { f, e, d, c, ... }`
* the set of elements of an interval is the intersection of both sets
* `I := [c, f] = (A & B) = { c, d, e, f }`

Because of that, an interval of indexes can be understood to define a substring
in the context of a linear sequence. That is, if the borders are understood to
index the endpoints (e.g. `I:=[1,3]` defines substring `s:=[a,b,c]` in the
context of the above ordered set of lower-case letters).

Note that an interval represents a unique linear sequence.
That is, any interval represents an ordered set of values.

<!-- ======================================================================= -->
## multi-dimensional

Multi-dimensional intervals are subsets of `(I1 X I2 X ...X IN)`. These define
squares/rectangles for `(N=2)`, cubes for `(N=3)`, or in general N-dimensional
hypercubes.
