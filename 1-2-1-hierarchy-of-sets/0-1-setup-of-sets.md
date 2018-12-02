
<!-- ======================================================================= -->
# Setup of sets

```
|-A---------------------| |-E-|
| |-B-----|   |-C-----| | | 7 |
| | 1   2 |   | 3     | | |---|
| | |-D-| |   | |-F-| | |
| | | 4 | | 5 | | 6 | | |
| | |---| |   | |---| | |
| |-------|   |-------| |
|-----------------------|
```

* Set A contains elements 1 to 6.
* Set B contains elements 1, 2 and 4.
* Set C contains elements 3 and 6.
* Set D only contains element 4.
* Set E only contains element 7.

Elements may belong to more than one set:

* Element 5 only belongs to set A.
* Elements 1 and 2 belong to sets A and B.
* Element 4 belongs to sets A, B and D.

Some of the relationships between those sets are:

* Set A contains set B.
* Set B is embedded into set A.
* Sets A and B both contain set D.
* Set D is embedded into sets A and B.
* Set B is disjoint from set C.

Note that the above example of nested sets would turn into a multiset of sets,
if element 3 would be removed from set C. That is because sets C and F would
then be distinct instances of sets that have identical content (i.e. equal sets).

<!-- ======================================================================= -->
## Simple setup (of sets)

**CLARIFICATION**
A set of sets is said to be **a (simple) setup (of sets)**,
if it does not contain the empty set `Ø` as an element.

* `S := (V,P)` is a setup of sets
* `P` is a set of sets of elements
* `V := E(P)` is the union of all sets in `P`

remarks

* Setup `S` is a two-element tuple of sets `V` and `P`
* No set `(s in P)` is allowed to be empty - i.e. `(Ø !in P)`
* `(P strict-subset-of P(V))` and `(0 <= #P < #P(V))`
* `(s subset-of V)` is true for any `(s in P)`

Note that `V` is empty if and only if `P` is empty. That is because even
though no `(p in P)` may be empty, `P` itself may still be empty.

* `(#P = 0) <-> (#V = 0)`
* `(#P > 0) <-> (#V > 0)`

Note that `V` may hold elements of any kind. That is, there is no requirement
of what kind of elements `V` must hold. That is, `V` may hold elements of one
kind (homogenous), or even elements of different kinds (heterogenous). Hence,
the elements in `V` may themselves even be sets of elements.

**Memory hook**
A (simple) setup is an arbitrary set of non-empty sets
that is accompanied by the union of all its sets.

<!-- ======================================================================= -->
## remarks

**CLARIFICATION**
Two distinct coupled sets in a setup are not necessarily related.

```
     \ set-2 |          |
set-1 \      | A        | B
------------------------------------------
 A           | C and R  | !C or (!R or R)
```

* `A` and `B` represent distinct non-empty sets - i.e. `(A != B)`
* two sets are coupled (`C`) ex-or disjoint (`!C`)
* two sets are related (`R`) ex-or unrelated (`!R`)

**CLARIFICATION**
In a setup, two disjoint sets are distinct.
However, two distinct sets are not necessarily disjoint.

* `disjoint <!=> distinct`
* (<!=) both sets may overlap each other
* (<!=) both sets may be strictly related

**CLARIFICATION**
In a setup, two disjoint sets are unrelated.
However, two unrelated sets are not necessarily disjoint.

* `disjoint <!=> unrelated`
* (<!=) both sets may overlap each other

**CLARIFICATION**
In a setup, two related sets are coupled with each other.
However, two coupled sets are not necessarily related.

* `coupled <=!> related`
* (=!>) both sets may overlap each other
* hint: `(a <-> b) <-> (!a <-> !b)`

<!-- ======================================================================= -->
## remarks

Note that the reason why `(!C or (!R or R))` feels odd is that two coupled sets
may or may not overlap each other. Hence, that expression needs to be read as
"if coupled, then either related or unrelated".

Note that the inclusion of the "overlaps" relationship makes it difficult to
classify the relationship between two sets. In addition to that, the definition
of "overlaps" (i.e. both sets have some elements in common and some elements
not in common) is not as abundantly clear as the definition of the "related-to"
relationship (i.e. without any exception, all the elements of one set are also
elements of the other set).

Note that the expression `(s in S)` is a syntactic simplification, which
needs to be understood as: "`s` is a set of elements, and as such an element
of the set of sets `P` of setup `S`". That is, a more accurate expression
would therefore be: `(s in P) and (P in S)`.

<!-- ======================================================================= -->
## Consistent setup (of sets)

**CLARIFICATION**
A set of sets `S` is said to be **a consistent setup (of sets)**,
if the following requirements are met:

1. `S := (V,P)` is a (simple) setup of sets
2. If two distinct sets in `P` are coupled, then both sets are related.

Note that requirement 2 will be referred to as "req-2" and
as "consistency in regards to the `subset-of` operator".

* `(s coupled-with t) -> (s related-to t)` is true if `(s != t)`
* Note that this expression is, due to req-2, required to be true.

Note that req-2 is needed to guarantee that a setup does not contain two
sets that overlap each other. That is, any two non-empty sets are required
to either be disjoint ex-or related with each other (see below).

**CLARIFICATION**
A setup counts as being consistent if `(#P <= 1)` is true.

* If `(#P == 0)`, then it does not contain two distinct sets
  which could be in conflict with req-2.
* If `(#P == 1)`, then it does not contain a 2nd distinct set
  which could cause a conflict with req-2.

**CLARIFICATION**
A consistent setup may contain sets that are disjoint to any other set in it.
That is, a setup is still consistent, even if the setup is equivalent to a set
of disjoint sets.

<!-- ======================================================================= -->
## (coupled <-> related)

**CLARIFICATION**
Any two sets in a consistent setup are related to each other, if they are
coupled with each other. Likewise, any two related sets in a consistent
setup are coupled with each other:

* `(s coupled-with t) <-> (s related-to t)` is true for any two `s,t in P`

That expression is true because ...

(1) `(s coupled-with t) <-> (s related-to t)` is true if `(s == t)` is true.
That is because, in the context of a setup, and by the definition of the
corresponding operators, that statement is true. That is because any non-empty
set is always coupled-with and related-to itself.

(2) `(s coupled-with t) -> (s related-to t)` is true if `(s != t)` is true.
That is because that expression is required to be true (see req-2).

In addition to that, and if two distinct sets are disjoint,
then both sets can not be related to each other.

(3) `(s coupled-with t) <- (s related-to t)` is true if `(s != t)` is true.
That is because two non-empty related sets are, by the definition of the
"related-to" operator, coupled with each other.

Note that two non-empty distinct and unrelated sets are not necessarily disjoint
(e.g. overlapping sets). However, the only requirement in an implication (i.e.
`(a -> b) := (!a or b)`) is, that `b` must be true if `a` is true. In contrary
to that, `b` may have any value if `a` is false. Consequently, the above
implication (3) is, by the definition of the "related-to" operator, satisfied.

(4) `(s coupled-with t) <-> (s related-to t)` is true if `(s != t)` is true.
That is because `((a -> b) and (a <- b)) <-> (a <-> b)` (i.e. 2+3).

(5) `(s coupled-with t) <-> (s related-to t)` is true for any two `s,t in P`.
That is because that expression is true regardless of whether both non-empty
sets are equal or not (i.e. 1+4).

Note that this proof is largely independent of the actual elements the above
operators are defined for. That is, the above expression is applicable, even
if the operators involved are defined for different elements, but in an
equivalent fashion.

<!-- ======================================================================= -->
## (disjoint ex-or related)

**CLARIFICATION**
Any two sets in a consistent setup are either disjoint,
ex-or one set is a subset of the other.

* `(s disjoint-to t) ex-or (s related-to t)` is true for any two `s,t in P`

That expression is true since it results from basic transformations:

(1) `(s coupled-with t) <-> (s related-to t)` is true for any two `s,t in P`.
That is because this expression is a consequence of req-2.

(2) `not (s disjoint-to t) <-> (s related-to t)` is true for any two `s,t in P`.
A valid transformation since `(s coupled-with t) <-> not (s disjoint-to t)`.

(3) `(s disjoint-to t) ex-or (s related-to t)` is true for any two `s,t in P`.
A valid transformation since `(!a <-> b) <-> (a ex-or b)`.

Note that this proof is largely independent of the actual elements the above
operators are defined for. That is, the above expression is applicable, even
if the operators involved are defined for different elements, but in an
equivalent fashion.

<!-- ======================================================================= -->
## (coupled <-> strictly related), if distinct

**CLARIFICATION**
Any two distinct coupled sets in a consistent setup are strictly related.
Likewise, any two strictly related sets in a consistent setup are coupled
with each other:

* `(s coupled-with t) <-> (s strictly-related-to t)` is true if `(s != t)`

That expression is true, because ...

(1) `(s coupled-with t) <-> (s related-to t)` is true if `(s != t)`.
That is because this expression is a consequence of req-2.

(2) `(s related-to t) -> (s strictly-related-to t)` is true if `(s != t)`.
That is because two distinct and related sets are always strictly related.
That is a consequence of the "strictly-related-to" operator.

(3) `(s coupled-with t) -> (s strictly-related-to t)` is true if `(s != t)`.
That is due to the transitivity of (->), in combination with (1).

(4) `(s related-to t) <- (s strictly-related-to t)` is true if `(s != t)`.
That is due to the definition of the "strictly-related-to" operator.

(5) `(s coupled-with t) <- (s strictly-related to t)` is true if `(s != t)`.
That is due to the transitivity of (->), in combination with (1).

(6) `(s coupled-with t) <-> (s strictly-related to t)` is true if `(s != t)`.
That is because `((a -> b) and (a <- b)) <-> (a <-> b)` (i.e. 3+5).

Note that `(s related-to t) <-> (s strictly-related-to)` is true if `(s != t)`.
That is due to (2) and (4). In combination with (1), that expression allows
an alternative proof.

Note that this proof is largely independent of the actual elements the above
operators are defined for. That is, the above expression is applicable, even
if the operators involved are defined for different elements, but in an
equivalent fashion.

Note that the above expression is obviously not true, if `(s == t)`.
That is because no non-empty set is strictly related to itself.

Note that a consistent setup is consequently also
"consistent in regards to the strict-subset-of operator".

<!-- ======================================================================= -->
## (disjoint ex-or strictly related), if distinct

**CLARIFICATION**
Two distinct sets in a consistent setup are either disjoint,
ex-or one set is a strict subset of the other.

* `(s disjoint-to t) ex-or (s strictly-related-to t)` is true if `(s != t)`

That expression is true since it results from basic transformations:

(1) `(s coupled-with t) <-> (s related-to t)` is true for any two `s,t in P`.
That is because this expression is a consequence of req-2.

(2) `(s coupled-with t) <-> (s strictly-related-to t)` is true if `(s != t)`.
That is because if two distinct sets are related, then one set is, by the
definition of the "strict-subset-of" operator, a strict subset of the other.

(3) `not (s disjoint-to t) <-> (s strictly-related-to t)` is true if `(s != t)`.
A valid transformation since `(s coupled-with t) <-> not (s disjoint-to t)`.

(4) `(s disjoint-to t) ex-or (s strictly-related-to t)` is true if `(s != t)`.
A valid transformation since `(!a <-> b) <-> (a ex-or b)`.

Note that this proof is largely independent of the actual elements the above
operators are defined for. That is, the above expression is applicable, even
if the operators involved are defined for different elements, but in an
equivalent fashion.

<!-- ======================================================================= -->
## Strict setup (of sets)

**CLARIFICATION**
A setup is said to be **a (strict/proper) setup (of sets)**,
if the following requirements are met:

1. `S := (V,P)` is a consistent setup.

Note that a consistent setup is therefore synonymous to a strict setup.
That is, there are no additional requirements that need to be satisfied.

This definition therefore stresses the consequences of req-2:

* Any two sets are (disjoint ex-or related).
* `(s disjoint-to t) ex-or (s related-to t)`, for any two `s,t in P`
* Any two distinct sets are (disjoint ex-or strictly related).
* `(s disjoint-to t) ex-or (s strictly-related-to t)`, if `(s != t)`

Also note that, in the context of a strict setup, the following "statements"
in regards to any two sets in P are true:

* disjoint <!=> distinct
* disjoint <=> unrelated
* coupled <=> (strictly) related

<!-- ======================================================================= -->
## remarks

Note that, for any two distinct coupled sets in a strict setup, it can be
stated that one set is located inside ex-or outside of the other. Consequently,
two such sets in a strict setup are distinctively ordered. That is, one set is
super-or sub-ordinate to the other (aka. more or less significant than).
