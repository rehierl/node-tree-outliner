
<!-- ======================================================================= -->
# Strict hierarchies

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
