
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
## set of sequences

trees, orders
- define "(strict) subtree", "(strict) suborder"?
- compare node order of a subtree -vs- node order of a tree

drawing borders around subtrees
- a hierarchy of subtrees based on the subtree-of operator
- translates directly into a hierarchy of sets of nodes

ordered sequences
- a tree's node order -vs- the traversal's node/visit order
- the traversal's visit order -vs- the traversal's enter order
- proof that: node order <-> visit order <-> enter order
- the issue: a node is a single unit - i.e. enter vs. exit

properties of (s in S)
- all sequences have the same order
- define "suborder" - order embedding?

define
- set-based operators for ordered sequences?

<!-- ======================================================================= -->
## more than "sequences"

* `s = [ e1, ..., eN ]` for `(s in ×Ti)`
* `(f: (×Ti,Index) -> Element)`
* note - closely related to orders
* note - distinct elements may hold the same value
* i.e. a sequence is a group of elements paired with an order-relation
* sequences represent ordered multisets - nope
* sequences may represent ordered sets

<!-- ======================================================================= -->
## interval order

**TODO** -
how does that order behave with regards to overlapping - incomparable?

**TODO** -
try different orders e.g. `(Li < Lj)`

**TODO** -
is one of those orders similar to the enter-/exit-order?

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
