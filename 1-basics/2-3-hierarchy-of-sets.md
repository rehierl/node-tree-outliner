
<!-- ======================================================================= -->
## TODOs

**TODO** -
define sub-hierarchy? -
as counterpart to sub-tree?

**TODO** -
go super-meta with forests? -
a forest is itself a set of elements -
a hierarchy of forests? -
"an outline of an outline"? -
an unordered/ordered forest?

**TODO** -
Given a set of elements `E` -
how many hierarchies are theoretically possible? -
what is the max possible number of sets in `P` (hint: powerset)? -
hint: resource management

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
has a unique rooted path `p := (s1,...,sk)` such that ...

* `p(i) = s(i) = si`
* `s(i) in P` and `(s(i) parent-set-of s(i+1))`
* `s1` is a root set, and `(s == sk)`

Note that there are several, less formal notations possible to denote the
rooted path of a set. The notation that will be used here is a follows:

* `/s1` - the rooted path of a root set `s1`.
* `/s1/.../sk` - the rooted path of set `sk` begins with root set `s1`.
* `#p` will be used to refer to the length of the rooted path `p`.

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
## Hierarchies and forests

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

**CLARIFICATION**
The **characteristic subset** of a set `s` in a forest `F`
is defined as follows:

* `CSS(s,F) := s - (union of all descendant sets of s)`
* `s in P`, where `F := (V,P)` is some forest.

The characteristic subset `CSS(s,F)` of set `s` in forest `F`, is a potentially
empty subset of `s`, such that none of the elements in `CSS(s,F)` is also an
element of any of the descendants of `s`.

In addition to that, `s` is the parent set of `CSS(s,F)`. Put differently, `s`
is the least significant set in `F` that contains all elements in `CSS(s,F)`.

Note that a CSS is only an implicit subset. That is, a forest does not contain
any CSS as an explicit element in its set of sets `P`.

```
|-A-------|   |-B-----------|
| 1 |-A-| |   | |-A-| |-B-| |
|   | 2 | |   | | 1 | | 2 | |
|   |---| |   | |---| |---| |
|---------|   |-------------|

CSS(/A)={1}, CSS(/A/A)={2}
CSS(/B)={}, CSS(/B/A)={1}, CSS(/B/B)={2}
```

Note that the CSS of a set is empty, if the corresponding set is the union of
its descendant sets (e.g. `CSS(/B)`). That is, a forest does not guarantee that
a CSS of its sets is non-empty.

**CLARIFICATION**
Given a non-empty CSS, and the corresponding forest of sets F, the parent set
of the CSS in F can be uniquely identified (hence the name):

1. Determine all the sets in F that contain all the elements of the given CSS.
2. Determine the least significant set of those sets.

Note that, in order to identify each set in `F`, the CSS of each set must
non-empty. That is, each set must contain one or more elements that none
of its descendant sets contain. Furthermore, and in order to identify each
set in `F` with a single element, the CSS of each set must contain exactly
one element.

**CLARIFICATION**
A multiset (of sets) is said to be **a strict hierarchy (of sets)**,
if the following requirements are met:

0. `H := (V,P)`
1. The multiset is a simple hierarchy.
2. `(#CSS(s,P) == 1)` for each set `s in P`

Note that ...

* strict hierarchy => simple hierarchy
* Each set `s in P` can be identified by a single value `v in V`.

**CLARIFICATION**
A multiset (of sets) is said to be **a strict forest (of hierarchies)**
or "a forest of strict hierarchies", if the following requirements are met:

0. `F := (V,P)`
1. The multiset is a simple forest.
2. Each hierarchy `h in P` is strict.

Note that

* strict forest => simple forest
* All hierarchies within a forest are disjoint.
* Each set `s in P` can be identified by a single value `v in V`.
