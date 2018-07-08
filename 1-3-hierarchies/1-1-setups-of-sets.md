
<!-- ======================================================================= -->
# Setups of sets

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

<!-- ======================================================================= -->
## Simple setup (of sets)

**CLARIFICATION**
A set of sets is said to be **a (simple) setup (of sets)**.

* `S := (V,P)`.
* i.e. a two-element tuple of sets.
* `V` is a set of values/elements.
* `P` is a set of subsets over `V`.

Note that `P` is a subset of `V`'s power-set (i.e. `P subset-of P(V)`).
That is, all elements in `P` are elements of `P(V)`.

Note that `V` is the union of all sets in `P` (i.e. `V` may be empty).
That is, a (simple) setup is completely defined by its set-of-sets `P`.

Note that the above example is a setup. The example would however no longer be
a setup, if number 3 would be removed from set C. That is, because this example
would then turn into a multiset of sets (i.e. sets C and F would be identical,
but still distinct sets - i.e. distinct objects that represent the same set).

Note that the expression "s in S" is a simplification which needs to be
understood as: s is a set of elements, and as such an element of the
set of sets P of the corresponding setup (i.e. "s in P").

<!-- ======================================================================= -->
## Consistent setup (of sets)

**CLARIFICATION**
A setup is said to be **a consistent setup (of sets)**,
if the following requirement is met:

* If two distinct sets have one or more elements in common,
  then one set is a subset of the other.

Note that this required characteristic is understood as
"consistent with regards to the `subset-of` operator".

* `(s != t) and (s coupled-with t) -> (s related-to t)`
* Note that this is by definition required to be true.
* Note that `(s coupled-with t)` excludes the empty set `{}`.

Note that an empty setup (i.e. an empty set of sets) is consistent. That is,
because it does not contain two distinct sets that could be in conflict with
the above requirement. The same reason allows to state that a setup is
consistent, if it contains one set only.

Note that this kind of consistency does not require that for each set (S1)
another set (S2) exists with which the first set (S1) has any elements in
common (e.g. set E, the empty set). That is, a setup is consistent, even
if all its sets are disjoint.

Note that, a consistent setup, which contains the empty set `{}` as an element,
is still consistent. That is, because the above requirement only needs to be
satisfied by sets that are not disjoint from one another. The empty set is
however disjoint to any set, and as such not required to be a subset of another
set (even though the empty set is a subset to any set). Because of that, two
distinct related sets are not necessarily coupled with each other. It can
therefore not be stated that "two distinct sets within a consistent setup are
either disjoint, ex-or one set is a subset of the other". That is, because the
empty set always fulfills both aspects at the same time (i.e. a singularity).

Note that the intention behind the above requirement is to guarantee that
the corresponding set-of-sets does not contain any two sets that overlap
each other. That is, two non-empty sets are either disjoint, ex-or related
to each other.

**CLARIFICATION**
If two distinct sets in a consistent setup have one or more elements in common,
then one set is a strict subset of the other.

(1) `(s related-to t)` is true.
That is, because `(s != t) and (s coupled-with t)` is required to be true.

(2) `(s != t)` is true.
That is, not just because both sets are required to be distinct entities, but
also because a consistent setup is still a set of sets. That is, `s` and `t`
differ in size and/or in the elements they hold.

(3) `(#s != #t)` is true.
That is, because `(s related-to t)` is true. Because of that, all the elements
of one set (e.g. `s`) are also elements of the other set (e.g. `t`). Because
of that, both sets can only differ in the number of elements they hold (e.g.
`(#s < #t)`).

(4) `(s strictly-related-to t)` is true.
That is, because `(s related-to t)` and `(#s != #t)` are true. The super-set
is therefore guaranteed to hold more elements than the sub-set.

* `(s != t) and (s coupled-with t) -> (s strictly-related-to t)`
* Note that this is a consequence of the initial requirement.

Note that a consistent setup is consequently also
"consistent with regards to the `strict-subset-of` operator".

<!-- ======================================================================= -->
## Strict setup (of sets)

**CLARIFICATION**
A setup is said to be **a strict setup (of sets)**,
if the following requirements are met:

0. `S := (V,P)`.
1. The setup is consistent.
2. The setup does not contain the empty set `{}`.

Note that ...

* `(#P < #P(V))` is true.
That is, because `{}` is never allowed

**CLARIFICATION**
Two distinct sets in a strict setup are either disjoint,
ex-or one set is a strict subset of the other.

(1) `(s != t)` is true.
That is, because the requirement is that both non-empty sets are distinct.
 
(2) `(s != t) and (s coupled-with t) -> (s strictly-related-to t)` is true.
That is, because a strict setup is also a consistent setup.

(3) `(s strictly-related-to t) -> (s coupled-with t) and (s != t)` is true.
That is, because the empty set `{}` is by definition not allowed to be an
element of a strict setup. Furthermore, two sets can not be strictly related,
if both sets are identical.

(4) `(s != t) and (s coupled-with t) <-> (s strictly-related-to t)` is true.
That is, because `((a -> b) and (a <- b))` is equivalent to `(a <-> b)`.

(5) `(s coupled-with t) <-> (s strictly-related-to t)` is true.
That is, because `(s != t)` is due to (1) always true and because `(T and b)`
is equivalent to `(b)`. Put differently, the focus is restricted to those
cases in which `(s != t)` is true.

(6) `(s !disjoint-to t) <-> (s strictly-related-to t)` is true.
That is, because `(s coupled-with t) <-> (s !disjoint-to t)` is true.

(7) `(s disjoint-to t) ex-or (s strictly-related-to t)` is true.
That is, because `(!a <-> b)` is equivalent to `(a ex-or b)`.

(8) `(s != t) <-> ((s disjoint-to t) ex-or (s-strictly-related-to t))` is
true. That is, because if `(s == t)`, then both sets are neither disjoint,
nor strictly related with each other. And due to (2-7), the right hand side
is true if `(s != t)`.

* `(s != t) <-> ((s disjoint-to t) ex-or (s strictly-related-to t))`
* Note that this is a consequence of the definition.

**CLARIFICATION**
For any two distinct coupled sets within a strict setup, it can be stated that
one set is located inside or outside of the other. That is, two such sets in a
strict setup are distinctively ordered:

* `(s strictly-related-to t) := (s strict-subset-of t) ex-or (t strict-subset-of s)`
