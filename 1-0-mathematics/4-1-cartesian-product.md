
<!-- ======================================================================= -->
# Cartesian product

* `X` represents the Cartesian product operator
* note the upper-case/capitalized letter 'X'

Note that the result of the Cartesian product is in general a set of sequences,
in which each sequence has length 2. That is independent of which input sets
were used. Consequently, the result of the Cartesian product is in principle
**a set of possibly nested sequences** (i.e. not a set of flat sequences).

Note that the Cartesian product is the default/standard formal basis used to
define types/domains. This however requires an extended definition (see below
- multi cartesian product).

<!-- ======================================================================= -->
## concatenation vs. cartesian product

* cartesian product <=!=> concatenation
* concatenation is associative, the cartesian product is not

Note that the result of a concatenation is
in principle always a set of flat sequences.

clarification

* `XV^N <-> xV^N`, if `V` is a set of values
* `XV^{a,b} <-> xV{a,b}`, if `V` is a set of values
* `XVi <-> xVi`, if all `Vi` are sets of values

<!-- ======================================================================= -->
## binary product

* `A X B = { (a,b) | a in A, b in B }`
* note that - `#(A X B) == #A * #B`
* note that - `(#s == 2)` for any `s in (A X B)`
* i.e. regardless of the input sets `A` and `B`

Note that, if `A` and `B` are both sets of sequences, then any `s in (A X B)`
is a sequence of sequences. That is, `(A X B)` is a set of sequences of
sequences in which each sequence has length `2`.

<!-- ======================================================================= -->
## non-associative

* `A := {1}`
* `A X (A X A) = { (1, (1,1)) }`
* `(A X A) X A = { ((1,1), 1) }`
* `A X (B X C) <-!-> (A X B) X C`

Note that the result of the Cartesian product is in general a set of nested
sequences. Because of that, the Cartesian product is not associative.

Note that, unless an implicit order of operation is assumed (e.g.
left-to-right), the result of `A X B X C X ...` is in general undefined.

<!-- ======================================================================= -->
## multi cartesian-product

Note that the definitions below extend the base definition. That is,
`A X B X C X ...` is defined not because an implicit order of operations is
selected, but because the definitions below define a single operation for
such "sequences".

n-ary cartesian product (XAi)

* `XAi := A1 X ... X AN = {(a1,...,aN) | (ai in Ai)}` - for any set `Ai`
* `XAi <=!=> (A1 X A2 X ...)`
* `(#s == N)` for any `s in XAi`

Note that the result of the Cartesian product is now defined to be "flat".
However, if one or more `Ai` is a set of sequences, then each sequence within
`XAi` will have a sequences as one or more of its elements (i.e. still nested).

n-ary cartesian power (XA^N)

* `XA^N := A X ... X A = {(a1,...,aN) : (ai in A)}` - for set `A`
* `XA^N := XAi` for `(Ai == A)` and `i in [1,N]`
* `XA^N <=!=> (A X A X ...)`

variable cartesian power (XA{a,b})

* see - regular expression like patterns
* (+) is the union operator for sets
* `XA{a,b}, XA^{a,b} := +(XA^i)` for `i in [a,b] in [1,*]`
* `XA{a,b} := (XA^a + XA^(a+1) + ... + XA^b)`
* `XA{1,4} = (XA^1 + XA^2 + XA^3 + XA^4)`
* `XA{a} = XA^{a,a} = XA^a`
* `XA{+} = (XA^1 + XA^2 + ...)`
