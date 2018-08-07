
<!-- ======================================================================= -->
# Cartesian product

* short - "cart-prod"
* here, (×) represents the product operator
* synonymous operators - `X` (upper-case letter)

Note that the result of the Cartesian product is in general a set of sequences,
such that each sequence has length 2. That is independent of which input sets
are used. Consequently, the result of the Cartesian product is in principle
**a set of possibly nested sequences** (i.e. not a set of flat sequences).

Note that the Cartesian product is the default/standard formal basis used to
define types/domains. This however requires to extend the base definition of
the Cartesian product (see below).

<!-- ======================================================================= -->
## binary product

* `A × B = { (a,b) | (a in A), (b in B) }`
* note that - `#(A × B) == #A * #B`
* note that - `(#s == 2)` for any `s in (A × B)`
* i.e. regardless of the input sets `A` and `B`

Note that, if `A` and `B` are both sets of sequences, then any `s in (A × B)`
is a sequence of sequences (i.e. a nested sequence). That is, `(A × B)` is a
set of nested sequences such that each sequence has length `2`.

<!-- ======================================================================= -->
## non-commutative

```
1 - A := {1}, B := {2}
2 - (A × B) = { (1,2) }
3 - (B × A) = { (2,1) }
=> (A × B) <-!-> (B × A)
```

Note that the Cartesian product is not commutative;
i.e. the results of `(A × B)` and `(B × A)` are different.

<!-- ======================================================================= -->
## non-associative

```
1 - A := {1}
2 - A × (A × A) = { (1, (1,1)) }
3 - (A × A) × A = { ((1,1), 1) }
=> A × (A × A) <-!-> (A × A) × A
```

Note that the result of the Cartesian product is in general a set of nested
sequences of length 2. Because of that, the Cartesian product is not associative.

<!-- ======================================================================= -->
## multi cartesian-product

In general, and unless an implicit order of operation is assumed (e.g.
left-to-right), expressions such as `(A × B × C × ...)` are undefined.

The following definition therefore extends the above base definition such
that these expressions represent single operations (i.e. not a sequence of
operations).

n-ary Cartesian product (×Ai)

* `×Ai := (A1 × ... × AN) = {(a1,...,aN) | (ai in Ai)}` - for any set `Ai`
* `(#s == N)` for any `(s in ×Ai)`

Note that the result of the Cartesian product is now defined to be "flat".
However, if one or more `Ai` are sets of sequences, then `×Ai` will still
represent a set of nested sequences.

n-ary Cartesian power (×A^N)

* `×A^N := A × ... × A = {(a1,...,aN) | (ai in A)}` - for set `A`
* `×A^N := ×Ai` for `(Ai == A)` and `i in [1,N]`

Note that the result `S` of `×Ai` and `×A^N` is a set of possibly nested
sequences such that all sequences `(s in S)` have the exact same length.

variable Cartesian power (×A{a,b})

* see - regular expression like patterns
* (+) is the union operator for sets
* `×A{a,b}, ×A^{a,b} := (×A^a + ×A^(a+1) + ... + ×A^b)`
* `×A{1,4} = (×A^1 + ×A^2 + ×A^3 + ×A^4)`
* `×A{a} = ×A^{a,a} = ×A^a`
* `×A{+} = (×A^1 + ×A^2 + ...)`
* `×A{0} = {}`, `×A{*} = (×A{0} + ×A{+}) = ×A{+}`

Note that the result `S` of `×A{a,b}` is a set of possibly nested sequences
such that the lengths of all sequences `(s in S)` are variable within the
specified interval; i.e. `(#s in [a,b])`.
