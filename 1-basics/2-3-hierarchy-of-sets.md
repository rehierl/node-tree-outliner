
<!-- ======================================================================= -->
# Hierarchy of sets

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
* Sets B and C are sibling sets and independent from one another.

With regards to a consistent setup, the following references may be used:

* All (strict) subsets of a set
  are said to be the set's **(strict) inner** sets.
* All sets to which a set is an (strict) inner set
  are said to be the set's **(strict) outer** sets.

Because any set is a subset to itself, any set can be understood to be an
inner and an outer set to itself (loops). In contrary to that no set is a
strict subset and therefore neither a strict inner, nor a strict outer set
to itself (no loops).

Note that two sets, which are disjoint from each other, are not understood
to be outside of each other, not even if both sets have the same parent set
(i.e. siblings). That is, "outside" and "not inside" are not equivalent.

* Any strict outer set of set S is an **ancestor set**
  and as such **super-ordinate** to, or **more significant** than S.
* Any strict inner set of set S is a **descendant set**
  and as such **sub-ordinate** to, or **less significant** than S.

Note that no set is understood to be an ancestor
and/or a descendant set to itself (no loops).

Note that the empty set is a strict subset to any non-empty set. Because of
that, any non-empty set is an ancestor set to the empty set. The empty set is
therefore the only set that may have disjoint ancestor sets. Consequently, a
hierarchy (see below) must not contain the empty set. From this point on, all
sets are assumed to be non-empty.

* A set, that has no ancestor set,
  is said to be a **root set**.
* The least significant ancestor set of set S
  is said to be the **parent set** of S.
* Set S1 is said to be one of the **child sets**
  of set S2, if S2 is the parent set of S1.
* Two sets that have the same parent set
  are said to be **siblings** to each other.

Note that none of the ancestors of a descendant set are disjoint from one
another. They always have at least all the elements of the descendant set in
common. Consequently, a strict setup does not allow its sets to have more than
one parent set. That is, all sets that have one or more ancestors always have
exactly one least significant ancestor and therefore exactly one parent set.
As a matter of consequence, each set that has a parent set also has exactly
one root set as its ancestor, which is the set's most significant ancestor.

Note that a set is not a parent set to itself (no loops). That is, because
a set is not understood to be an ancestor to itself. Consequently, each set
either has no parent set (e.g. a root set), ex-or exactly one parent set.

Note that a set can not be an ancestor set to itself (no cycles). Likewise,
a set can not be a descendant set to itself. That is, because a set can not
be a subset to one of its strict subsets. These inner sets always have less
elements than all of their ancestor sets.

Note that a non-empty strict setup always has one or more root sets. That is,
because (1) a strict setup that only contains a single set has that set as a
root set. In such a case, the setup does not have a set which could be an
ancestor to that set. Furthermore, (2) the addition of a set to a strict setup,
in such a way that the setup remains to be strict, will either add an additional
root set, or a descendant set (i.e. a non-root set) to an existing set.

**CLARIFICATION**
With regards to the above definitions,
a strict setup has the following properties:

* A set is a strict subset to all of its ancestors.
* The ancestors of a set are all coupled with each other.
* A set either has one or more ancestors, ex-or none at all.
* A set either has a parent set, ex-or the set is a root set.
* No set has more than one parent set.
* A strict setup has no loops and no cycles.
* A strict setup always has one or more root sets.
* No set has more than one root set as an ancestor.

**CLARIFICATION**
Each set `s in P` in a strict setup `S := (V,P)`
has a unique **rooted path** `p := (s0,s1,...,sk)` such that ...

* `p(i) = s(i) = si`
* `s(i) in P` and `(s(i) parent-set-of s(i+1))`
* `s0` is the universal set
* `s0` is a virtual parent set that contains
  all sets possible root sets as its child sets
* `s1 in P` is a root set, and `(s == sk)`

Note that there are several, less formal notations possible to denote the
rooted path of a set. The notation that will be used below is a follows:

* note that `s0/...` <=> `/...`
* `/s1` - the rooted path of a root set `s1`.
* `/s1/.../sk` - the rooted path of set `sk` begins with root set `s1`.
* `#p` will be used to refer to the length of the rooted path `p`.

Note that each element within a rooted path is a set of possibly infinitely
many elements.

```
|-A-------|   |-B-----------|
| 1 |-A-| |   | |-A-| |-B-| |
|   | 2 | |   | | 1 | | 2 | |
|   |---| |   | |---| |---| |
|---------|   |-------------|
```

* Root sets A and B both represent separate hierarchies.
* Set /A/A is a strict subset of root set A.
* Sets /B/A and /B/B are both strict subsets of root set B.

<!-- ======================================================================= -->
## Hierarchies, Forests

**CLARIFICATION**
A multiset (of sets) is said to be **a (simple) hierarchy (of sets)**,
if the following requirements are met:

0. `H := (V,P)`
1. The multiset is a non-empty strict setup.
2. The setup has exactly one root set.

Some of the properties of a hierarchy are:

* A hierarchy has no loops and no cycles.
* A hierarchy has no overlapping sets.
* Two distinct sets are either disjoint,
  ex-or one is a strict subset of the other.
* Each set either has no, ex-or exactly one parent set.
* Each set has a distinct rooted path (i.e. /root/to/set).
* Ancestor sets have more elements than their descendant sets.

**CLARIFICATION**
Two hierarchies are said to be disjoint, if their root sets are disjoint.

Note that, if set `r1` is disjoint from `r2`,
then any subset `s1` of `r1` is disjoint to any subset `s2` of `r2`.

**CLARIFICATION**
A multiset (of sets) is said to be **a (simple) forest (of hierarchies)**
or "a forest of simple hierarchies", if the following requirements are met:

0. `F := (V,P)`
1. The multiset is a strict setup.
2. The setup has zero, one or more root sets.

Note that a strict setup is automatically a forest of hierarchies. That is, a
forest is not "a set of sets of sets" (i.e. "a set of hierarchies"). A forest
is like a hierarchy, a single set of sets. Because of that, any operation
defined on a set of sets can be used in combination with forests.

* strict setup <=> a forest of hierarchies
* a hierarchy => a forest of hierarchies

Note that, in contrary to a hierarchy, a forest may be empty.
That is, a forest is not required to contain even a single root set.

Note that any two hierarchies in a forest of N hierarchies are disjoint. That
is, because the forest would otherwise either have less than N hierarchies, or
it would not even be a strict setup. From a loose perspective, a forest is
a set of disjoint hierarchies.

**CLARIFICATION**
Any subset of a hierarchy is a forest of hierarchies.

Note that, under certain circumstances (i.e. the hierarchy's root set
is included), the subset will itself be a hierarchy.

<!-- ======================================================================= -->
## Characteristic subset (CSS)

```
|-A-------|   |-B-----------|
| 1 |-A-| |   | |-A-| |-B-| |
|   | 2 | |   | | 1 | | 2 | |
|   |---| |   | |---| |---| |
|---------|   |-------------|
```

* CSS(/A)={1}, CSS(/A/A)={2}
* CSS(/B)={}, CSS(/B/A)={1}, CSS(/B/B)={2}

**CLARIFICATION**
The **characteristic subset** CSS of set `s` in hierarchy `H := (V,P)`
is defined as follows:

* `css(s), css(s,H) := css-of-set(s,H)`
* `css-of-set(s,H) := s - (union of all descendant sets of s in P)`
* signature: (P,H) -> P(V)

Note that ...

* Each set has exactly one CSS.
* The CSS of a set is an element of the powerset `P(V)`.
* A CSS is not an element in `P` (i.e. implicit, not explicit).

The characteristic subset `css(s)` of set `s` in hierarchy `H`, is a potentially
empty subset of `s`, such that none of the elements in `css(s)` is also an
element of any of the descendants of `s`.

Consequently, set `s` and all of its ancestor sets must contain all the elements
in the set's characteristic subset. Otherwise, hierarchy `H` would not be a
consistent setup (i.e. in conflict with `subset-of`) and therefore also not a
hierarchy. Put differently, `s` is the least significant set that contains all
the elements in `css(s)`. That is, set `s` is the parent set of `css(s)`.

Note that the CSS of a set is empty, if the corresponding set is the union of
its descendant sets (e.g. CSS(/B)). That is, a (simple) hierarchy does not
guarantee that all the characteristic subsets of its sets are non-empty.

**CLARIFICATION**
Given a non-empty CSS, and the corresponding hierarchy `H := (V,P)`,
the parent set of the CSS can be identified as follows:

1. Determine all the sets in H to which the CSS is a subset.
2. Return the least significant set of these sets.

Note that this operation will be referred to as the `set-of-css()` operation:

* `set-of-css(css,H)` := "the parent set of `css` in `H`"
* signature: (P(V),H) -> P

Note that ...

* The set of a CSS can not be determined, if the supplied CSS is empty.
* The CSS of each set must be non-empty in order to identify each set.

<!-- ======================================================================= -->
## Relationship between the elements in V and P

(warning - not sure, if the following is error-free
or even if it covers all possible cases)

Note that this section is with regards to the requirements
which a given set of sets P thrusts upon the set of elements V.

```
|-A-------|   |-B-----------|   |-C---------------------|
| 1 |-A-| |   | |-A-| |-B-| |   | |-A-| |-B-----------| |
|   | 2 | |   | | 1 | | 2 | |   | | 1 | | |-C-| |-D-| | |
|   |---| |   | |---| |---| |   | |---| | | 2 | | 3 | | |
|---------|   |-------------|   |       | |---| |---| | |
                                |       |-------------| |
                                |-----------------------|
```

(if each set is only allowed to hold a single element)

A hierarchy is minimal, if none of the elements in V can be removed without
changing the structure of the hierarchy and/or without violating any of the
hierarchy's requirements (e.g. no empty set, one root set).

(1) V must have one (unique) element per leaf set `l in L`

* `L := { l | (l in P) and (l is a leaf set) }`
* because H is not allowed to contain empty sets
* each leaf set `l` must have a unique element in V
* because it would otherwise not be possible
  to distinguish the leaf sets from one another
* `(#L <= #V)` must be true

(2) V must have one (unique?) element per parent `p in P1`

* `P1 := { p | (p in P) and (p is a parent) and (p has one child only) }`
* because it would otherwise not be possible to distinguish
  such a parent `p` from parent `q in P1` if `(p != q)`
* `(#L + #P1 <= #V)` must be true

<!-- ======================================================================= -->

In order for `set-of-css()` to be inverse to `css-of-set()` (and vice versa),
each set within a hierarchy `H := (V,P)` must have a non-empty CSS.

Because of that requirement, each set must have one or more elements, which
none of its descendant sets is allowed to have. Consequently, such a
hierarchy must have at least as many elements in V as it has sets in P
(i.e. `(#P <= #V)`).

The CSS of a set can obviously be considered to represent data which is "unique"
to that set. That is, because there is always exactly one least significant set
which holds all the elements in that CSS. As such, the non-empty CSS of a set
can be understood to further characterize the corresponding set.

Note however, that the elements within the CSS of a set has an effect on the
relationship a set has with all the other sets in a hierarchy. After all, the
elements of a CSS are also elements of its ancestor sets (including the CSS's
parent set). That is, the elements within a CSS are not independent of the
relationships within a hierarchy (and vice versa).

* Recall that a root set `r in P` is the union of all of its descendant sets:
  i.e. `(#r == #V)`.

<!-- ======================================================================= -->
## strict hierarchy/forest

**CLARIFICATION**
A multiset (of sets) is said to be **a strict hierarchy (of sets)**,
if the following requirements are met:

0. `H := (V,P)`
1. The multiset is a simple hierarchy.
2. `(#css(s) == 1)` for each set `s in P`

Note that ...

* strict hierarchy => simple hierarchy
* The CSS of each set consists of a single element in `V`.
* Each set `s in P` can be identified by a single element in `V`.

**CLARIFICATION**
A multiset (of sets) is said to be **a strict forest (of hierarchies)**
or "a forest of strict hierarchies", if the following requirements are met:

0. `F := (V,P)`
1. The multiset is a simple forest.
2. Each hierarchy in `F` is a strict hierarchy.

Note that

* strict forest => simple forest
* All hierarchies within a forest are disjoint.
* Each set `s in P` can be identified by a single value `v in V`.
