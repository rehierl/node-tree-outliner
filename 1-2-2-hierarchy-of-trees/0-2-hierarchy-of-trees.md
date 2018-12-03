
<!-- ======================================================================= -->
# (Simple) Hierarchy/Forest of trees

* the following definitions are analogous to those in ...
* (/see/ "core definitions" in "hierarchy of sets" /)

<!-- ======================================================================= -->
## core definitions

In regards to a strict setup, the following terms may be used:

* The **proper subtrees** of a tree
  are said to be the tree's **inner** trees.
* The trees to which a tree is an inner tree
  are said to be the tree's **outer** trees.

Note that, if the *simple subtree* operator would have been used in the above
two definitions, then any tree would be an inner and an outer tree to itself
(i.e. loops). However, since the *proper subtree* operator was used instead,
no tree is an inner and/or an outer tree to itself (i.e. no loops).

Note that two disjoint trees are not understood to be outside of each other,
not even if both trees have the same parent (i.e. siblings). That is because
neither of them is an inner tree of the other. Hence, "outside" and "not inside"
are not equivalent!

* Any outer tree of tree `t` is said to be an **ancestor** tree of `t`
  and as such **super-ordinate** to, or **more significant** than `t`.
* Any inner tree of tree `t` is said to be a **descendant** tree of `t`
  and as such **sub-ordinate** to, or **less significant** than `t`.

Note that a tree is no ancestor and no descendant to itself (i.e. no loops,
no cycles). Likewise, disjoint trees are neither ancestors nor descendants
to each other.

* A tree that has no ancestor
  (other than the universal graph),
  is said to be a **root** tree.
* The least significant ancestor of tree `t`
  is said to be the **parent** tree of `t`.
* The most significant ancestor of tree `t`
  is said to be the **root (tree) of** tree `t`.
* Tree `s` is said to be a **child** tree of `t`,
  if `t` is the parent of `s`.
* Two trees that have the same parent
  are said to be **siblings** to each other.
* A tree is said to be a **leaf** tree,
  if it has no descendant.

Note that none of the ancestors of a descendant are disjoint from one another.
They always have all the elements of the descendant in common. Consequently,
a strict setup does not allow its trees to have more than one parent. That is
because each non-root tree has exactly one most significant (i.e. its root)
and exactly one least significant ancestor (i.e. its parent).

* root tree -> ... -> parent tree -> child tree -> ... -> leaf tree

Note that an ancestor always has more elements than any of its descendants.
Likewise, a descendant always has fewer elements than any of its ancestors.
That is a consequence of the strict relationship between an ancestor and its
descendants. Consequently, each tree in a strict setup either has no parent
at all (e.g. a root) ex-or exactly one parent.

Note that a non-empty strict setup always has one or more root trees. That is,
because (1) a strict setup that only has a single tree has that tree as its
only root. Furthermore, (2) the addition of a new tree to a strict setup, in
such a way that the setup still satisfies all of the requirements, will (2.1)
add a new root (in case that tree is disjoint to any pre-existing tree), (2.2)
turn one or more existing root trees into non-root trees (in case these are
descendant to the new tree), or (2.3) add the new tree as a descendant to a
pre-existing root.

That is, if a new tree is added to a strict setup, the number of root trees
is increased by one (`#RS° = #RS+1`, cases 1 and 2.1), remains unchanged
(`#RS° = #RS`, cases 2.2 and 2.3) or is increased by a certain amount
(`#RS° = #RS-N` for `N in [0,#RS-1]`, case 2.2).

**SUMMARY**
A strict setup has the following properties:

* Any tree is a proper subtree to all of its ancestors.
* The ancestors of a tree are strictly related to each other.
* A tree either has ancestors ex-or none at all.
* A tree either has a parent ex-or the tree is a root.
* A tree that has a parent also has a root tree.
* A strict setup has no loops and no cycles.
* A non-empty strict setup has at least one root.

<!-- ======================================================================= -->
## remarks

**CLARIFICATION**
The sets of ancestor and descendant trees may be defined as follows:

* where `h` represents the corresponding hierarchy
* `A(t), A(t,h) := { a | (t proper-subtree-of a) for any (a in P) }`
* `D(t), D(t,h) := { d | (d proper-subtree-of t) for any (d in P) }`
* `AS(h) := { a | (a in A(t,h)) for any (t in P) }`
* `DS(h) := { d | (d in D(t,h)) for any (t in P) }`

Note that ...

* `PS := AS`, `CS := DS`
* i.e. each parent has a descendant and is itself an ancestor
* i.e. each child has an ancestor and is itself a descendant
* `RS := (PS \ CS)`, `LS := (CS \ PS)`
* i.e. each tree is either a root ex-or a child
* i.e. each tree is either a leaf ex-or a parent

**CLARIFICATION**
The following definitions may be used for clarification purposes:

* `(a in AS)` - the set of all ancestor trees
* `(d in DS)` - the set of all descendant trees
* `(r in RS)` - the set of all root trees
* `(p in PS)` - the set of all parent trees
* `(c in CS)` - the set of all child trees
* `(l in LS)` - the set of all leaf trees

Note that ...

* `(#RS, #PS, #CS and #LS) <= #P`
* `RS` and `LS` are both empty if and only if `(P == Ø)`
* i.e. a non-empty strict setup always has a root and a leaf
* `PS` and `CS` are both empty if `(RS == LS)`
* i.e. if each root is a leaf

**CLARIFICATION**
Each tree `(t in P)` in a strict setup `S := (U,P)`
has a unique **rooted path** `p := (t0,t1,...,tk)`
that can be used to reference `t`.

* `p(i) = t(i) = ti`
* `t(i) in P` and `(t(i) parent-tree-of t(i+1))`
* where `t0` represents the universal graph
* i.e. an ancestor graph to any tree possible
* any root is a child to the universal graph
* `(t1 in P)` is a root of `S`
* `(t == tk)` is true

Note that there are several, less formal notations possible that can be used
to denote the rooted path of a tree. The notation that will be used here is:

* `/...` is intended to be equivalent to `t0/...`
* `/t1` - the rooted path of root tree `t1`
* `/t1/.../tk` - the rooted path of tree `tk` that beings in its root tree `t1`

<!-- ======================================================================= -->
## (Simple) Hierarchy/Forest of trees

**CLARIFICATION**
Any strict setup `S := (U,P)` corresponds with a forest of trees.

* `G := (P,E)` where `(E subset-of P×P)`
* `P` is the setup's set of trees
* `E` is the setup's set of edges
* `e := (p1,p2)` such that `(e in E)` and `(p1 parent-of p2)`

**CLARIFICATION**
A setup is said to be **a (simple) hierarchy (of trees)**,
if the following requirements are met:

1. `H := (U,P)` is a strict setup
2. The setup has one and only one root set.

A simple hierarchy has the following properties:

* A hierarchy is not empty since it must have a root.
* No tree in a hierarchy is empty.
* A hierarchy has no loops and no cycles.
* A hierarchy has no overlapping trees (req-2).
* Two trees in a hierarchy are either disjoint ex-or related.
* Two distinct trees are either disjoint ex-or strictly related.
* Each tree either has no ex-or one parent.
* A hierarchy always has one or more leafs.
* Ancestors have more elements than their descendants.
* In a hierarchy, each tree has a unique rooted path (i.e. /root/to/tree).

**CLARIFICATION**
A setup is said to be **a (simple) forest (of hierarchies)**
or "a forest of simple hierarchies", if the following requirements are met:

1. `F := (U,P)` is a strict setup.
2. The setup has zero, one or more root trees.

Any strict setup is therefore a forest of hierarchies.
In contrary to that, not every strict setup is also a hierarchy.

* strict setup <=> a forest of hierarchies
* a hierarchy => a forest of hierarchies

Note that, in contrary to a hierarchy, a forest may be empty.
That is, a forest is not required to even have a root.

Note that a forest is not strictly "a set of sets of trees" (i.e. "a set of
hierarchies"). A forest is like a hierarchy, one "flat" set of trees. Because
of that, any operation defined on a set of trees (e.g. union, subset, etc.)
can be used in the context of forests.

Note that any two hierarchies in a forest of N hierarchies are disjoint. That
is because the forest would otherwise either have less than N hierarchies, or
it would not even be a strict setup. A forest therefore corresponds with a set
of disjoint hierarchies.

**CLARIFICATION**
The theoretical **set of all possible hierarchies (H)** and the theoretical
**set of all possible forests (F)** are defined as follows:

* `H := { h | "h is a hierarchy" }`
* `F := { f | "f is a forest of hierarchies" }`

Because of that, the expression `(h in H)` states that `h` is expected to be a
hierarchy. Likewise, `(f in F)` states that `f` is expected to be a forest of
hierarchies.

* `(H strict-subset-of F)`

Note that an empty setup is a forest, but not a hierarchy.

<!-- ======================================================================= -->
## remarks

Note that the definition of a hierarchy does not cover the process of forming
the trees it contains. It merely describes how these need to be related with
each other. That is, the subtrees of the hierarchy's root may be formed in any
number of ways (e.g. as generic or induced subtrees). Hence, further aspects
need to be taken into account in order to choose one method over the other.

**CLARIFICATION**
The root `(r in P)` of a hierarchy `H := (U,P)` is equal to `U`. Because
of that, a hierarchy's root is the largest tree (i.e. in terms of number
of elements) in `P`.

That is because (1) `U` is the union of all trees in `P` (i.e. `U := E(P)`),
and (2) any other tree `(t in P)` is a proper subtree to the root (since the
setup would otherwise have more than one root).

**CLARIFICATION**
Two hierarchy instances `H1` and `H2` are disjoint, if their roots are
disjoint. (The focus here is on two entities, i.e. two separate setups).

Note that, if root `r1` of `H1` is disjoint to `r2` of `H2`,
then any subtree `t1` of `r1` is disjoint to any subtree `t2` of `r2`.

**CLARIFICATION**
Any subset of a hierarchy `H := (U,P)` (i.e. more accurately any subset
of `P`), corresponds with a forest of hierarchies.

Note that the subset of a hierarchy will itself be a hierarchy,
if the hierarchy's root is included.
