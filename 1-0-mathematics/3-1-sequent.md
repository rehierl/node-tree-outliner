
<!-- ======================================================================= -->
# Sequent

* two elements of the same sequence are **sequent**
* two elements of different sequences are **not sequent**
* not sequent <=!=> in-sequent

Note that, from now on, the terms "elements" and "values" are used synonymously:
e.g. the values of a sequence are sequent => they appear sequently.

Note that the notion of the term "consecutive" is the same as that of
"strictly presequent" or "strictly subsequent" (see below).

Note that confusion is inevitable,
if a sequence contains an element more than once.

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
//- the result is >0, if e1 comes before e2
//- the result is <0, if e1 comes after e2
//- the order is upside-down, if the result is <0
distanceBetween(e1,e2,seq) begin
  i1 = indexOf(e1,seq)
  i2 = indexOf(e2,seq)
  return (i2 - i1)
end

//- basic pattern of an extended definition
//- the below short definitions use the same pattern
//- the below definitions replace the name and operator
isPreSequentTo(e1,e2,seq) begin
  return (distanceBetween(e1,e2,seq) > 0)
end

//- pre-sequent (i1 < i2)
isPreSequentTo => (distanceBetween > 0)
isStrictlyPreSequentTo => (distanceBetween == +1)
isLooselyPreSequentTo => (distanceBetween > +1)

//- sub-sequent (i1 > i2)
isSubSequentTo => (distanceBetween < 0)
isStrictlySubSequentTo => (distanceBetween == -1)
isLooselySubSequentTo => (distanceBetween < -1)

//- in-sequent
isInSequentTo => (distanceBetween == 0)
```

<!-- ======================================================================= -->
## sequent

* `e1` and `e2` are elements of the same sequence

if the order of elements is not relevant in a given context:

* `absDistance(x,y) := abs(distanceBetween(x,y))`
* `(x insequent-to y) := (absDistance(x,y)) == 0)`
* `(x strictly-sequent-to y) := (absDistance(x,y) == 1)`
* `(x loosely-sequent-to y) := (absDistance(x,y) > 1)`

<!-- ======================================================================= -->
## pre-sequent (<, <<)

* `e1` appears before `e2`
* `e1` **precedes** `e2`

x is presequent to y (<)

* `(x < y)` := `x` and `y` are sequent, and `x` appears before `y`
* `s[i] is presequent to s[j]` for any `i,j in [1,#s]` and `(i < j)`

x is strictly presequent to y (<<)

* `(x << y)` := `x` is presequent to `y`, and `x` appears directly before `y`

x is loosely presequent to y

* `x` is presequent to `y`, but `x` is not strictly presequent to `y` -
* i.e. there are other entries in between

<!-- ======================================================================= -->
## sub-sequent (>, >>)

* `e2` appears after `e1`
* `e2` **succeeds** `e1`

y is subsequent to x (>)

* `(y > x)` := `x` and `y` are sequent, and `y` appears after `x`
* `s[i] is subsequent to s[j]` for any `i,j in [1,n]` and `(i > j)`

y is strictly subsequent to x (>>)

* `(y >> x)` := `y` is subsequent to `x`, and `y` appears directly after `x`

y is loosely subsequent to x

* `y` is subsequent to `x`, but `y` is not strictly subsequent to `x`
* i.e. there are other entries in between

<!-- ======================================================================= -->
## in-sequent (<>)

* randomly pick two elements `x,y in s=[e1,...,eN]`
* i.e. the number of unique/distinct elements in `s` is N

clarification

* if `(x != y)`, then `x` is either pre- or subsequent to `y`
* if `(x == y)`, then `x` is neither pre- nor subsequent to `y`

x insequent to y (<>)

* `x` and `y` are sequent, but neither pre- nor subsequent
* `(x <> y) <=> (y <> x)`

<!-- ======================================================================= -->
## examples

* presequent -> strictly or loosely presequent
* subsequent -> strictly or loosely subsequent
* insequent -> not presequent and not subsequent

assumed that `x` and `y` are sequent

* `not (x presequent-to y) <-> (x insequent-to y) or (x subsequent-to y)`
* `not (x subsequent-to y) <-> (x insequent-to y) or (x presequent-to y)`
* `not (x insequent-to y) <-> (x presequent-to y) or (x subsequent-to y)`
