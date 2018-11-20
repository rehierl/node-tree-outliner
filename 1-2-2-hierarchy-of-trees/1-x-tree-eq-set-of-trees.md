
**TODO** - the parent-tree of a subtree is such that the parent's
root is the parent node of the subtree's root.

**TODO** - the hierarchy's root is equal to the actual tree -
however, the focus is on expressing the initial tree using
different node entities and the relationships between them

<!-- ======================================================================= -->
# Unordered tree <=> Hierarchy of trees

```
node tree       hierarchy of subtrees          node tree
=========  <=>  ========================  <=>  =========

    1           {   1,     2,  3 , 4, 5}           1
 =======         =======      ===               =======
 2  3  5         2  3  5       4                2  3  5
   ===             ===                            ===
    4               4                              4
```

**CLARIFICATION**
The hierarchy of subtrees `H` created based upon an unordered tree `T := (N,E)`
corresponds with that tree. That is, `H` can be used to recreate `T`.
Because of that, this correspondence will be referred to as
the **(sub)tree-based correspondence** of a node tree.

<!-- ======================================================================= -->
## core concept

A sequence `s` can be expressed as a path graph `G`, if "predecessor-of" is
used as the graph's semantics (i.e. `sem(G) := predecessor-of`). By definition,
a path graph represents a tree `T` (i.e. "predecessor-of" directly corresponds
with "parent-of") as there is only one least element (i.e. root) and because
each element, except for the root, has one immediate predecessor.

```
sequence s        path graph G            tree T
                  (predecessor-of)        (parent-of)
==========        ================        ===========
(1,2,3)      =>   1 -> 2 -> 3        =>   1 -> 2 -> 3
```

In addition to that, a tree itself is an induced subtree (e.g. `X := T[1]`)
such that there is no border edge (i.e. `(BE(T,X) == Ø)`). In contrary to that,
any other distinct induced proper subtree is associated with a border edge
(e.g. `(BE(T,T[2]) == (1,2))`). Based upon these subtrees and the associated
border edges, a tree of subtrees `T°` can be defined, if a node is created for
each subtree `T[N]` and if each border edge is used to connect the corresponding
nodes.

Note that the border edges are in regards to the overall supertree `T`. Hence,
any proper subtree would be directly connected with the root `T[1]`. However,
the very same border edge can be retrieved given the subtree `T[n]` and any
other subtree `T[a]` such that `(a ancestor-of n)`.

* e.g. `(BE(T,T[3]) == BE(T[2],T[3]))`

Note that the border edges therefore need to be understood in regards to the
corresponding parent subtree (i.e. the least significant ancestor subtree).

Note that the "parent-of" semantics of the border edges in `T` (loosely)
corresponds with the "supertree-of" semantics in regards to the nodes of
the subtree nodes in `T°`. From a different perspective, the "ancestor-of"
semantics directly corresponds with the "supertree-of" semantics.

```
|-T[1]-|  supertree-of  |-T[2]-|  supertree-of  |-T[3]-|
|  1   |   parent-of    |  2   |   parent-of    |  3   |
|  |   |      ->        |  |   |      ->        |------|
|  2   |                |  3   |
|  |   |                |------|
|  3   |
|------|
```

Any tree can be transformed into such a tree of trees:

```
tree T             tree of trees T°
===========        ====================
1 -> 2 -> 3   =>   T[1] -> T[2] -> T[3]
```

Based on such a tree of trees, the source tree can be recreated by first
replacing each node `T[N]` with the graph difference `D[N] := T[N] \ T[C]`
where `(T[N] parent-of T[C])` (in general: for each child `T[C]` of `T[N]`).
After that, the resulting graph difference `D[N]` needs to be replaced by
the remaining root node (see: characteristic element).

Note that this process needs to begin at the root (i.e. replacing the subtrees
with nodes from top to down). Otherwise, the above graph difference could not
result in a single tree/node. However, different approaches (e.g. depth-first,
breadth-first, concurrency) are still possible. In contrary to this formal
operation, and provided that all invariants in the tree of trees are met, one
would simply implement this step by replacing each subtree with its root.

Note that `T[C]` is a proper induced subtree of `T[N]`. Because of that,
this operation is consistent with the restrictions described under the
definition of the difference operation on trees.

```
|-D[1]-|   parent-of   |-D[2]-|   parent-of   |-D[3]-|
|  1   |      ->       |  2   |      ->       |  3   |
|------|               |------|               |------|
```

Any such tree of trees can be used to recreate the source tree:

```
tree of trees T°            tree T
====================        ===========
T[1] -> T[2] -> T[3]   =>   1 -> 2 -> 3
```

**CLARIFICATION**
Any tree corresponds with **a tree of (sub)trees**:

```
tree T              tree of trees T°
===========         ====================
1 -> 2 -> 3   <=>   T[1] -> T[2] -> T[3]
```
