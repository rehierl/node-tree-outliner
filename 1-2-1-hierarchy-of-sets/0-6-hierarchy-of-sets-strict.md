
<!-- ======================================================================= -->
# Strict/Normalized Hierarchy/Forest of sets

**CLARIFICATION**
A setup is said to be **a strict/normalized hierarchy (of sets)**,
if the following requirements are met:

0. `H := (V,P,G)`
1. The setup is a (simple) hierarchy.
2. `(#CE(s) == 1)` for any `(s in P)`

Note that ...

* A strict hierarchy is also a simple hierarchy.
* Each element in V is a CE since (CE(h) == V) is true.
* Any set (s in P) can be identified/retrieved by its CE.
* Each CSS has exactly one CE, i.e. (#CSS(h) == #CE(h)).
* The P has as many elements as V, i.e. (#P == #V).
* Each (v in V) is a CE.

Note that the term "normalized" is in regards to:
"Each CSS has exactly one CE".

**CLARIFICATION**
A setup is said to be **a strict/normalized forest (of hierarchies)**, or
"a forest of strict/normalized hierarchies", if the following requirements
are met:

0. `F := (V,P,G)`
1. The setup is a simple forest.
2. Each hierarchy in `F` is strict.

Note that

* A strict forest is also a simple forest.
* Any forest is a union of disjoint hierarchies.
* Any hierarchy in a forest can be identified/retrieved by the CE of its root.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Any non-empty CSS can be minimized to hold exactly one CE.

No additional CE adds substantial information to a hierarchy as those merely
increase the storage requirement of a hierarchy (hint: ancestor sets). That
is, instead of having multiple distinct CEs per set, each of which can be
understood to represent a bit of information that is unique to a set, a set
should only have one reference to the combined information (set of CEs) of
that set.

**CLARIFICATION**
A simple hierarchy of sets may be referred to as **a minimal (simple)
hierarchy (of sets)**, if the CSS of each parent set is empty.

* `(#css(p) == 0)` for any `(p in PS)`

**CLARIFICATION**
A simple hierarchy may be referred to as **a normalized minimal (simple)
hierarchy (of sets)**, if it was created from a minimal hierarchy by
minimizing the characteristic subsets of its leaf sets.

* `(#css(p) == 0)` for any `(p in PS)`
* `(#css(l) == 1)` for any `(l in LS)`

Note that no element `(v in V)` can be removed from a normalized minimal
hierarchy without changing the relationship of one or more sets `(s in P)`,
or without violating the requirements of a simple hierarchy (e.g. empty sets).
