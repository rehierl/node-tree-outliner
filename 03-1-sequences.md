
# Sequences

* `s` represents a sequence of elements.
* `s = [si] = [e1,e2,...,eN] = [e(1),...,e(N)]` for `N in [0,+Inf)`
* or alternatively `s = (si) = (e1,e2,...,eN)`
* Two elements of the same sequence are **sequent**.
* Any two elements appear **sequently** within the same sequence.

Any element `e(i)` may belong to a different domain `E(i)`

* `e(i) not in E(j)` may be true
* `e(i)` is not necessarily in the same domain as `e(j)`

The **length of** a sequence `s`

* `#s := #(s) := lengthOf(s) := s.length := N`
* `#s length-of s` is always true

Sequence `s` is **empty**

* `is-empty s` (alt. `isEmpty(s)`) is true, if `(#s = 0)`
* `is-empty () := is-empty [] = true`

The **n-th entry of** sequence `s`

* `s(i) = s[i] = ei` for `i in [1,#s]`
* synonymous - entry, element, item
* `s(i) = undefined`, if `(#s = 0)`

The **reversed** sequence `s'` of sequence `s`

* `s' = (eN,...,e1)`, if `s = (e1,...,eN)`
* `s` and `s'` are palindromic sequences, if `(s = s')`

<!-- ======================================================================= -->
## equality, inequality

Two sequences `s` and `t` are **equal by value (==)**

* `(s == t)`, if `(#s = #t)` and `(s(i) = t(i))` for any `i in [1,#s]`
* synonymous - `(s == t)`, `(s = t)`, `(s equal-to t)`
* In general, the test for equality by value must take the type of both
  elements into account (e.g. `(+2 != +2.0)`): `(s == t)`, if `(#s = #t)`
  and `(typeOf(s(i)) = typeOf(t(i)))` and `(s(i) = t(i))`

Two sequences `s` and `t` are **unequal by value (!=)**

* `(s != t)`, if `not (s equal-to t)`
* synonymous - `(s != t)`, `(s unequal-to t)`
* They differ in length and/or in some corresponding entries.

Two sequences `s` and `t` are **equal by reference (===)**

* `(s === t)`, if `(addressOf(s) == addressOf(t))`
* synonymous - `(s === t)`, `(s identical-to t)`
* `(s === t) => (s == t)` - but not `<=`

Two sequences `s` and `t` are **unequal by reference (!==)**

* `(s !== t)`, if `(addressOf(s) != addressOf(t))`
* synonymous - `(s !== t)`, `(s different-to t)`
* `(s != t) => (s !== t)` - but not `<=`
* Different references are needed to store different values.
* A single reference can not store two different values at the same time.
* Different references may still represent equal values.

Equality/inequality default to equal/unequal by value.

* equal => equal by value, but not necessarily equal by reference
* unequal => unequal by value and also unequal by reference

<!-- ======================================================================= -->
## infix, subsequence

* (left-bound, offset-based notation)
  `t = [e(l),e(l+1),...,e(l+k-1)]`
  for some `l in [1,N]` and `k in [1,(N-l)]` -
  `l` is the left border,  offset `o = l` (letter).
* (right-bound notation)
  `t = [e(r-k+1),...,e(r-k+i),...,e(r)]`
  for some `r in [1,N]`, `k in [1,r]` and `i in [1,k]` -
  `r` is the right border.
* `left-bound <=> right-bound`

Sequence `t` is a **subsequence of** sequence `s`:

* `t subsequence-of s`, if `(s(o+j) = t(j))`
  for `o in [1,N]`, `k in [1,(N-o)]` and `j in [1,k]`.
* `(t = s)`, if `t subsequence-of s` and `(#t = #s)`
* A sequence is a subsequence to itself.
* `(s = s)` and `s subsequence-of s` are both always true.
* An empty sequence has no subsequence.

<!-- ======================================================================= -->
## prefix

Sequence `t` is **a prefix of** sequence `s`

* `t prefix-of s`, if `t subsequence-of s`
  and offset `(o = 1)` (digit)
* `t` is bound to the 1st entry of `s`
* `s prefix-of s` is always true.
* A sequence is a prefix to itself.

Sequence `t` is **the n-th prefix of** sequence `s`

* `t n-prefix-of s`, if `t prefix-of s` and `(#t = k = n)`
* `prefix(s,n) = t`, if `(t n-prefix-of s)`
* The N-th prefix of a sequence is the sequence itself.

Sequence `u` is **a common prefix of** sequence `s` and sequence `t`

* `u prefix-of s,t`, if `(u prefix-of s)` and `(u prefix-of t)`
* `s` and `t` share the common prefix `u`
* `#u in [1,min(#s,#t)]`
* For any common prefix `u`, there is a `n` such that `u n-prefix-of s,t`

Sequence `u` is **the n-th common prefix of** sequences `s` and `t`

* `u n-prefix-of s,t`, if `(u prefix-of s,t)` and `(#u = n)`
* `n in [1,min(#s,#t)]`

Sequence `u` is **the common prefix of** sequence `s` and sequence `t`

* If there is no other common suffix `v` such that `(#v > #u)`
* `u max-prefix-of s,t`

<!-- ======================================================================= -->
## suffix

Sequence `t` is **a suffix of** sequence `s`

* `t suffix-of s`, if `t subsequence-of s` and `(r = N)`
* `t` is bound to the last entry of `s`
* `t` and `s` have the same order (i.e. `t` is not reversed)
* `s suffix-of s` is always true
* Any sequence is a suffix to itself.

Sequence `t` is **the n-th suffix of** sequence `s`

* `t n-suffix-of s`, if `t suffix-of s` and `(#t = k = n)`
* `suffix(s,n) = t`, if `(t n-suffix-of s)`
* The N-th suffix of a sequence is the sequence itself.

Sequence `u` is **a common suffix of** sequence `s` and sequence `t`

* `u suffix-of s,t`, if `(u suffix-of s)` and `(u suffix-of t)`
* `s` and `t` share the common suffix `u`
* `#u in [1,min(#s,#t)]`
* For any common suffix `u`, there is a `n` such that `u n-suffix-of s,t`

Sequence `u` is **the n-th common suffix of** sequences `s` and `t`

* `u n-suffix-of s,t`, if `(u suffix-of s,t)` and `(#u = n)`
* `n in [1,min(#s,#t)]`

Sequence `u` is **the common suffix of** sequence `s` and sequence `t`

* If there is no other common suffix `v` such that `(#v > #u)`
* `u max-suffix-of s,t`

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
