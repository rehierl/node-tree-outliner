
<!-- ======================================================================= -->
# TODO - order theory

what exactly is "order embedding"

* a "sub-order", a "merger", or what?
* i.e. develop a feeling for "it"

interval order

* how does that order behave with regards to overlapping intervals
* try different orders e.g. `(Li < Lj)`
* is one of those orders similar to the enter-/exit-order?

prefix order

* as a vertical perspective?
* i.e. rooted paths?

<!-- ======================================================================= -->
## poset -> dag

partial order

* reflexive, transitive, antisymmetric - i.e. directed
* (<=) non-strict poset, (<) strict/irreflexive poset
* every strict poset corresponds with a DAG - i.e. acyclic
* the transitive closure of a DAG is is a strict poset and a DAG

non-strict poset (P,<=) - cyclic

* assumed that (a,b) is an edge in a directed cycle (c)
* (1) c=(a,b,...) - i.e. (a <= b)
* (2) c=(a,b,...,a,b,...) - i.e. (b <= a)
* hint: (b <= a) due to cycle and transitivity
* i.e. (a <= b) and (b <= a) - i.e. (a = b)
* i.e. the cycle defines (a) and (b) to be equal
* => a non-strict poset could have cycles

strict poset (P,<) - acyclic

* strict => irreflexive => a-symmetric
* (<) does not support reflexive edges
* i.e. (a,a) would be in conflict with (<)
* (<) does not support cycles
* i.e. (b,a) would be in conflict with (a,b)
* i.e. (a < b) and (b < a) can not both be true
* => a strict poset can not have cycles

<!-- ======================================================================= -->
## prefix-order

```
prefix-order          tree-related order
-------------------   -----------------------------
0 1 2 3 4 5 6 7 8 9   0 1 2 3 4 5 6 7 8 9
=================     ========= =========
===============         =======   ===
=============             =====     =
===========                   =
=========
=======
=====
===
=
```

* add in-comparable substrings
* compare with suffix-order
