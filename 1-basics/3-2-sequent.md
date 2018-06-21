
<!-- ======================================================================= -->
# Sequent

* two elements of the same sequence are said to be **sequent**
* any two elements appear **sequently** within the same sequence

clarification

* the elements of a sequence and the values they have are used synonymously
* i.e. the values of a sequence are sequent => they appear sequently
* confusion is inevitable, if a sequence is itself not unique -
  e.g. `s = (1, 2, 1, 3)`

<!-- ======================================================================= -->
## pseudocode definitions

```
indexOf(sequence,element) begin
  for i in 1 to sequence.length begin
    //- note: test for reference equality
    if(sequence(i) === element) return i
  end
  throw new ElementNotFoundException()
end

distanceBetween(seq,e1,e2) begin
  i1 = indexOf(seq,e1)
  i2 = indexOf(seq,e2)
  return (i2 - i1)
end

//- in short: (i1 < i2)
isPreSequentTo(seq,e1,e2) begin
  return (distanceBetween(seq,e1,e2) > 0)
end

//- pre-sequent
isPreSequentTo => (distanceBetween > 0)
isStrictlyPreSequentTo => (distanceBetween == +1)
isLooselyPreSequentTo => (distanceBetween > +1)

//- sub-sequent
isSubSequentTo => (distanceBetween < 0)
isStrictlySubSequentTo => (distanceBetween == -1)
isLooselySubSequentTo => (distanceBetween < -1)

//- in-sequent
isInSequentTo => (distanceBetween == 0)
```

<!-- ======================================================================= -->
## pre-sequent (<, <<)

* `e1` appears before `e2`
* `e1` **precedes** `e2`

x is presequent to y (<)

* `x < y` => `x` and `y` are sequent, and `x` appears before `y`
* `s(i) is presequent to s(j)` for any `i,j in [1,N]` and `(i < j)`

x is strictly presequent to y (<<)

* `x << y` => `x` is presequent to `y`, and `x` appears directly before `y`

x is loosely presequent to y

* `x` is presequent to `y`, but `x` is not strictly presequent to `y` -
* i.e. there are other entries in between

<!-- ======================================================================= -->
## sub-sequent (>, >>)

* `e2` appears after `e1`
* `e2` succeeds `e1`

y is subsequent to x (>)

* `y > x` => `x` and `y` are sequent, and `y` appears after `x`
* `s(i) is subsequent to s(j)` for any `i,j in [1,n]` and `(i > j)`

y is strictly subsequent to x (>>)

* `y >> x` => `y` is subsequent to `x`, and `y` appears directly after `x`

y is loosely subsequent to x

* `y` is subsequent to `x`, but `y` is not strictly subsequent to `x`
* i.e. there are other entries in between

<!-- ======================================================================= -->
## in-sequent (<>)

* randomly pick two values: `ei,ej in s=[e1,...,eN]`
* if `(ei !== ej)`: `ei` is either pre- or subsequent to `ej`
* if `(ei === ej)`: `ei` is neither pre- nor subsequent to `ej`

x insequent to y (<>)

* `x` and `y` are sequent, but neither pre- nor subsequent
* `(x <> y) <=> (y <> x)`

<!-- ======================================================================= -->
## sequent

* `e1` and `e2` are in the same sequence

if the order of elements is not relevant in a given context:

* x is insequent to y <=> `(absDistance(x,y)) == 0)`
* x is strictly sequent to y <=> `(absDistance(x,y) == 1)`
* x is loosely sequent to y <=> `(absDistance(x,y) > 1)`

clarification

* `abs()` returns the absolute value of a signed value
* `absDistance(x,y) := abs(distanceBetween(x,y))`

<!-- ======================================================================= -->
### examples

* presequent => strictly or loosely presequent
* subsequent => strictly or loosely subsequent
* insequent => not presequent and not subsequent

assumed that `x` and `y` are sequent

* `not (x presequent-to y) <=> (x insequent-to y) or (x subsequent-to y)`
* `not (x subsequent-to y) <=> (x insequent-to y) or (x presequent-to y)`
* `not (x insequent-to y) <=> (x presequent-to y) or (x subsequent-to y)`
