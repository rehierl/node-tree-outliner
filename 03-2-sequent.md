
# Sequent

* Two elements of the same sequence are **sequent**.
* Any two elements appear **sequently** within the same sequence.

clarification

* the elements of a sequence and the values they have are used synonymously

<!-- ======================================================================= -->

<!-- ======================================================================= -->
## x-sequent

* `s=[e1,e2,...,eN]` represents a sequence of variables.

```
indexOf(sequence,entry) begin
  for i in 1 to sequence.length begin
    //- (===) checks for reference equality
    if(sequence(i) === entry) return i
  end
  throw new EntryNotFoundException()
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
isPreSequentTo := (distanceBetween > 0)
isStrictlyPreSequentTo := (distanceBetween == +1)
isLooselyPreSequentTo := (distanceBetween > +1)

//- sub-sequent
isSubSequentTo := (distanceBetween < 0)
isStrictlySubSequentTo := (distanceBetween == -1)
isLooselySubSequentTo := (distanceBetween < -1)

//- in-sequent
isInSequentTo := (distanceBetween == 0)
```

### pre-sequent (<,<<)

* `e1` appears before `e2`
* `e1` **precedes** `e2`
* `e1` is **presequent to** `e2`
* **presequent (<)** := `x` and `y` are sequent -
  and `x` appears before `y`
* **strictly presequent (<<)** := `x` is presequent to `y` -
  and `x` appears directly before `y`
* **loosely presequent** := `x` is presequent to `y` -
  but `x` is not strictly presequent to `y` -
  i.e. there are other entries in between
* `s(i) is presequent to s(j)` for any `i,j in [1,N]` and `(i < j)`

### sub-sequent (>,>>)

* `e2` appears after `e1`
* `e2` **succeeds** `e1`
* `e2` is **subsequent to** `e1`
* **subsequent (>)** := `x` and `y` are sequent -
  and `y` appears after `x`
* **strictly subsequent (>>)** := `y` is subsequent to `x` -
  and `y` appears directly after `x`
* **loosely subsequent** := `y` is subsequent to `x` -
  but `y` is not strictly subsequent to `x` -
  i.e. there are other entries in between
* `s(i) is subsequent to s(j)` for any `i,j in [1,n]` and `(i > j)`

### in-sequent (<>)

* A slot in a sequence can never hold more than one variable.
* There is a 1:1 relationship between the slots and its entries.
* Randomly pick two variables: `v1,v2 in s=[e1,...,eN]`
* If `(v1 !== v2)`: `v1` is either pre- or subsequent to `v2`.
* If `(v1 === v2)`: `v1` is neither pre- nor subsequent to `v2`.
* `e1` is **insequent to** `e1`
* **insequent (<>)** := `e1` and `e2` are sequent -
  but `e1` is neither pre- nor subsequent to `e2`.

But, two entities are not necessarily identical just because they are neither
pre- nor subsequent according to some order:

```
s=[e1,e2,...,eN]

(a < b) := (a.value < b.value)
(a > b) := (a.value > b.value)

for i in 1 to N begin
  s[i].value = (i Mod 2)
end
```

With such an order in mind, ...

* `e1` is not identical to `e3` just because `e1` is insequent to `e3`.
* The order is insufficient to infer reference equality.

### examples

* presequent => strictly or loosely presequent
* subsequent => strictly or loosely subsequent
* insequent => not presequent and not subsequent

Assumed that `x` and `y` are sequent, then ...

* `not (x presequent-to y) <=> (x insequent-to y) or (x subsequent-to y)`
* `not (x subsequent-to y) <=> (x insequent-to y) or (x presequent-to y)`
* `not (x insequent-to y) <=> (x presequent-to y) or (x subsequent-to y)`
* `(x insequent-to y) <=> (y insequent-to x)`
