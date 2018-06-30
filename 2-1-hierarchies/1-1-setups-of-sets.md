
* note the additional input (i.e. sets of sets)

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

**CLARIFICATION**
If set D is a subset of set B, set F a subset of set C, and if sets B and C
are disjoint from one another, then both subsets (D and F) are also disjoint
from one another.

Note that any two subsets of two disjoint sets are also disjoint from one
another. That is because otherwise, both subsets would not be subsets to
their respective super-sets.

**CLARIFICATION**
A set of sets is said to be **a (simple) setup (of sets)**.

* `S := (V,P)`.
* i.e. a two-element tuple of sets.
* `V` is a set of values/elements.
* `P` is a set of subsets over `V`.

Note that the expression "s in S" is a simplification which needs to be
understood as: s is a set of elements, and as such, an element of the
set of sets P of the corresponding setup (i.e. "s in P").

Note that `P` is a subset of `V`'s power-set (i.e. `P subset-of P(V)`).
That is, all elements in `P` are elements of `P(V)`.

Note that `V` is the union of all sets in `P` (i.e. `V` may be empty).
That is, a (simple) setup is completely defined by its set-of-sets `P`.

Note that the above example is a setup. The example would however no longer be
a setup, if number 3 would be removed from set C. That is, because this example
would then turn into a multiset of sets (i.e. sets C and F would be identical,
but still distinct sets - think in terms of distinct objects that represent the
same "thing").

<!-- ======================================================================= -->
## Consistent setup (of sets)

**CLARIFICATION**
A setup is said to be **a consistent setup (of sets)**,
if the following requirement is met:

* If two distinct sets have one or more elements in common,
  then one set is a subset of the other.

Note that this characteristic is understood as
"consistent with regards to the `subset-of` operator".

Note that an empty setup (i.e. an empty set of sets) is consistent. That is,
because it does not contain two distinct sets that could be in conflict with
the above requirement. The same reason allows to state that a setup, which
contains one set only, is consistent.

Note that this kind of consistency does not require that for each set (S1)
another set (S2) exists with which the first set (S1) has any elements in
common (e.g. set E, the empty set). That is, an extreme case of a consistent
setup would be, if all the sets within it are disjoint.

Note that, a consistent setup, which contains the empty set as an element,
is still consistent. That is, because the above requirement only needs to be
satisfied by sets that are not disjoint from one another. The empty set is
however disjoint to any set, and as such not required to be a subset of another
set (even though the empty set is a subset to any set). It can therefore not be
stated that "two sets within a consistent setup are either disjoint, ex-or one
set is a subset of the other". That is, because the empty set always fulfills
both aspects at the same time (i.e. a singularity).

**CLARIFICATION**
If two distinct sets in a consistent setup have one or more elements in common,
then one set is a strict subset of the other.

(1) Because the above requirement must be met, one set is a subset of the
other if both sets have one or more elements in common. (Assume, that set
t is a subset of set s).

(2) Each set within a consistent setup is unique.
That is, because a consistent setup is still a set of sets.

Because a consistent setup is still a set of sets, each set in such a setup is
unique. Because of that, and if two distinct sets in a consistent setup have one
or more elements in common, then one set is a subset of the other. After all,
that is the requirement of a consistent setup (i.e. it would not be a consistent
setup, if that would not be true).

, and, in addition to that, the super-set has at least one element
which the other set does not have (i.e. related => strictly related).
Consequently, a consistent setup is automatically also consistent with regards
to the `strict-subset-of` operator.

Note that this is a consequence of the above requirement.

**CLARIFICATION**
A setup is said to be **a strict setup (of sets)**,
if the following requirements are met:

0. `S := (V,P)`.
1. The setup is consistent.
2. The setup does not contain the empty set `{}`.

Note that ...

* Two distinct sets in a strict setup are either disjoint,
  ex-or one set is a strict subset of the other.
* that is: `(s disjoint-to t) <=> (s not-coupled-with t)`
* (#P < #P(V)) is always true

That is, because two non-empty sets either are disjoint from one another, ex-or
they have one or more elements in common. Furthermore, the "consistent setup"
requirement states that, if two non-empty sets have common elements, then one
set must be a subset of the other. Because of that, two distinct sets within
a strict setup are either disjoint, ex-or one set is a strict subset of the
other.
