
<!-- ======================================================================= -->
# pre-/in-/sub-sequent

* two components of the same sequence are **sequent**
* two components of different sequences are **not sequent**
* not sequent <=!=> in-sequent

Note that the terms "components" and "elements" are in general used without
further distinction: e.g. the elements of a sequence are sequent, i.e. they
appear sequently within a sequence. However, conflicts are inevitable, if a
sequence contains an element more than once.

* e.g. is `1` in `[1,2,1]` presequent to `2`? .. Yes and no.

<!-- ======================================================================= -->
## pseudocode definitions

Note that the naming convention is such that the name of a binary operation
refers to the 1st parameter, which will be tested against the 2nd parameter
(i.e. the context of the corresponding operation).

```
//- return the index of a component in the given sequence
indexOf(sequence, component) begin
  index = 1
  for c in sequence begin
    if(c === component) return index
    index = index + 1
  end
  throw new NotFoundException()
end

//- abbreviation
i(s,c) or idx(s,c) => indexOf(s,c)

//- returns an (pos|neg) integer value
//- the result is >0, if c1 appears before c2
//- the result is <0, if c1 appears after c2
//- the order is upside-down, if the result is <0
distanceBetween(s,c1,c2) begin
  return (idx(s,c2) - idx(s,c1))
end

//- abbreviation
d(s,c1,c2) => distanceBetween(s,c1,c2)

//- returns a positive integer value in [0,*]
//- the number of jumps required to reach c2 from c1
//- the result is =0, if (c1 == c2)
//- the result is +1, if c1 is adjacent to c2
//- the result is +2, if one ci is located between c1 and c2
absDistance(seq,c1,c2) begin
  result = distanceBetween(seq,c1,c2)
  return (result >= 0) ? result : (-1)*result
end

//- pre-sequent (i1 < i2)
isPreSequentTo => (distanceBetween > 0)
isStrictlyPreSequentTo => (distanceBetween == +1)
isLooselyPreSequentTo => (distanceBetween > +1)

//- sub-sequent (i1 > i2)
isSubSequentTo => (distanceBetween < 0)
isStrictlySubSequentTo => (distanceBetween == -1)
isLooselySubSequentTo => (distanceBetween < -1)

//- in-sequent (i1 == i2)
isInSequentTo => (distanceBetween == 0)
```

<!-- ======================================================================= -->
## covered-by

* `(a covered-by b)`, if `(a strictly-sequent-to b)`
* see "partial order" in "order theory"

Note that the notion of the terms "consecutive" and "covering" is similar to
strictly-sequent, strictly-presequent and strictly-subsequent (see below).

<!-- ======================================================================= -->
## sequent

* components `x` and `y` are sequent, ...
* if they are components of the same sequence `s`

if the order of components is not relevant in a given context:

* `(x sequent-to y) := (absDistance(x,y) >= 0)`
* `(x insequent-to y) := (absDistance(x,y) == 0)`
* `(x strictly-sequent-to y) := (absDistance(x,y) == 1)`
* `(x loosely-sequent-to y) := (absDistance(x,y) > 1)`

<!-- ======================================================================= -->
## pre-sequent (<, <<)

* component `x` appears before `y`
* `x` **precedes** `y`

x is **presequent-to** y (<)

* `(x < y)` := `x` and `y` are sequent, and `x` appears before `y`
* `(s[i] presequent-to s[j])` for any `i,j in [1,#s]` and `(i < j)`

x is **strictly-presequent-to** y (<<)

* `(x << y)` := `x` is presequent-to `y`, and `x` appears directly before `y`
* `(s[i] strictly-presequent-to s[j])` if `(i == (j-1))`

x is **loosely-presequent-to** y

* `x` is presequent-to `y`, but `x` is not strictly presequent-to `y` -
* `(s[i] loosely-presequent-to s[j])` if `(i < (j-1))`
* i.e. there are other entries in between

<!-- ======================================================================= -->
## sub-sequent (>, >>)

* component `y` appears after `x`
* `y` **succeeds** `x`

y is **subsequent-to** x (>)

* `(y > x)` := `x` and `y` are sequent, and `y` appears after `x`
* `(s[i] subsequent-to s[j])` for any `i,j in [1,#s]` and `(i > j)`

y is **strictly-subsequent-to** x (>>)

* `(y >> x)` := `y` is subsequent-to `x`, and `y` appears directly after `x`
* `(s[i] strictly-subsequent-to s[j])` if `(i == (j+1))`

y is **loosely-subsequent-to** x

* `y` is subsequent-to `x`, but `y` is not strictly subsequent-to `x`
* `(s[i] loosely-subsequent-to s[j])` if `(i > (j+1))`
* i.e. there are other entries in between

<!-- ======================================================================= -->
## in-sequent (<>)

* randomly pick two components `x,y in s=[c1,...,cN]`, where `(N = #s)`

clarification

* if `(x != y)`, then `x` is either pre- or subsequent-to `y`
* if `(x == y)`, then `x` is neither pre- nor subsequent-to `y`

x **insequent-to** y (<>)

* `x` and `y` are sequent, but neither pre- nor subsequent
* i.e. in-sequent <=!=> not sequent
* `(x <> y) <-> (y <> x)`

<!-- ======================================================================= -->
## examples

* presequent -> strictly- or loosely-presequent
* subsequent -> strictly- or loosely-subsequent
* insequent -> not presequent and not subsequent

assumed that `x` and `y` are sequent

* `not (x presequent-to y) <-> (x insequent-to y) or (x subsequent-to y)`
* `not (x subsequent-to y) <-> (x insequent-to y) or (x presequent-to y)`
* `not (x insequent-to y) <-> (x presequent-to y) or (x subsequent-to y)`
