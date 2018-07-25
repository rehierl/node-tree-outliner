
<!-- ======================================================================= -->
# Cartesian product

* short - "cart-prod"
* `X` represents the Cartesian product operator
* note the upper-case/capitalized letter 'X'

Note that the result of the Cartesian product is in general a set of sequences,
such that each sequence has length 2. That is independent of which input sets
are used. Consequently, the result of the Cartesian product is in principle
**a set of possibly nested sequences** (i.e. not a set of flat sequences).

Note that the Cartesian product is the default/standard formal basis used to
define types/domains. This however requires to extend the base definition of
the Cartesian product (see below).

<!-- ======================================================================= -->
## binary product

* `A X B = { (a,b) | (a in A), (b in B) }`
* note that - `#(A X B) == #A * #B`
* note that - `(#s == 2)` for any `s in (A X B)`
* i.e. regardless of the input sets `A` and `B`

Note that, if `A` and `B` are both sets of sequences, then any `s in (A X B)`
is a sequence of sequences (i.e. a nested sequence). That is, `(A X B)` is a
set of nested sequences such that each sequence has length `2`.

<!-- ======================================================================= -->
## non-commutative

```
1 - A := {1}, B := {2}
2 - (A X B) = { (1,2) }
3 - (B X A) = { (2,1) }
=> (A X B) <-!-> (B X A)
```

Note that the Cartesian product is not commutative;
i.e. the results of `(A X B)` and `(B X A)` are different.

<!-- ======================================================================= -->
## non-associative

```
1 - A := {1}
2 - A X (A X A) = { (1, (1,1)) }
3 - (A X A) X A = { ((1,1), 1) }
=> A X (A X A) <-!-> (A X A) X A
```

Note that the result of the Cartesian product is in general a set of nested
sequences of length 2. Because of that, the Cartesian product is not associative.

<!-- ======================================================================= -->
## multi cartesian-product

In general, and unless an implicit order of operation is assumed (e.g.
left-to-right), expressions such as `(A X B X C X ...)` are undefined.

The following definition therefore extends the above base definition such
that these expressions represent single operations (i.e. not a sequence of
operations).

n-ary Cartesian product (XAi)

* `XAi := (A1 X ... X AN) = {(a1,...,aN) | (ai in Ai)}` - for any set `Ai`
* `(#s == N)` for any `(s in XAi)`

Note that the result of the Cartesian product is now defined to be "flat".
However, if one or more `Ai` are sets of sequences, then `XAi` will still
represent a set of nested sequences.

n-ary Cartesian power (XA^N)

* `XA^N := A X ... X A = {(a1,...,aN) | (ai in A)}` - for set `A`
* `XA^N := XAi` for `(Ai == A)` and `i in [1,N]`

Note that the result `S` of `XAi` and `XA^N` is a set of possibly nested
sequences such that all sequences `(s in S)` have the exact same length.

variable Cartesian power (XA{a,b})

* see - regular expression like patterns
* (+) is the union operator for sets
* `XA{a,b}, XA^{a,b} := (XA^a + XA^(a+1) + ... + XA^b)`
* `XA{1,4} = (XA^1 + XA^2 + XA^3 + XA^4)`
* `XA{a} = XA^{a,a} = XA^a`
* `XA{+} = (XA^1 + XA^2 + ...)`
* `XA{0} = {}`, `XA{*} = (XA{0} + XA{+}) = XA{+}`

Note that the result `S` of `XA{a,b}` is a set of possibly nested sequences
such that the lengths of all sequences `(s in S)` are variable within the
specified interval; i.e. `(#s in [a,b])`.
