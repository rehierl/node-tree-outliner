
<!-- ======================================================================= -->
# Interval

* intervals allow to focus on natural numbers rather than arbitrary posets
* intervals are by definition continuous sets/intervals
* they allow to ignore non-continuous sets (i.e. gaps)
* what about sub-intervals of equal/incomparable elements
* hierarchy of nested intervals - somehow redundant
* stresses the (disjoint ex-or strictly-related) aspect
* => hierarchy of nested sets
* treat like (nested) sets

<!-- ======================================================================= -->
## Intervals

In order to "know" what is in between both endpoints, there needs to be
knowledge of the corresponding set of elements and the order of elements:

* `[c, f]` represents an interval of characters
* one needs to know that the set of elements is a known set of characters
* e.g. latin-1, utf-8, or some other mapping of symbols to code points
* `S := {a, z, x, f, h, i, ...}`
* one needs to know that the elements in `S` are ordered in some way
* e.g. alphabetically first-to-last, ordered in reverse, etc.
* note - the "set and order" are implied by the notation `[c,f]` => `(c <= f)`
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

Note that this perspective requires total, order-isomorphic orders.
That is the underlying bijection must be known and order-preserving.

<!-- ======================================================================= -->
## wikipedia, partial orders, interval

* `[a,b]` for `(a <= b)` is the set of elements `x` such that `(a <= x <= b)`
* `[a,b]` for integers `(a < b)` may be empty - e.g. `(b = a+1)`
* i.e. `[a,b] = ([a,*] & [*,b])`

<!-- ======================================================================= -->
## wikipedia, interval order

* `(xi < xj)` for intervals `xi -> (Li,Ri)` if `(Ri < Lj)`
* TODO - how does that order behave with regards to overlapping - incomparable?
* TODO - try different orders e.g. `(Li < Lj)`
* TODO - is one of those orders similar to the enter-/exit-order?

<!-- ======================================================================= -->
## wikipedia, intervals

* intervals of totally ordered sets
* an interval is a set of numbers, such that ...
* any number in between its endpoints is included
* intervals are integral to interval arithmetic

terminology

* `a,b` are referred to as "limit/end-points"
* degenerate - zero/one-element interval
* proper - two or more elements
* left/right-bounded - the left/right limit point is included
* bounded - both limit points are included
* unbounded - at most one limit point is included
* half-bounded - only one limit point is included
* finite/infinite interval - finite if bounded
* diameter - the absolute difference between both endpoints
* synonymous - diameter, length, width, measure, size
* bounded - diameter is finite
* center/midpoint - (a+b)/2
* radius - |a-b|/2
* left/right-open, open - has no min/max or both
* left/right-closed, closed - has min/max or both
* synonymous - bounded, closed
* interior - largest inner open interval
* i.e. the set of points that are no endpoints
* closure - smallest outer closed interval
* interval enclosure/span - smallest interval that contains I

segment vs. interval

* different sources use these terms with the exact opposite meaning
* (1) interval (open, no endpoints) - segment (closed, with endpoints)
* (2) interval (closed) - segment (open)
* increasing use of "interval with qualification"
* in general, i prefer (1) as i read "segment" to refer to an inner part

notational

* `[a,b) = [a,b[`
* `(a,a) = {}` - empty set/interval
* `[a,a] = {a}` - degenerated interval
* `[-Inf,b], (-Inf,b]` - both are distinct
* `(-Inf,b] = [*,b]` - in this discussion

properties

* an intersection of intervals is itself an interval
* in general, the union of intervals is a set of intervals
* any element in an interval defines a partition of intervals
* i.e. an interval version of the trichotomy principle

multi-dimensional

* n-dimensional interval - subset of xIn
* thought to define regions bounded by squares/rectangles
* in general n-dimensional hyper-cubes/rectangles
* facet - replace each non-degenerate Ik by a degenerate Ik (an endpoint)
* faces - I itself and all faces of its facets
* corners - the faces that consist of a single point of xIn
