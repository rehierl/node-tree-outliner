
<!-- ======================================================================= -->
# (Simple) Hierarchy/Forest of sets

* (/see/ "core definitions" in "node trees" /)

<!-- ======================================================================= -->
## example

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

* Root set A is the parent set of sets B and C.
* Set B is the parent set of set D.
* Sets A and B both are outer or ancestor sets of set D.
* Sets B, C and D all are inner or descendant sets of set A.
* Sets B and C are sibling sets and disjoint to one another.

<!-- ======================================================================= -->
## core definitions

In regards to a strict setup, the following terms may be used:

* The **strict subsets** of a set
  are said to be the set's **inner** sets.
* The sets to which a set is an inner set
  are said to be the set's **outer** sets.

Note that, if the *simple subset* operator would have been used in the above
two definitions, then any set would be an inner and an outer set to itself
(i.e. loops). However, since the *proper subset* operator was used instead,
no set is an inner and/or an outer set to itself (i.e. no loops).

Note that two disjoint sets are not understood to be outside of each other, not
even if both sets have the same parent (i.e. siblings). That is because neither
of them is an inner set of the other. Hence, "outside" and "not inside" are not
equivalent!

* Any outer set of set `s` is said to be an **ancestor** set of `s`
  and as such **super-ordinate** to, or **more significant** than `s`.
* Any inner set of set `s` is said to be a **descendant** set of `s`
  and as such **sub-ordinate** to, or **less significant** than `s`.

Note that a set is no ancestor and no descendant to itself (i.e. no loops,
no cycles). Likewise, disjoint sets are neither ancestors nor descendants
to each other.

Note that the empty set `{}` is a strict subset to any non-empty set. Because
of that, any non-empty set is an ancestor to it. The empty set is therefore the
only set that has disjoint ancestors. Consequently, a strict setup must not
contain the empty set. From this point forward, all sets are therefore expected
to be non-empty.

* A set that has no ancestor
  (other than the universal set),
  is said to be a **root** set.
* The least significant ancestor of set `s`
  is said to be the **parent** set of `s`.
* The most significant ancestor of set `s`
  is said to be the **root (set) of** set `s`.
* Set `s` is said to be a **child** set of `t`,
  if `t` is the parent of `s`.
* Two sets that have the same parent
  are said to be **siblings** to each other.
* A set is said to be a **leaf**,
  if it has no descendant.

Note that none of the ancestors of a descendant are disjoint from one another.
They always have all the elements of the descendant in common. Consequently,
a strict setup does not allow its sets to have more than one parent. That is
because each non-root set has exactly one most significant (i.e. its root)
and exactly one least significant (i.e. its parent) ancestor.

* root set -> ... -> parent set -> child set -> ... -> leaf set

Note that an ancestor always has more elements than any of its descendants.
Likewise, a descendant always has fewer elements than any of its ancestors.
That is a consequence of the strict relationship between an ancestor and its
descendants. Consequently, each set in a strict setup either has no parent
at all (e.g. a root) ex-or exactly one parent.

Note that a non-empty strict setup always has one or more root sets. That is,
because (1) a strict setup that only has a single set has that set as its only
root. Furthermore, (2) the addition of a new set to a strict setup, in such a
way that the setup still satisfies all the requirements, will (2.1) add a new
root (in case that set is disjoint to any pre-existing set), (2.2) turn one or
more existing root sets into non-root sets (in case these are descendant to the
new set), or (2.3) add the new set as a descendant set to a pre-existing root.

That is, if a new set is added to a strict setup, the number of root sets
is increased by one (`#RS° = #RS+1`, cases 1 and 2.1), remains unchanged
(`#RS° = #RS`, cases 2.2 and 2.3) or is decreased by a certain amount
(`#RS° = #RS-N` for `N in [0,#RS-1]`, case 2.2).

**SUMMARY**
A strict setup has the following properties:

* Any set is a strict subset to all of its ancestors.
* The ancestors of a set are strictly related to each other.
* A set either has ancestors ex-or none at all.
* A set either has a parent ex-or the set is a root.
* A set that has a parent also has a root set.
* A strict setup has no loops and no cycles.
* A non-empty strict setup has at least one root.

<!-- ======================================================================= -->
## remarks

**CLARIFICATION**
The sets of ancestor and descendant sets may be defined as follows:

* where `h` represents the corresponding hierarchy
* `A(s), A(s,h) := { a | (s strict-subset-of a) for any (a in P) }`
* `D(s), D(s,h) := { d | (d strict-subset-of s) for any (d in P) }`
* `AS(h) := { a | (a in A(s,h)) for any (s in P) }`
* `DS(h) := { d | (d in D(s,h)) for any (s in P) }`

Note that ...

* `PS := AS`, `CS := DS`
* i.e. each parent has a descendant and is itself an ancestor
* i.e. each child has an ancestor and is itself a descendant
* `RS := (PS \ CS)`, `LS := (CS \ PS)`
* i.e. each set is either a root ex-or a child
* i.e. each set is either a leaf ex-or a parent

**CLARIFICATION**
The following definitions may be used for clarification purposes:

* `(a in AS)` - the set of all ancestor sets
* `(d in DS)` - the set of all descendant sets
* `(r in RS)` - the set of all root sets
* `(p in PS)` - the set of all parent sets
* `(c in CS)` - the set of all child sets
* `(l in LS)` - the set of all leaf sets

Note that ...

* `(#RS, #PS, #CS and #LS) <= #P`
* `RS` and `LS` both empty if and only if `(P == Ø)`
* i.e. a non-empty strict setup always has a root and a leaf
* `PS` and `CS` are both empty if `(RS == LS)`
* i.e. if each root is a leaf

**CLARIFICATION**
Each set `(s in P)` in a strict setup `S := (V,P)`
has a unique **rooted path** `p := (s0,s1,...,sk)`
that can be used to reference `s`.

* `p(i) = s(i) = si`
* `s(i) in P` and `(s(i) parent-set-of s(i+1))`
* where `s0` represents the universal set
* i.e. an ancestor set to any set possible
* any root is a child to the universal set
* `(s1 in P)` is a root of `S`
* `(s == sk)` is true

Note that there are several, less formal notations possible that can be used
to denote the rooted path of a set. The notation that will be used here is:

* `/...` is intended to be equivalent to `s0/...`
* `/s1` - the rooted path of root set `s1`
* `/s1/.../sk` - the rooted path of set `sk` that begins in its root set `s1`

Examples:

```
|-A-------|   |-B-----------|
| 1 |-A-| |   | |-A-| |-B-| |
|   | 2 | |   | | 1 | | 2 | |
|   |---| |   | |---| |---| |
|---------|   |-------------|
```

* Root sets /A and /B both represent separate hierarchies.
* Set /A/A is a strict subset of root set /A.
* Set /B/A is a strict subset of root set /B.
* Set /B/B is a strict subset of root set /B.

<!-- ======================================================================= -->
## (Simple) Hierarchy/Forest of sets

**CLARIFICATION**
Any strict setup `S := (U,P)` corresponds with a forest of trees.

* `G := (P,E)` where `(E subset-of P×P)`
* `P` is the setup's set of sets
* `E` is the setup's set of edges
* `e := (p1,p2)` such that `(e in E)` and `(p1 parent-of p2)`

**CLARIFICATION**
A setup is said to be **a (simple) hierarchy (of sets)**,
if the following requirements are met:

1. `H := (V,P)` is a strict setup
2. The setup has one and only one root set.

A simple hierarchy has the following properties:

* A hierarchy is not empty since it must have a root.
* No set in a hierarchy is empty (i.e. `(Ø !in P)`).
* A hierarchy has no loops and no cycles.
* A hierarchy has no overlapping sets (req-2).
* Two sets in a hierarchy are either disjoint ex-or related.
* Two distinct sets are either disjoint ex-or strictly related.
* Each set either has no ex-or one parent.
* A hierarchy always has one or more leafs.
* Ancestors have more elements than their descendants.
* In a hierarchy, each set has a unique rooted path (i.e. /root/to/set).

**CLARIFICATION**
A setup is said to be **a (simple) forest (of hierarchies)**
or "a forest of simple hierarchies", if the following requirements are met:

1. `F := (V,P)` is a strict setup.
2. The setup has zero, one or more than one root sets.

Any strict setup is therefore a forest of hierarchies.
In contrary to that, not every strict setup is also a hierarchy.

* strict setup <=> a forest of hierarchies
* a hierarchy => a forest of hierarchies

Note that, in contrary to a hierarchy, a forest may be empty.
That is, a forest is not required to even have a root.

Note that a forest is not strictly "a set of sets of sets" (i.e. "a set of
hierarchies"). A forest is like a hierarchy, one "flat" set of sets. Because
of that, any operation defined on a set of sets (e.g. union, subset, etc.)
can be used in the context of forests.

Note that any two hierarchies in a forest of N hierarchies are disjoint. That
is because the forest would otherwise either have less than N hierarchies, or
it would not even be a strict setup. A forest therefore corresponds with a set
of disjoint hierarchies.

**CLARIFICATION**
The theoretical **set of all possible hierarchies (H)** and the theoretical
**set of all possible forests (F)** are defined as follows:

* `H := { h | "h is a hierarchy" }`
* `F := { f | "f is a forest of hierarchies" }`

Because of that, the expression `(h in H)` states that `h` is expected to be a
hierarchy. Likewise, `(f in F)` states that `f` is expected to be a forest of
hierarchies.

* `(H strict-subset-of F)`

Note that an empty setup is a forest, but not a hierarchy.

<!-- ======================================================================= -->
## remarks

Note that the definition of a hierarchy does not cover the process of forming
the sets it contains. It merely describes how these need to be related with
each other. That is, the subsets of the hierarchy's root may be formed in any
number of different ways. Hence, further aspects need to be taken into account
in order to choose one method over the other.

**CLARIFICATION**
The root set `(r in P)` of a hierarchy `H := (V,P)` is equal to `V`. Because
of that, a hierarchy's root set is the largest set (i.e. in terms of number
of elements) in `P`.

That is because (1) `V` is the union of all sets in `P` (i.e. `V := E(P)`),
and (2) any other set `(s in P)` is a strict subset to the root (since the
setup would otherwise have more than one root).

**CLARIFICATION**
Two hierarchy instances `H1` and `H2` are disjoint, if their roots are
disjoint. (The focus here is on two entities, i.e. two separate setups).

Note that, if root `r1` of `H1` is disjoint to `r2` of `H2`,
then any subset `s1` of `r1` is disjoint to any subset `s2` of `r2`.

**CLARIFICATION**
Any subset of a hierarchy `H := (V,P)` (i.e. more accurately any subset
of `P`), corresponds with a forest of hierarchies.

Note that the subset of a hierarchy will itself be a hierarchy,
if the hierarchy's root is included.
