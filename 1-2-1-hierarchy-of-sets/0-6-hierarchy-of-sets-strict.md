
<!-- ======================================================================= -->
# Strict/Normalized Hierarchy/Forest of sets

**CLARIFICATION**
A setup is said to be **a strict/normalized hierarchy (of nested sets)**,
if the following requirements are met:

0. `H := (V,P,G)`
1. The setup is a (simple) hierarchy.
2. `(#CE(s) == 1)` for any `(s in P)`

Note that ...

* strict hierarchy => simple hierarchy
* Each element in V is a CE: (CE(h) == V).
* Any set (s in P) has exactly one CE.
* Any set (s in P) can be identified its CE.
* Each CSS has exactly one CE: (#CSS(h) == #CE(h)).
* There are as many elements in V as there are elements in P: (#P == #V)

Note that the word "normalized" is with regards to:
"Each non-empty CSS holds one CE only".

**CLARIFICATION**
A setup is said to be **a strict/normalized forest (of hierarchies)**
or "a forest of strict hierarchies", if the following requirements are met:

0. `F := (V,P,G)`
1. The setup is a simple forest.
2. Each hierarchy in `F` is strict.

Note that

* strict forest => simple forest
* Any forest is a union of disjoint hierarchies.
* Any hierarchy in a forest can be identified by the CE of its root set.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Any non-empty CSS can be minimized to hold exactly one CE.

Additional CEs do not add substantial information to a hierarchy. They merely
increase the storage requirement of a hierarchy (hint: ancestor sets). That is,
instead of having multiple distinct CEs per set, each of which can be understood
to represent a bit of information that is unique to a set, a set should only
hold one reference to the combined information of that set.

**CLARIFICATION**
A simple hierarchy of sets may be referred to as **a minimal (simple)
hierarchy (of nested sets)**, if the CSS of each parent set is empty.

* `(#css(p) == 0)` for any `(p in PS)`

**CLARIFICATION**
A simple hierarchy may be referred to as **a normalized minimal (simple)
hierarchy (of nested sets)**, if it was created from a minimal hierarchy
by minimizing the characteristic subsets of its leaf sets.

* `(#css(p) == 0)` for any `(p in PS)`
* `(#css(l) == 1)` for any `(l in LS)`

Note that no element `(v in V)` can be removed from a normalized minimal
hierarchy without changing the relationship of one or more sets `(s in P)`,
or without violating the requirements of a simple hierarchy (e.g. empty sets).
