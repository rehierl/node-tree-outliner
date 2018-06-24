
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
Each set `s in P` within a strict setup `S := (E,P)`
has a unique rooted path `p := (s1,...,sk)` such that ...

* `si in P` and `(si parent-set-of s(i+1))`
* `s1` is a root set, and `(s == sk)`

Note that there are several, less formal notations possible to denote such a
rooted path. If needed, the following notation will be used:

* `/s1` - the rooted path of a root set `s1`.
* `/s1/.../sk` - the rooted path of set `sk`.
* `#p` will be used to refer to the length of such a path.

<!-- ======================================================================= -->
## Hierarchies and forests

```
|-A-------|   |-B-----------|
| 1 |-A-| |   | |-A-| |-B-| |
|   | 2 | |   | | 1 | | 2 | |
|   |---| |   | |---| |---| |
|---------|   |-------------|
```

* Root sets A and B both represent separate hierarchies.
* Inner set A/A is a strict subset of root set A.
* Inner sets B/A and B/B are both strict subsets of root set B.
* The union of all the sets represent a forest.

**CLARIFICATION**
A multiset (of sets) is said to be **a hierarchy (of sets)**,
if the following requirements are met:

1. The multiset is a non-empty strict setup.
2. The setup has exactly one root set.

Some of the properties of a hierarchy are:

* A hierarchy has no loops and no cycles.
* A hierarchy does not contain overlapping sets.
* Two distinct sets are either disjoint,
  ex-or one is a strict subset of the other.
* Each set either has no, ex-or exactly one parent set.
* Each set has a distinct rooted path (i.e. /root/to/set).
* Ancestor sets have more elements than their descendant sets.

Note that the formal definition of a hierarchy (`H := (E,P)`)
is equivalent to that of a simple setup (`S := (E,P)`).

**CLARIFICATION**
Two hierarchies are said to be disjoint, if their root sets are disjoint.

Note that the subsets of two disjoint sets are also disjoint.

**CLARIFICATION**
A multiset (of sets) is said to be **a forest (of hierarchies)**,
if the following requirements are met:

1. The multiset is a strict setup.
2. The setup has zero, one or more root sets.

Note that a strict setup is automatically a forest of hierarchies. That is, a
forest is not "a set of sets of sets" (i.e. "a set of hierarchies"). A forest
is like a hierarchy, a set of sets. Because of that, any operation defined on
a set of sets can be used in combination with forests.

* strict setup <=> a forest of hierarchies
* a hierarchy => a forest of hierarchies

Note that, in contrary to a hierarchy, a forest may be empty.
That is, a forest is not required to contain even a single root/hierarchy.

Note that any two hierarchies within a forest of N hierarchies are disjoint.
That is, because the forest would otherwise have less than N hierarchies,
or it would not even be a strict setup.

**CLARIFICATION**
Any subset of a hierarchy is a forest of hierarchies.

Note that, under certain circumstances (i.e. the hierarchy's root set
is included), the subset will itself be a hierarchy.

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
## Characteristic subset (CSS)
## Identifying subset (ISS)

* `ISS(s, H) := s - (union of all descendant sets of s)`
* `s in H`, where `H` is a simple or strict hierarchy

```
Hierarchy A: ISS(A,A)={}, ISS(B,A)={1}
Hierarchy B: ISS(B,B)={1}, ISS(A,B)={2}
Hierarchy C: ISS(C,C)={}, ISS(A,C)={1}, ISS(B,C)={2}
```

Note that the identifying subset of a set, taken from a strict hierarchy,
is mpty, if the corresponding set is the union of its descendant sets (e.g.
`ISS(C,C)`). That is, a strict hierarchy does not guarantee that all its
inner identifying subsets are non-empty.

**CLARIFICATION**
The identifying subset `ISS(s,H)` of set `s`, which is taken from a simple or
strict hierarchy `H`, is a potentially empty subset of `s`, such that none of
the elements in `ISS(s,H)` is also an element of any of the descendants of `s`.

In addition to that, `s` is the parent set of `ISS(s,H)`. Put differently,
`s` is the least significant set in `H` that still contains all the elements
in `ISS(s,H)`.

**CLARIFICATION**
Given a non-empty identifying subset ISS and the corresponding hierarchy of
sets H, the parent set of ISS in H can be uniquely identified. Hence the name.

1. Determine all the sets in H that contain ISS as a subset.
2. Determine the least significant set of those sets.

**CLARIFICATION**
In order to guarantee that each identifying subset within a hierarchy is
non-empty, every set within a hierarchy must have one or more elements that
none of its descendant sets have.
