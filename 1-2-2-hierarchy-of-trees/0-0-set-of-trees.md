
<!-- ======================================================================= -->
# Set of sub-trees

* (/see/ "relationships" in "graph theory" /)

<!-- ======================================================================= -->
## relationships

**TODO** - Note the border graph between A and D
(and the border graph between A and D) ...

```
multiset-of-trees = <
A: 1 , B: 4 , C: 4 , D: 2 , E: 2, F: 3
  ===    ===    ===    ===
  2 3     2      2      5
>
```

Elements B and C represent trees that are equal. The relationship between both
trees is therefore neither "disjoint" nor "strictly related". Because of that,
the relationship can only be described as being "equal", which is why there
is no **distinct order** (i.e. inside vs. outside, aka. subtree vs. supertree)
between the two.

Consequently, and in order to avoid these kind of circumstances, each element
must represent a unique tree. Put differently, all trees **must be distinct**
from one another, which is why a set-of-trees, rather than a multiset-of-trees
is required.

Similar to that, and even though trees A and B are distinct from one another,
there is no distinct relationship between the two. That is, both trees have
nodes in common (they would otherwise be disjoint) and nodes that the other
tree does not have (they would otherwise be related). As such, both trees
**overlap** each other and therefore represent another type of relationship
between two trees.

Likewise, trees A and D overlap each other. However, the root of D is a node
in A, which is why the union of both trees would result in another tree. As
before, there is no clear relationship between the two.

Note that the set of nodes of trees A and B overlap each other. This obviously
also applies to trees A and D. Hence if the sets of these trees would have to
be visualized as a set of nested sets, then the borders of those sets would
cross each other. Because of that, overlapping trees may themselves be seen
to cross each other.

<!-- ======================================================================= -->
## disjoint, coupled, overlap

**CLARIFICATION**
Trees `S := (M,F)` and `T := (N,E)` are **disjoint** (from one another),
if the intersection graph between the two is equal to the empty graph.

* `(S disjoint-to T) := ((S & T) == Ø)`
* `(S disjoint-to T) <-> (T disjoint-to S)`

Recall that two trees, which have an edge in common, must also have both
of the endpoints of that edge in common. Two trees are therefore disjoint,
if (and only if) their sets of nodes are disjoint.

* `(F coupled-with E) -> (M coupled-with N)`
* `(M disjoint-to N) -> (F disjoint-to E)`
* `(S disjoint-to T) <-> (M disjoint-to N)`

**CLARIFICATION**
Trees `S := (M,F)` and `T := (N,E)` are **coupled** (with each other),
if the intersection graph between the two is un-equal to the empty graph.

* `(S coupled-with T) := ((S & T) != Ø)`
* `(S coupled-with T) <-> (T coupled-with S)`

Note that "disjoint-to" and "coupled-with" are exclusive to each other.
That is, two trees are either disjoint ex-or coupled with each other.
Because of that, "disjoint-to" is converse/antonymous to "coupled-with".

* `(S disjoint-to W) ex-or (S coupled-with W)`
* `(disjoint ex-or coupled) <=> (disjoint <-> !coupled)`

Note that the common nodes/edges can be understood to act as a "link" between
two trees. These links can be understood to bind both trees together, which
is why those trees can be said to be "connected" or "coupled" with each other
via some "point of contact".

**CLARIFICATION**
Two trees `S := (M,F)` and `T := (N,E)` are said to **overlap** (each other),
if the intersection between the two is non-empty, and if each tree has node
that is not a node in the other tree. Put differently, both trees must be
coupled with (aka. intersect) each other and no tree is a subtree of the other.

* `(S overlaps T) := (I != Ø) and (I != S) and (I != T)` where `I := (S & T)`
* `(S overlaps T) := (S coupled-with T) and (S unrelated-to T)`
* `(S overlaps T) <-> (T overlaps S)`

<!-- ======================================================================= -->
## subtree, strict/proper subtree

**CLARIFICATION**
Tree `S := (M,F)` is a **(simple) subtree of** tree `T := (N,E)`,
if all the nodes/edges in `S` are nodes/edges in `T`.

* `(S subtree-of T) := (S subgraph-of T)`
* note - `S` and `T` are both required to be trees
* `(S subtree-of T) := (M subset-of N) and (F subset-of E)`
* `(F subset-of E) -> (M subset-of N)` (but not necessarily vice versa)

Note that, since a tree can not have any disconnected nodes, 

Note that whether or not `S` is an induced subtree of `T` is not relevant at
this point. However, at some later point and based upon further considerations,
a subtree may still be required to be an induced subtree.

**CLARIFICATION**
Tree `S := (M,F)` is a **strict/proper subtree of** tree `T := (N,E)`,
if `S` is a (simple) subtree of and unequal to `T`.

* `(S proper-subtree-of T) := (S subtree-of T) and (S != T)`
* `(S proper-subtree-of T) -> (S subtree-of T) and (T no-subtree-of S)`
* `(S proper-subtree-of T) -> (#M < #N)`

<!-- ======================================================================= -->
## related, strictly/properly related

**CLARIFICATION**
Tree `S := (M,F)` is **related to** tree `T := (N,E)`,
if one tree is a (simple) subtree of the other.

* `(S related-to T) := (S subtree-of T) or (T subtree-of S)`
* `(S related-to T) <-> (T related-to S)`

**CLARIFICATION**
Tree `S := (M,F)` is **unrelated to** tree `T := (N,E)`,
if none is a (simple) subtree of the other.

* `(S unrelated-to T) := not (S related-to T)`
* `(S unrelated-to T) <-> (T unrelated-to S)`

**CLARIFICATION**
Tree `S := (M,F)` is **strictly/properly related to** tree `T := (N,E)`,
if both trees are related and distinct to each other.

* `(S strictly-related-to T) := (S related-to T) and (S != T)`
* `(S strictly-related-to T) <-> (T strictly-related-to S)`

Note that the definition of the "related-to" terms is intended to shift
ones focus away from the elements the trees contain. That is, the focus#
is shifted towards the relationship between two trees.

<!-- ======================================================================= -->
## derived statements

Recall that any tree is unequal to the empty graph since each tree must
by definition have at least have a root node.
