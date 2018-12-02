
<!-- ======================================================================= -->
# (Simple) Setup of trees

* (/see/ "setup of sets" in "hierarchy of sets" /)

Note that "setup of sets" contains proofs which confirm the clarifications
that will follow in this section.

<!-- ======================================================================= -->
# Simple Setup of trees

**CLARIFICATION**
A set of trees is said to be **a (simple) setup (of trees)**, if it does not
contain an empty tree. (Obviously, there are no empty trees since each tree
must have at least a root node. Hence, every set of trees is a setup of trees).

* `S := (U,P)` is a setup of trees
* `P` is a set of trees
* `U` is the union of all trees in `P`

remarks

* Setup `S` is a two-element tuple of set `P` and the union graph `U`
* No tree `(t in P)` is allowed to be empty - i.e. `(Ø !in P)`
* `(P subset-of P(U))` and `(0 <= #P <= #P(U))`
* where `P(U)` is the set of all possible subtrees of graph `U`
* i.e. `P(U)` is similar to the powerset of a simple set of elements
* `(t subtree-of U)` is true for any `(t in P)`

Note that `U` is empty if any only if `P` is empty. That is because even
though no `(t in P)` may be empty, `P` itself may still be empty.

* `(P == Ø) <-> (U == Ø)`
* `(P != Ø) <-> (U != Ø)`

Note that, since a tree is by definition always a non-empty graph, any set of
trees is equivalent to a simple setup of trees. However, the exact nature of
the union graph `U` is undetermined since a simple setup of trees does not have
any requirement in regards to the relationship between the trees in `P`. That
is, `U` may or may not be a non-tree graph. Likewise, `P` may or may not be
equivalent to a forest of disjoint trees.

**Memory hook**
A (simple) setup is equivalent to an arbitrary set of trees
which is accompanied by the union graph of all its trees.

<!-- ======================================================================= -->
## remarks

**CLARIFICATION**
Two distinct coupled trees in a setup are not necessarily related with each
other since both trees may overlap/cross each other.

**CLARIFICATION**
In a setup, two disjoint trees are distinct.
However, two distinct trees are not necessarily disjoint.

* `disjoint <!=> distinct`
* (<!=) both trees may overlap each other
* (<!=) both trees may be properly related

**CLARIFICATION**
In a setup, two disjoint trees are unrelated.
However, two unrelated trees are not necessarily disjoint.

* `disjoint <!=> unrelated`
* (<!=) both trees may overlap each other

**CLARIFICATION**
In a setup, two related trees are coupled with each other.
However, two coupled trees are not necessarily related.

* `coupled <=!> related`
* (=!>) both trees may overlap each other

<!-- ======================================================================= -->
## remarks

Note that the inclusion of the "overlaps" relationship makes it difficult to
classify the relationship between two trees. In addition to that, the definition
of "overlaps" (i.e. both trees have a non-empty intersection and are unrelated
to each other) is not as abundantly clear as the definition of the "related-to"
relationship (i.e. without any exception, all the elements of one tree are also
elements of the other tree).

Note that the expression `(t in S)` is a syntactic simplification, which needs
to be understood as: "`t` is a tree, and as such an element of the set of trees
`P` in setup `S`". That is, a more accurate expression would therefore be:
`(t in P) and (P in S)`.

<!-- ======================================================================= -->
## Consistent setup (of trees)

**CLARIFICATION**
A set of trees `S` is said to be **a consistent setup (of trees)**,
if the following requirements are met:

1. `S := (U,P)` is a (simple) setup of trees.
2. If two distinct trees in `P` are coupled, then both trees are related.

Note that requirement 2 will be referred to as req-2 and
as "consistency in regards to the subtree-of operator".

* `(s coupled-with t) -> (s related-to t)` is true if `(s != t)`
* Note that this expression is, due to req-2, required to be true.

Note that req-2 is needed to guarantee that a setup does not contain overlapping
trees. That is, any two trees are required to either be disjoint ex-or related
with each other (see below).

**CLARIFICATION**
A setup counts as being consistent if `(#P <= 1)` is true.

* If `(#P == 0)`, then it does not contain two trees
  which could be in conflict with req-2.
* If `(#P == 1)`, then it does not contain a 2nd tree
  which could cause a conflict with req-2.

**CLARIFICATION**
A consistent setup may contain trees that are disjoint to any other tree in it.
That is, a setup is still consistent, even if the setup is equivalent to a set
of disjoint trees.

<!-- ======================================================================= -->
## (coupled <-> related)

**CLARIFICATION**
Any two trees in a consistent setup are related to each other, if they are
coupled with each other. Likewise, any two related trees in a consistent
setup are coupled with each other.

* `(s coupled-with t) <-> (s related-to t)` is true for any two `s,t in P`
* (/see/ "setup of sets" in "hierarchy of sets" /)

<!-- ======================================================================= -->
## (disjoint ex-or related)

**CLARIFICATION**
Any two trees in a consistent setup are either disjoint
ex-or one is a subtree of the other.

* `(s disjoint-to t) ex-or (s related-to t)` is true for any two `s,t in P`
* (/see/ "setup of sets" in "hierarchy of sets" /)

<!-- ======================================================================= -->
## (coupled <-> strictly related), if distinct

**CLARIFICATION**
Any two distinct coupled trees in a consistent setup are strictly related.
Likewise, any two strictly related trees in a consistent setup are coupled
with each other.

* `(s coupled-with t) <-> (s strictly-related-to t)` is true if `(s != t)`
* (/see/ "setup of sets" in "hierarchy of sets" /)

Note that this expression is obviously not true if `(s == t)`.
That is because no tree is strictly related to itself. 

Note that a consistent setup is therefore also
"consistent in regards to the strict-subtree-of operator".

<!-- ======================================================================= -->
## (disjoint ex-or strictly related), if distinct

**CLARIFICATION**
Two distinct trees in a consistent setup are either disjoint,
ex-or one is a proper subtree of the other.

* `(s disjoint-to t) ex-or (s strictly-related-to t)` is true if `(s != t)`
* (/see/ "setup of sets" in "hierarchy of sets" /)

<!-- ======================================================================= -->
## Strict setup (of trees)

**CLARIFICATION**
A setup is said to be **a (strict/proper) setup (of trees)**,
if the following requirements are met:

1. `S := (U,P)` is a consistent setup.

Note that a consistent setup is therefore synonymous to a strict setup.
That is, there are no additional requirements that need to be satisfied.

This definition therefore stresses the consequences of req-2:

* Any two trees are (disjoint ex-or related).
* `(s disjoint-to t) ex-or (s related-to t)`, for any two `s,t in P`
* Any two distinct trees are (disjoint ex-or strictly related).
* `(s disjoint-to t) ex-or (s strictly-related-to t)`, if `(s != t)`

Also note that, in the context of a strict setup, the following "statements"
in regards to any two trees in `P` are true:

* disjoint <!=> distinct
* disjoint <=> unrelated
* coupled <=> (strictly) related

<!-- ======================================================================= -->
## remarks

Note that, for any two distinct coupled trees in a strict setup, it can be
stated that the set of nodes of one tree is located inside ex-or outside of
the set of nodes of the other tree. Consequently, two such trees in a strict
setup are distinctively ordered. That is, one tree is super- or sub-ordinate
to the other (aka. more or less significant than).

**TODO** - lookup HTML's "well formed" rule
- then define "a well formed setup"
