
<!-- ======================================================================= -->
# TODO - sequences

you would if you could, but you won't because you can't
- https://en.wikipedia.org/wiki/List_of_unsolved_problems_in_mathematics

a set-based definition of sequences
- Kuratowski's definition
- based on the subset-of relationship

relationship with interval order
- intervals represent parts of an ordered set

sequences define trees - direct edges
- (f: Index -> Index)
- (a,b) = node a has parent b

sequences define trees - nested intervals
- (f: Index -> Length)
- (a,b) = node sequence of node a has length b
- node sequence of node a is a subsequence of the root's sequence

<!-- ======================================================================= -->
## interval order

**TODO** -
how does that order behave with regards to overlapping - incomparable?

**TODO** -
try different orders e.g. `(Li < Lj)`

**TODO** -
is one of those orders similar to the enter-/exit-order?

<!-- ======================================================================= -->
## subsequences

* mathematics / subsequences
* needs an introductory summary

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

* i.e. "just add in-comparable substrings"
* or - compare with suffix-order
