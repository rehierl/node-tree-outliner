
<!-- ======================================================================= -->
# (Simple) Hierarchy/Forest of sets

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

* (/see/ "core definitions" in "node trees" /)

In regards to a strict setup, the following references may be used:

* All **strict subsets** of a set
  are said to be the set's **inner** sets.
* All sets to which a set is an inner set
  are said to be the set's **outer** sets.

Because any set is a *simple subset* to itself, any set can be understood to
be an inner and an outer set to itself (loops). In contrary to that no set is
a *strict subset* and therefore neither a strict inner, nor a strict outer set
to itself (no loops).

Note that two sets, which are disjoint from one another, are not understood
to be outside of each other, not even if both sets have the same parent set
(i.e. siblings). That is because neither of them is an inner set of the other.
Hence, "outside" and "not inside" are not equivalent!

* Any outer set of set `s` is an **ancestor set** to `s`
  and as such **super-ordinate** to, or **more significant** than `s`.
* Any inner set of set `s` is a **descendant set** to `s`
  and as such **sub-ordinate** to, or **less significant** than `s`.

Note that no set is understood to be an ancestor and/or a descendant set to
itself (no loops). Likewise, disjoint sets are neither understood as being
ancestors nor descendants to each other.

Note that the empty set `{}` is a strict subset to any non-empty set. Because
of that, any non-empty set is an ancestor set to the empty set. The empty set
is therefore the only set that would have disjoint ancestors. Consequently, a
strict setup must not contain the empty set. From this point forward, all sets
are expected to be non-empty.

* A set, that has no ancestor set
  (other than the universal set),
  is said to be a **root (set)**.
* The least significant ancestor set of set `s`
  is said to be the **parent (set)** of `s`.
* The most significant ancestor set of set `s`
  is said to be the **root (set) of** set `s`.
* Set `s` is said to be a **child (set)**
  of set `t`, if `t` is the parent set of `s`.
* Two sets which have the same parent set
  are said to be **siblings**.
* A set is said to be a **leaf (set)**,
  if it has no descendant set.

Note that none of the ancestors of a descendant set are disjoint from one
another. They always have at least all the elements of the descendant set
in common. Consequently, a strict setup does not allow its sets to have more
than one parent set. That is, each non-root set always has exactly one least
significant ancestor and therefore exactly one parent set. Likewise, each
non-root set always has exactly most significant ancestor as its root set.

* root set -> ... -> parent set -> child set -> ... -> leaf set

Note that a set is not a parent set to itself (no loops). That is because
a set is not an ancestor to itself. Consequently, each set within a strict
setup either has no parent set (e.g. a root set) ex-or exactly one parent set.

Note that an ancestor set always has more elements than any of its descendant
sets. Conversely, a descendant set always has fewer elements than any of its
ancestors. That is a direct consequence of the strict relationship between
ancestor and descendant sets.

Note that a set can not be an ancestor set to itself (no cycles). That is,
because a set can not be an outer set to itself. Likewise, a set can not be
a descendant set to itself. That is because a set can not be an inner set to
itself as it is no strict subset to itself.

Note that a non-empty strict setup always has one or more root sets. That is,
because (1) a strict setup that only has a single set has that set as its only
root set. Furthermore, (2) the addition of a set to a strict setup, in such a
way that the setup still satisfies all the requirements of a strict setup, will
(2.1) add a new root set (in case that new set is disjoint to any pre-existing
set), (2.2) turn one or more existing root sets into non-root sets (in case
these root sets are descendant to the new set), or (2.3) add the new set as a
descendant set to an existing root set.

That is, if a new set is added to a strict setup, the number of root sets
is increased by one (`#RS' = #RS+1`, cases 1 and 2.1), remains unchanged
(`#RS' = #RS`, cases 2.2 and 2.3) or is decreased by a certain amount
(`#RS' = #RS-N` for `N in [0,#RS-1]`, case 2.2).

**SUMMARY**
A strict setup has the following properties:

* Any set is a strict subset to all of its ancestors.
* The ancestors of a set are strictly related to each other.
* A set either has one or more ancestors, ex-or none at all.
* A set either has a parent set, ex-or the set is a root set.
* A strict setup has no loops and no cycles.
* A non-empty strict setup always has one or more root sets.
* A set that has a parent set also has a root set.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The sets of ancestor/descendant sets may be defined as follows:

* where `h` represents the corresponding hierarchy
* `A(s), A(s,h) := { a | (s strict-subset-of a) for any (a in P) }`
* `D(s), D(s,h) := { d | (d strict-subset-of s) for any (d in P) }`
* `AS(h) := { a | (a in A(s,h)) for any (s in P) }`
* `DS(h) := { d | (d in D(s,h)) for any (s in P) }`

Note that ...

* `PS := AS`, `CS := DS`
* i.e. each parent has a descendant and is itself an ancestor
* i.e. each child has an ancestor and is itself a descendant
* `RS := (PS - CS)`, `LS := (CS - PS)`
* i.e. each set is either a root ex-or a child
* i.e. each set is either a leaf ex-or a parent

**CLARIFICATION**
The following definitions may be used to clarify statements

* `(a in AS)` - the set of all ancestor sets
* `(d in DS)` - the set of all descendant sets
* `(r in RS)` - the set of all root sets
* `(p in PS)` - the set of all parent sets
* `(c in CS)` - the set of all child sets
* `(l in LS)` - the set of all leaf sets

Note that ...

* `(#RS, #PS, #CS and #LS) <= #P`
* `RS` and `LS` are empty if, and only if `(#P == 0)`
* i.e. a non-empty strict setup always has a root and a leaf
* `PS` and `CS` are both empty if `(#RS == #LS)`

**CLARIFICATION**
Each set `s in P` in a strict setup `S := (V,P)`
has a unique **rooted path** `p := (s0,s1,...,sk)` such that ...

* `p(i) = s(i) = si`
* `s(i) in P` and `(s(i) parent-set-of s(i+1))`
* where `s0` represents the universal set
* i.e. an ancestor set to any set possible
* any root set is a child set of the universal set
* `s1 in P` is a root set of `S`, and `(s == sk)`

Note that there are several, less formal notations possible that can be used
to denote the rooted path of a set. The notation that will be used here is:

* `/...` is intended to be equivalent to `s0/...`
* `/s1` - the rooted path of a root set `s1`.
* `/s1/.../sk` - the rooted path of set `sk` that begins in its root set `s1`.

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
Any strict setup of sets represents a forest of directed unordered trees.
Based on a strict setup, the following relation can be defined:

* `R := (P,G)` where `(G subset-of PxP)`
* `e := (p1,p2)` such that `(e in G)` and `(p1 parent-set-of p2)`
* `P` is the hierarchy's set of sets
* `G` is the graph (aka. set of edges)

**CLARIFICATION**
A setup is said to be **a (simple) hierarchy (of sets)**,
if the following requirements are met:

0. `H := (V,P)`
1. The setup is strict.
2. The setup has exactly one root set.

A simple hierarchy has the following properties:

* A hierarchy is not empty as it must have a root set.
* A hierarchy does not contain the empty set - `{} !in P`.
* A hierarchy has no loops and no cycles.
* A hierarchy has no overlapping sets (req-2).
* Two sets are either disjoint ex-or related.
* Two distinct sets are either disjoint ex-or strictly related.
* Each set either has no, ex-or exactly one parent set.
* A hierarchy always has one or more leaf sets.
* Ancestor sets have more elements than their descendant sets.
* Each set has a distinct rooted path (i.e. /root/to/set).

**CLARIFICATION**
A setup is said to be **a (simple) forest (of hierarchies)**
or "a forest of simple hierarchies", if the following requirements are met:

0. `F := (V,P)`
1. The setup is a strict.
2. The setup has zero, one or more than one root sets.

Note that, in contrary to a hierarchy, a forest may be empty.
That is, a forest is not required to have even a single root set.

* strict setup <=> a forest of hierarchies
* a hierarchy => a forest of hierarchies

Note that any strict setup is a forest of hierarchies. That is, a forest is
not strictly "a set of sets of sets" (i.e. "a set of hierarchies"). A forest
is like a hierarchy, one set of "flat" sets. Because of that, any operation
defined on a set of sets (e.g. union, subset, etc) can be used in combination
with forests.

Note that any two hierarchies in a forest of N hierarchies are disjoint. That
is, because the forest would otherwise either have less than N hierarchies, or
it would not even be a strict setup. A forest is therefore a set of disjoint
hierarchies.

**CLARIFICATION**
The theoretical **set of all possible hierarchies (H)** and the theoretical
**set of all possible forests (F)** are defined as follows:

* `H := { h | "h is a hierarchy" }`
* `F := { f | "f is a forest of hierarchies" }`

Because of that `(h in H)` states that `h` must be a hierarchy.
Likewise, `(f in F)` states that `f` must be a forest of hierarchies.

* `(H strict-subset-of F)`

Note that an empty setup is a forest but not a hierarchy.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The root set (r in P) of a hierarchy `H := (V,P)` is equal to V. Because
of that, a hierarchy's root set is the largest set (i.e. in terms of number
of elements) in P.

That is because (1) V is the union of all sets in P (i.e. V := E(P)),
and (2) any other set (s in P) is a strict subset to the root set (r in P).

**CLARIFICATION**
Two distinct hierarchies are disjoint, if their root sets are disjoint.

Note that, if root set `r1` is disjoint to `r2`,
then any subset `s1` of `r1` is disjoint to any subset `s2` of `r2`.

**CLARIFICATION**
Any subset of a hierarchy `H := (V,P)` (i.e. more accurately any subset
of `P`), in general represents a forest of hierarchies.

Note however that, under certain circumstances (i.e. the hierarchy's
root set is included), the subset will itself be a hierarchy.
