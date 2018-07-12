
<!-- ======================================================================= -->
# Strict hierarchies

**CLARIFICATION**
A setup is said to be **a strict hierarchy (of nested sets)**,
if the following requirements are met:

0. `H := (V,P)`
1. The setup is a (simple) hierarchy.
2. `(#css(s) == 1)` for any set `(s in P)`

Note that ...

* strict hierarchy => simple hierarchy
* Each CSS holds exactly one CE.
* (#V == #P == #CE(h) == #CSS(h))
* Any set (s in P) has exactly one CE.
* Any set (s in P) can be identified via one CE.

**CLARIFICATION**
A setup is said to be **a strict forest (of hierarchies)**
or "a forest of strict hierarchies", if the following requirements are met:

0. `F := (V,P)`
1. The setup is a simple forest.
2. Each hierarchy in `F` is strict.

Note that

* strict forest => simple forest
* All hierarchies within a forest are disjoint.
* Any hierarchy can be identified by the CE of its root set.
