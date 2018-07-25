
<!-- ======================================================================= -->
# order - boundaries

<!-- ======================================================================= -->
## wikipedia, upper/lower set

* upper set (aka. upward closed, upset) a subset U of poset (X,<=)
* such that, if (x in U) and (x <= y), then (y in U)
* lower set (aka. downward closed, down set) a subset L of poset (X,<=)
* such that, if (x in L) and (y <= x), then (y in L)

remarks

* order ideal, ideal - sometimes synonymous to lower set
* every poset is an upper set to itself
* intersection/union of upper sets => upper set
* complement of upper set => lower set
* complement of lower set => upper set

<!-- ======================================================================= -->
## wikipedia, minimal/maximal elements

* minimal element - of subset S of poset (T,<=)
* (x in S) is minimal, if ((s <= x) => (x = s)) for all (s in S)
* i.e. not greater than another element
* maximal element - of subset S of poset (T,<=)
* (x in S) is maximal, if ((x <= s) => (x = s)) for all (s in S)
* i.e. not smaller than another element

remarks

* a set may have several minimal/maximal elements

<!-- ======================================================================= -->
## wikipedia, least/greatest elements

* least element - of subset S of poset (T,<=)
* (x in S) such that (x <= s) for all (s in S)
* i.e. smaller than every other
* greatest element - of subset S of poset (T,<=)
* (x in S) such that (x >= s) for all (s in S)
* i.e. greater than every other

remarks

* if they exist, then there is only one least/greatest
* greatest - an upper bound in S - necessarily unique
* there may be only one least/greatest element in S
* S has upper bounds =!> S has a greatest element
* S has lower bounds =!> S has a least element
* a finite chain always has a least and a greatest element
* if S has a greatest, then it has only one maximal (itself)

totally ordered sets

* minimum - minimal and/or least
* maximum - maximal and/or greatest
* absolute/local maximum/minimum
* absolute extrema - absolute maximum/minimum

least/greatest of the poset itself

* least - aka. bottom/zero/0
* greatest - aka. top/unit/1
* bounded poset - if T has both
* completeness property - T is bounded

<!-- ======================================================================= -->
## wikipedia, minimal/maximal vs. least/greatest

example

* S := {{d,o}, {d,o,g}, {d,o,g,a}, {o,a,f}}, ordered by containment
* {d,o} is minimal as it contains no set in the collection
* {g,o,a,d} is maximal as it is no subset to another set
* {o,a,f} is minimal and maximal
* S has no least/greatest element
* i.e. key is incomparable elements?

<!-- ======================================================================= -->
## wikipedia, lower/upper bounds

* a lower bound - of subset S of poset (K,<=)
* lower-bounds(S) := { (x in K) | (x <= s) for all (s in S) }
* an upper bound - of subset S of poset (K,<=)
* upper-bounds(S) := { (x in K) | (x >= s) for all (s in S) }

remarks

* note - lower/upper bounds do not have to exist
* note - lower/upper bounds not necessarily in S
* S is bounded from above - S has an upper bound
* S is bounded from below - S has a lower bound
* every finite subset of a non-empty totally ordered set has both

LB/UB generalized to functions

* given (g,f: D -> (K,<=))
* (y in K) is an upper bound of f(), if (y >= f(x)) for any (x in D)
* "sharp" upper bound, if (y = f(x)) for one or more (x in D)
* sharp - optimal, i.e. it cannot get more restrictive
* g() is an upper bound of f(), if (g(x) >= f(x)) for any (x in D)
* likewise, upper bound of a set of functions
* "lower bound" as a result of duality

tight bounds

* least upper bound, tight upper bound, supremum - no smaller upper bound
* greatest lower bound, tight lower bound, infimum - no greater lower bound

<!-- ======================================================================= -->
## wikipedia, infimum/supremum

infimum - of subset S of poset (T,<=)

* aka. inf, (pl) infima, greatest lower bound (GLB)
* greatest-of( lower-bounds(S) )

supremum - of subset S of poset (T,<=)

* aka. sup, (pl) suprema, least upper bound (LUB)
* least-of( upper-bounds(S) )

remarks

* infima/suprema not necessarily in S
* a set may have suprema/infima, but not necessarily a minimal/maximal elements
* if an infimum/supremum exists, then it is unqiue
* S has greatest element => S has supremum
* otherwise, sup does not exist or in (T\S)
* S has least element => S has infimum
* otherwise, inf does not exist or in (T\S)

**TODO** - canceled at some point
