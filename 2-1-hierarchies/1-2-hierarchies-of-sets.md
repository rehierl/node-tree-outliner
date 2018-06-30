
<!-- ======================================================================= -->
# TODOs

**TODO** -
define sub-hierarchy? -
as counterpart to sub-tree?

**TODO** -
go meta with forests? -
a forest is itself a set of elements -
a hierarchy of forests? -
"an outline of an outline"? -
an unordered/ordered forest?

**TODO** -
given a set of elements E -
how many hierarchies are theoretically possible? -
what is the max possible number of sets in P (hint: powerset)? -
with regards to: resource management, allocation of resources

<!-- ======================================================================= -->
# Hierarchy/Forest of sets

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

With regards to a strict setup, the following references may be used:

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
that, any non-empty set is an ancestor set to the empty set. The empty set
is therefore the only set that may have disjoint ancestors. Consequently, a
strict setup must not contain the empty set. From this point forwards, all
sets are considered to be non-empty.

* A set, that has no ancestor set (other than the universal set),
  is said to be a **root set**.
* The least significant ancestor set of set S
  is said to be the **parent set** of S.
* (The most significant ancestor set of set S
  is said to be the **root set of** S).
* Set S1 is said to be a **child set**
  of set S2, if S2 is the parent set of S1.
* Two sets which have the same parent set
  are said to be **siblings**.
* Set S1 is said to be a **leaf set**
  if there is no set descendant to S1.

Note that none of the ancestors of a descendant set are disjoint from one
another. They always have at least all the elements of the descendant set
in common. Consequently, a strict setup does not allow its sets to have more
than one parent set. That is, each non-root set always has exactly one least
significant ancestor and therefore exactly one parent set. Likewise, each
non-root set always has exactly one root set as an ancestor.

Note that a set is not a parent set to itself (no loops). That is, because a
set is not an ancestor to itself. Consequently, each set within a strict setup
either has no parent set (e.g. a root set), ex-or exactly one parent set.

Note that an ancestor set always has more elements than any of its descendant
sets. Likewise, a descendant set always has fewer elements than any of its
ancestor sets. That is a direct consequence of the `strict-subset-of` operator.

Note that a set can not be an ancestor set to itself (no cycles). That is,
because a set can not be a subset to one of its strict subsets. Likewise,
a set can not be a descendant set to itself. That is, because a set can not
be a strict subset to itself.

Note that a non-empty strict setup always has one or more root sets. That is,
because (1) a strict setup that only contains a single set has that set as its
only root set. That is, because in such a case, the setup does not have a set
which could be an ancestor to that set. Furthermore, (2) the addition of a set
to a strict setup, in such a way that the setup remains to be strict, will
either add a new root set (in case that new set is disjoint to any pre-existing
set), ex-or a new descendant set (i.e. a non-root set) to one or more existing
sets.

**CLARIFICATION**
A strict setup has the following properties:

* A set is a strict subset to all of its ancestors.
* The ancestors of a set are not disjoint from one another.
* A set either has one or more ancestors, ex-or none at all.
* A set either has a parent set, ex-or the set is a root set.
* A strict setup has no loops and no cycles.
* A non-empty strict setup always has one or more root sets.
* A set that has a parent set also has one root set as an ancestor.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The following definitions may be used to clarify discussions:

* RS := all sets that have no ancestor set - set of root sets
* LS := all sets that have no descendant set - set of leaf sets
* PS := all sets that are parent to some child set
* CS := all sets that are child to some parent set

Note that ...

* RS, PS, CS and LS all are subsets of P
* RS and LS are only empty if `(#P == 0)` is true
* i.e. a non-empty strict setup always has a root and a leaf
* (RS & CS) and (PS & LS) are both always empty
* i.e. RS and CS are disjoint, as are PS and LS
* i.e. a root isn't a child, and a parent isn't a leaf
* ((RS + CS) == P == (PS + LS)) is true
* i.e. each set is either a root ex-or a child
* i.e. each set is either a parent ex-or a leaf
* i.e. RS and CS are "inverse" to each other, as are PS and LS
* PS and CS are both empty if `(#RS == #P)` is true

**CLARIFICATION**
Each set `s in P` in a strict setup `S := (V,P)`
has a unique **rooted path** `p := (s0,s1,...,sk)` such that ...

* `p(i) = s(i) = si`
* `s(i) in P` and `(s(i) parent-set-of s(i+1))`
* `s0` is the universal set
* `s0` is a virtual ancestor set of all possible sets
* any root set is a child set of the universal set
* `s1 in P` is a root set, and `(s == sk)`

Note that there are several, less formal notations possible to denote the
rooted path of a set. The notation that will be used below is a follows:

* note that `/...` is meant to be equivalent to `s0/...`
* `/s1` - the rooted path of a root set `s1`.
* `/s1/.../sk` - the rooted path of set `sk` begins with root set `s1`.
* `#p` refers to the length of the rooted path `p`.

Note that each element within such a rooted path is a set of possibly
infinitely many elements.

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
## (simple) Hierarchy/Forest of sets

**CLARIFICATION**
A setup is said to be **a (simple) hierarchy (of sets)**,
if the following requirements are met:

0. `H := (V,P)`
1. The setup is strict.
2. The setup has exactly one root set.

Some of the properties of a hierarchy are:

* A hierarchy is not empty (one root set).
* A hierarchy has no loops and no cycles.
* A hierarchy has no sets that overlap each other.
* Two distinct sets are either disjoint,
  ex-or one is a strict subset of the other.
* Each set either has no, ex-or exactly one parent set.
* A hierarchy always has one or more leaf sets.
* Ancestor sets have more elements than their descendant sets.
* Each set has a distinct rooted path (i.e. /root/to/set).

**CLARIFICATION**
A setup is said to be **a (simple) forest (of hierarchies)**
or "a forest of simple hierarchies", if the following requirements are met:

0. `F := (V,P)`
1. The setup is a strict.
2. The setup has zero, one or more root sets.

Note that, in contrary to a hierarchy, a forest may be empty.
That is, a forest is not required to contain even a single root set.

* strict setup <=> a forest of hierarchies
* a hierarchy => a forest of hierarchies

Note that any strict setup is a forest of hierarchies. That is, a forest is not
strictly "a set of sets of sets" (i.e. "a set of hierarchies"). A forest is like
a hierarchy, a single set of sets. Because of that, any operation defined on a
set of sets can be used in combination with forests.

Note that any two hierarchies in a forest of N hierarchies are disjoint. That
is, because the forest would otherwise either have less than N hierarchies, or
it would not even be a strict setup. From a loose perspective, a forest is a
set of disjoint hierarchies.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Two hierarchies are disjoint, if their root sets are disjoint.

Note that, if root set `r1` is disjoint from `r2`,
then any subset `s1` of `r1` is disjoint to any subset `s2` of `r2`.

**CLARIFICATION**
Any subset of a hierarchy is a forest of hierarchies.

Note that, under certain circumstances (i.e. the hierarchy's root set
is included), the subset will itself be a hierarchy.

<!-- ======================================================================= -->
## strict Hierarchy/Forest of sets

**CLARIFICATION**
A setup is said to be **a strict hierarchy (of sets)**,
if the following requirements are met:

0. `H := (V,P)`
1. The setup is a (simple) hierarchy.
2. `(#css(s) == 1)` for each set `s in P`

Note that ...

* strict hierarchy => simple hierarchy
* The characteristic subset of each set `css(s)`
  consists of a single element in `V`.
* Each set `s in P` can be identified by a single element in `V`.

**CLARIFICATION**
A setup is said to be **a strict forest (of hierarchies)**
or "a forest of strict hierarchies", if the following requirements are met:

0. `F := (V,P)`
1. The setup is a simple forest.
2. Each hierarchy in `F` is strict.

Note that

* strict forest => simple forest
* All hierarchies within a forest are disjoint.
* Each set `s in P` can be identified by a single value `v in V`.
