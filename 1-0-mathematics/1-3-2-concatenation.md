
<!-- ======================================================================= -->
# Concatenation

* (×) represents the concatenation operator
* synonymous terms - add, append, concatenate
* synonymous operators - `x` (lower-case letter), `&`, `+`, etc.

Note that any sequence is in principle the result of concatenating its elements:
`s = [e1, ..., eN] := e1 × ... × eN`. That is, the result of the concatenation
operation is in general a flat sequence.

Note that in general sets will be homogenous sets-of-elements. That is, the
elements within a set are either all sequences, or the sets hold non-sequence
elements (i.e. values) only. Because of that, the concatenation operation
differs from the Cartesian product.

<!-- ======================================================================= -->
## cartesian product vs. concatenation

* (X) cartesian product <=!=> (x) concatenation
* `XVi <-> xVi`, if all `Vi` are sets of elements
* `XV^N <-> xV^N`, if `V` is a set of (atomic) elements
* `XV^{a,b} <-> xV{a,b}`, if `V` is a set of elements

If the concatenation is extended to operate on sets, the result will be a
single set of sequences. Depending on the input parameters, the resulting set
of sequences will be in general **a set of flat sequences** (i.e. no nesting).
That is in contrast to the base definition of the Cartesian product.

In contrary to the extended definition of the Cartesian product, there is no
general statement possible about the lengths of the sequences in the resulting
set-of-sequences. Likewise, the number of sequences in the resulting set can
in general not be determined.

However, such statements can still be made under certain circumstances: If no
input set is a set of sequences, then the length of each sequence within the
resulting set corresponds with the number of sets involved. In contrary to
that, the sequences in the resulting set of the Cartesian product always have
the exact same length.

<!-- ======================================================================= -->
## (v × w)

* combining (sets of) values with (sets of) values

`v × w := (v,w)`

* for two values `v` and `w`
* signature - (value, value) -> sequence
* note that - `(A × B) <-!-> (B × A)`

`v × W := { (v,w) | (w in W) }`

* for value `v` and set-of-values `W`
* signature - (value, set-of-values) -> set-of-sequences
* note that - `(#s == 2)` for any `s in (v × W)`
* note that - `#(v × W) == #W`

`V × W := { (v,w) | (v in V) and (w in W) }`

* for set-of-values `V` and set-of-values `W`
* signature - (set-of-values, set-of-values) -> set-of-sequences
* note that - `(#s == 2)` for any `s in (V × W)`
* note that - `#(V × W) == (#V * #W)`

similar definition(s) for

* `V × w := { (v,w) | (v in V) }`

<!-- ======================================================================= -->
## (s × v)

* combining (sets of) sequences with (sets of) values

`s × v := [s1,...,si,v]`

* for sequence `s`, `(#s = i)` and value `v`
* signature - (sequence, value) -> sequence
* note that - value `v` is added to the end of sequence `s`
* note that - `#(s × v) = (#s + 1)`

`v × s := [v,s1,...,si]`

* for sequence `s`, `(#s = i)` and value `v`
* signature - (value, sequence) -> sequence
* note that - value `v` is added to the beginning of sequence `s`
* note that - `#(v × s) = (1 + #s)`

`s × V := { (s × v) | for all (v in V) }`

* for sequence `s` and set-of-values `V`
* signature - (sequence, set-of-values) -> set-of-sequences
* note that - `(#t == (#s+1))` for any `t in (s × V)`
* note that - `#(s × V) == #V`

`S × v := { (s × v) | for all (s in S) }`

* for set-of-sequences `S` and value `v`
* signature - (set-of-sequences, value) -> set-of-sequences
* note that - `(s in S)` may have any length
* note that - `#(S × v) == #S`

`S × V := { (s × v) | for all (s in S) and all (v in V) }`

* for set-of-sequences `S` and set-of-values `V`
* signature - (set-of-sequences, set-of-values) -> set-of-sequences
* note that - `(s in S)` may have any length
* note that - `#(S × V) == (#S * #V)`

similar definition(s) for

* `V × s := { (v × s) | for all (v in V) }`
* `v × S := { (v × s) | for all (s in S) }`

<!-- ======================================================================= -->
## (s × t)

* combining (sets of) sequences with (sets of) sequences

`s × t := [s1,...,si,t1,...,tj]`

* for sequences `s` and `t`, `(#s = i)`, `(#t = j)` and `i,j in [0,*]`
* signature - (sequence, sequence) -> sequence
* note that - `#(s × t) = (#s + #t)`

`s × T := { (s × t) | for all (t in T) }`

* for sequence `s` and set-of-sequences `T`
* signature - (sequence, set-of-sequences) -> set-of-sequences
* note that - sequence `u in (S × T)` may have any length
* note that - `#(s × T) == #T`

`S × T := { (s × t) | for all (s in S) and all (t in T) }`

* for set-of-sequences `S` and set-of-sequences `T`
* signature - (set-of-sequences, set-of-sequences) -> set-of-sequences
* note that - sequence `u in (S × T)` may have any length
* note that - `#(S × T) <= (#S * #T)`

similar definition(s) for

* `S × t := { (s × t) | for all (s in S) }`

clarification

* `(s1 × t1) == (s2 × t2)` is possible
* if `(s1 prefi×-of s2)` and `(t2 suffi×-of t1)`
* e.g. `([1]×[2,3]) == ([1,2]×[3]) == [1,2,3]`

<!-- ======================================================================= -->
## summary

* `a×b×c = (a×b)×c = a×(b×c)` - one sequence only
* `a×b×C = (a×b)×C = a×(b×C)` - a set of sequences
* `a×B×C = (a×B)×C = a×(B×C)` - a set of sequences
* `A×b×C = (A×b)×C = A×(b×C)` - a set of sequences
* `A×B×C = (A×B)×C = A×(B×C)` - a set of sequences

Note that ...

* The concatenation is, like the Cartesian product, non-commutative.
* In contrary to that, the concatenation is associative.
* For sequences `a,b,c` and sets-of-sequences `A,B,C`,
  the result is in general a set of flat sequences.
* Sets-of-nested-sequences are still possible, if the input
  sets-of-sequences are themselves sets-of-nested-sequences.

<!-- ======================================================================= -->
## multi-concatenation

n-ary concatenation product (×Ai)

* `×A1 := A1` and `×AN := ×A(N-1) × AN`
* `×Ai <=> (A1 × A2 × ...)`

n-ary concatenation power (×A^N)

* `×A^1 := A` and `×A^N := ×A^(N-1) × A`
* `×A^N := ×Ai` for `(Ai == A)` and `i in [1,N]`
* `×A^N <=> (A × A × ...)`

variable concatenation power (×A{a,b})

* (/see/ "regular expression like patterns" /)
* (+) is the union operator for sets
* `×A{a,b}, ×A^{a,b} := (×A^a + ×A^(a+1) + ... + ×A^b)`
* `×A{1,4} = (×A^1 + ×A^2 + ×A^3 + ×A^4)`
* `×A{a} = ×A^{a,a} = ×A^a`
* `×A{+} = (×A^1 + ×A^2 + ...)`
* `×A{0} = {}`, `×A{*} = (×A{0} + ×A{+}) = ×A{+}`
