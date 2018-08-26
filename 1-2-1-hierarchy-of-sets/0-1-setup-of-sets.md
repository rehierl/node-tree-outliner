
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
if number 3 would be removed from set C. That is because sets C and F would
then be distinct sets that hold identical content (i.e. distinct objects that
represent the same set).

<!-- ======================================================================= -->
## Simple setup (of sets)

**CLARIFICATION**
A set of sets is said to be **a (simple) setup (of sets)**,
if it does not contain the empty set `{}` as an element.

* `S := (V,P)`.
* `V` is a set of elements.
* `P` is a set of sets of elements.
* `V := E(P)` := "the union of all sets (s in P)"

clarifications

* No set `(s in P)` is allowed to be empty - i.e. `({} !in P)`
* `S` is a two-element tuple of possibly empty sets.
* `(s subset-of V)` for any `(s in P)`
* `(P strict-subset-of P(V))`

Note that `P` is a strict subset of `V`'s power-set `P(V)`. That is, all
elements in `P` are elements of `P(V)`. However, no element in `P` is allowed
to be empty.

* `(0 <= #P < #P(V))`

Note that `V` is empty if only if `P` is empty. That is because even though
no `(p in P)` may be empty, `P` itself is still allowed to be empty.

* `(#P = 0) <-> (#V = 0)`
* `(#P > 0) <-> (#V > 0)`

Note that `V` may hold elements of any kind. That is, there is no requirement
of what kind of elements `V` must hold. The only restriction there is, is that
all elements within `V` must be distinct from any other element in `V`. Other
than that, `V` may hold elements of one kind (homogenous), or elements of
different kinds (heterogenous).

**Memory hook**
A (simple) setup is a set of non-empty sets.

<!-- ======================================================================= -->
## derived statements

Note that the expression `(s in S)` is a simplification, which needs to be
understood as: `s` is a set of elements, and as such an element of the set
of sets `P` of setup `S`. That is, a more accurate expression would be:
`(s in P) and (P in S)`.

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
However, two distinct sets are still not necessarily disjoint.

* `disjoint <!=> distinct`
* (<!=) both sets may overlap each other.
* (<!=) both sets may be strictly related.

**CLARIFICATION**
In a setup, two disjoint sets are unrelated.
However, two unrelated sets are still not necessarily disjoint.

* `disjoint <!=> unrelated`
* (<!=) both sets may overlap each other.

**CLARIFICATION**
In a setup, two related sets are coupled.
However, two coupled sets are still not necessarily related.

* `coupled <=!> related`
* (=!>) both sets may overlap each other.
* hint: `(a <-> b) <-> (!a <-> !b)`

<!-- ======================================================================= -->
## Consistent setup (of sets)

**CLARIFICATION**
A set of sets `S` is said to be **a (consistent) setup (of nested sets)**,
if the following requirements are met:

0. `S := (V,P)`
1. `S` is a (simple) setup.
2. If two distinct sets in `S` have one or more elements in common,
   then one set is a subset of the other.

Note that requirement 2 will be referred to as "req-2" and
as "consistency with regards to the `subset-of` operator".

* `(s coupled-with t) -> (s related-to t)` is true if `(s != t)`
* Note that this statement is required to be true (/see/ "req-2" /).

Note that the intention of the above requirement is to guarantee that the setup
does not contain two sets that overlap each other. That is, any two non-empty
sets are either disjoint ex-or related with each other.

**CLARIFICATION**
A setup is consistent if `(#P <= 1)` is true.

* If `(#P == 0)`, then it does not contain two distinct sets
  which could be in conflict with req-2.
* If `(#P == 1)`, then it does not contain a 2nd distinct set
  which could cause a conflict with req-2.

**CLARIFICATION**
A consistent setup may contain sets that are disjoint to any other set in it.
That is, a setup is still consistent, even if all of its sets are disjoint.

<!-- ======================================================================= -->
## (coupled <-> related)

**CLARIFICATION**
Any two sets in a consistent setup are related to each other, if they have
one or more elements in common. Likewise, any two related sets in a consistent
setup are coupled:

* `(s coupled-with t) <-> (s related-to t)` is true for any two `s,t in P`

That statement is true, because ...

(1) `(s coupled-with t) <-> (s related-to t)` is true if `(s == t)` is true.
That is because, in the context of a setup, and by the definition of the
corresponding operators, that statement is always true. That is because any
non-empty set is always coupled-with and related-to itself.

(2) `(s coupled-with t) -> (s related-to t)` is true if `(s != t)` is true.
That is because that statement is required to be always true (i.e. req-2).

In addition to that, and if two distinct sets are disjoint (i.e. not coupled),
then both sets can not be related with each other.

(3) `(s coupled-with t) <- (s related-to t)` is true if `(s != t)` is true.
That is because, due to the definition of the `related-to` operator,
two related sets are always coupled with each other.

However, two non-empty distinct and unrelated sets are not always disjoint
(i.e. not coupled - e.g. overlap). But, the only requirement in an implication
(i.e. `(a -> b) := (!a or b)`) is, that `b` must always be true if `a` is true.
In contrary to that, `b` may hold any value if `a` is false. Consequently, the
above implication is, by the definition of the `related-to` operator, always
satisfied.

(4) `(s coupled-with t) <-> (s related-to t)` is true if `(s != t)` is true.
That is because `((a -> b) and (a <- b)) <-> (a <-> b)` (i.e. 2+3).

(5) `(s coupled-with t) <-> (s related-to t)` is true for any two `s,t in P`.
That is because that statement is true regardless of whether both non-empty
sets are equal or distinct (i.e. 1+4).

<!-- ======================================================================= -->
## (disjoint ex-or related)

**CLARIFICATION**
Any two sets in a consistent setup are either disjoint,
ex-or one set is a subset of the other.

* `(s disjoint-to t) ex-or (s related-to t)` is true for any two `s,t in P`

That statement is true, because it results from basic transformations:

(1) `(s coupled-with t) <-> (s related-to t)` is true for any two `s,t in P`
Is true because it is a consequence of the initial requirement.

(2) `not (s disjoint-to t) <-> (s related-to t)` is true for any two `s,t in P`
Is a valid transformation because `(s coupled-with t) <-> (s not disjoint-to t)`.

(3) `(s disjoint-to t) ex-or (s related-to t)` is true for any two `s,t in P`
Is a valid transformation because `(!a <-> b) <-> (a xor b)`.

<!-- ======================================================================= -->
## (coupled <-> strictly related), if distinct

**CLARIFICATION**
Any two distinct sets in a consistent setup are strictly related, if they have
one or more elements in common. Likewise, any two strictly related sets in a
consistent setup are coupled:

* `(s coupled-with t) <-> (s strictly-related-to t)` is true if `(s != t)`

That statement is true, because ...

(1) `(s coupled-with t) <-> (s related-to t)` is true if `(s != t)`.
That statement is true because it is a consequence of req-2.

(2) `(s related-to t) -> (s strictly-related-to t)` is true if `(s != t)`.
That statement is true because two distinct and related sets are always
strictly related. That is a consequence of the `strictly-related-to` operator.

(3) `(s coupled-with t) -> (s strictly-related-to t)` is true if `(s != t)`.
That statement is true as a result of the transitive (->) operator
in combination with `(s coupled-with t) -> (s related-to t))` - see (1)

(4) `(s related-to t) <- (s strictly-related-to t)` is true if `(s != t)`.
That statement is true because of the very definition of the
`strictly-related-to` operator.

(5) `(s coupled-with t) <- (s strictly-related to t)` is true if `(s != t)`.
That statement is true as a result of the transitive (->) operator
in combination with `(s coupled-with t) <- (s related-to t))` - see (1)

(6) `(s coupled-with t) <-> (s strictly-related to t)` is true if `(s != t)`.
That is because `((a -> b) and (a <- b)) <-> (a <-> b)` (i.e. 3+5).

Note that the above statement is obviously not true, if `(s == t)`. That is,
because no non-empty set is ever strictly related to itself. The statement
therefore only applies, if both sets are distinct.

Note that a consistent setup is consequently also
"consistent with regards to the `strict-subset-of` operator".

<!-- ======================================================================= -->
## (disjoint ex-or strictly related), if distinct

**CLARIFICATION**
Two distinct sets in a consistent setup are either disjoint,
ex-or one set is a strict subset of the other.

* `(s disjoint-to t) ex-or (s strictly-related-to t)` is true if `(s != t)`

That statement is true, because it results from basic transformations:

(1) `(s coupled-with t) <-> (s strictly-related-to t)` is true if `(s != t)`.
Is true because it is a consequence of the initial requirement.

(2) `not (s disjoint-to t) <-> (s strictly-related-to t)` is true if `(s != t)`.
Is a valid transformation because `(s coupled-with t) <-> (s not disjoint-to t)`.

(3) `(s disjoint-to t) ex-or (s strictly-related-to t)` is true if `(s != t)`.
Is a valid transformation because `(!a <-> b) <-> (a xor b)`.

<!-- ======================================================================= -->
## Strict setup (of sets)

**CLARIFICATION**
A setup is said to be **a (strict) setup (of nested sets)**,
if the following requirements are met:

0. `S := (V,P)`.
1. `S` is a consistent setup.

Note that a consistent setup is therefore equivalent to a strict setup.
That is, there are no additional requirements which need to be satisfied:
A consistent setup is equivalent to a strict setup.

This definition therefore stresses the consequences of the initial requirement
(req-2) of a consistent setup:

* Any two sets are either disjoint ex-or related.
* `(s disjoint-to t) ex-or (s related-to t)`, for any two `s,t in P`
* Two distinct sets are either disjoint ex-or strictly related.
* `(s disjoint-to t) ex-or (s strictly-related-to t)`, if `(s != t)`

Also note that, in the context of a strict setup, the following "statements"
related to any two sets in P are true:

* disjoint <!=> distinct
* disjoint <=> unrelated
* coupled <=> (strictly) related

**CLARIFICATION**
For any two distinct coupled sets within a strict setup, it can be stated that
one set is located inside ex-or outside of the other. Consequently, two such
sets in a strict setup are distinctively ordered. That is, one set is always
super-ordinate to, or more significant than the other.
