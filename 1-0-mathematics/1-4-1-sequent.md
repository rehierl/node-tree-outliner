
<!-- ======================================================================= -->
# Sequent

* two elements of the same sequence are **sequent**
* two elements of different sequences are **not sequent**
* not sequent <=!=> in-sequent

Note that, from now on, the terms "elements" and "values" are in general used
synonymously: e.g. the values of a sequence are sequent, i.e. they appear
sequently within a sequence.

Note that confusion is inevitable,
if a sequence contains one or more elements more than once.

Note that the notion of the term "consecutive" is the same as that of
"strictly presequent" or "strictly subsequent" (see below).

<!-- ======================================================================= -->
## covered-by

* `(a covered-by b)`, if `(a strictly-sequent-to b)`
* see "partial order" in "order theory"

<!-- ======================================================================= -->
## pseudocode definitions

Note that the naming convention is such that the name of a binary operation
refers to the 1st parameter, which will be tested against the 2nd parameter
(i.e. the context of the corresponding operation).

```
indexOf(element, sequence) begin
  for i in 1 to sequence.length begin
    if(sequence[i] === element) return i
  end
  throw new ElementNotFoundException()
end

//- returns an (pos|neg) integer value
//- the result is >0, if e1 appears before e2
//- the result is <0, if e1 appears after e2
//- the order is upside-down, if the result is <0
distanceBetween(e1,e2,seq) begin
  i1 = indexOf(e1,seq)
  i2 = indexOf(e2,seq)
  return (i2 - i1)
end

//- returns a positive integer value in [0,*]
//- the number of jumps required to reach e2 from e1
//- the result is =0, if (e1 == e2)
//- the result is +1, if e1 is adjacent to e2
//- the result is +2, if one ei is located between e1 and e2
absDistance(e1,e2,seq) begin
  result = distanceBetween(e1,e2,seq)
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
## sequent

* `e1` and `e2` are sequent, if they are elements of the same sequence `s`

if the order of elements is not relevant in a given context:

* `(x sequent-to y) := (absDistance(x,y) >= 0)`
* `(x insequent-to y) := (absDistance(x,y) == 0)`
* `(x strictly-sequent-to y) := (absDistance(x,y) == 1)`
* `(x loosely-sequent-to y) := (absDistance(x,y) > 1)`

<!-- ======================================================================= -->
## pre-sequent (<, <<)

* `e1` appears before `e2`
* `e1` **precedes** `e2`

x is presequent to y (<)

* `(x < y)` := `x` and `y` are sequent, and `x` appears before `y`
* `(s[i] presequent-to s[j])` for any `i,j in [1,#s]` and `(i < j)`

x is strictly presequent to y (<<)

* `(x << y)` := `x` is presequent to `y`, and `x` appears directly before `y`
* `(s[i] strictly-presequent-to s[j])` if `(i == (j-1))`

x is loosely presequent to y

* `x` is presequent to `y`, but `x` is not strictly presequent to `y` -
* `(s[i] loosely-presequent-to s[j])` if `(i < (j-1))`
* i.e. there are other entries in between

<!-- ======================================================================= -->
## sub-sequent (>, >>)

* `e2` appears after `e1`
* `e2` **succeeds** `e1`

y is subsequent to x (>)

* `(y > x)` := `x` and `y` are sequent, and `y` appears after `x`
* `(s[i] subsequent-to s[j])` for any `i,j in [1,#s]` and `(i > j)`

y is strictly subsequent to x (>>)

* `(y >> x)` := `y` is subsequent to `x`, and `y` appears directly after `x`
* `(s[i] strictly-subsequent-to s[j])` if `(i == (j+1))`

y is loosely subsequent to x

* `y` is subsequent to `x`, but `y` is not strictly subsequent to `x`
* `(s[i] loosely-subsequent-to s[j])` if `(i > (j+1))`
* i.e. there are other entries in between

<!-- ======================================================================= -->
## in-sequent (<>)

* randomly pick two elements `x,y in s=[e1,...,eN]`, where `(N = #s)`
* note - the focus is on elements, not values

clarification

* if `(x != y)`, then `x` is either pre- or subsequent to `y`
* if `(x == y)`, then `x` is neither pre- nor subsequent to `y`

x insequent to y (<>)

* `x` and `y` are sequent, but neither pre- nor subsequent
* i.e. in-sequent <=!=> not sequent
* `(x <> y) <-> (y <> x)`

<!-- ======================================================================= -->
## examples

* presequent -> strictly or loosely presequent
* subsequent -> strictly or loosely subsequent
* insequent -> not presequent and not subsequent

assumed that `x` and `y` are sequent

* `not (x presequent-to y) <-> (x insequent-to y) or (x subsequent-to y)`
* `not (x subsequent-to y) <-> (x insequent-to y) or (x presequent-to y)`
* `not (x insequent-to y) <-> (x presequent-to y) or (x subsequent-to y)`
