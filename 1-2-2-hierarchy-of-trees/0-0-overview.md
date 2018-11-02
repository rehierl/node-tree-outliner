
<!-- ======================================================================= -->
# An overview of "hierarchy of trees"

A sequence `s` can be expressed as a path graph `G`, if "predecessor-of" is
used as the graph's semantics (i.e. `sem(G) := predecessor-of`). By definition,
a path graph represents a tree `T` (i.e. "predecessor-of" directly corresponds
with "parent-of") as there is only one least element and because each element,
except for the least element, has one immediate predecessor.

```
sequence s        path graph G            tree T
                  (predecessor-of)        (parent-of)
==========        ================        ===========
(1,2,3)      =>   1 -> 2 -> 3        =>   1 -> 2 -> 3
```

In addition to that, a tree itself is an induced subtree (e.g. `X := T[1]`)
such that there is no border edge (i.e. `(BE(T,X) == Ø)`). In contrary to
that, any other distinct induced proper subtree is associated with a border
edge (e.g. `(BE(T,T[2]) == (1,2))`). Based on these subtrees and the associated
border edges, a tree of subtrees `T°` can be defined, if each node represents
a subtree and if each border edge represents an edge in `T°`.

Note that the border edges are in regards to the overall supertree `T`.
Hence, any proper subtree would be directly connected with the root `T[1]`.
However, the very same border edge can be retrieved given the subtree
`T[x]` and any other subtree `T[a]` such that `(a ancestor-of x)` (e.g.
`(BE(T,T[3]) == BE(T[2],T[3]))`). Thus, the border edges need to be understood
in regards to the corresponding parent subtree (i.e. the least significant
ancestor subtree).

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

Each tree can be transformed into a tree of trees:

```
tree T             tree of trees T°
===========        ====================
1 -> 2 -> 3   =>   T[1] -> T[2] -> T[3]
```

Based on such a tree of trees, the initial tree can be recreated by first
replacing each node `T[X]` by the graph difference `D[X] := T[X] \ T[Y]`
where `(T[X] parent-of T[Y])` (in general: for each child `T[Y]` of `T[X]`).
After that, the resulting graph difference `D[X]` needs to be replaced by
the remaining root node (see: characteristic element).

Note that this process needs to begin at the root (i.e. replacing the subtrees
with nodes from top to down). Otherwise, the above graph difference could not
result in a single tree/node. However, different approaches (e.g. depth-first,
breadth-first, concurrency) are still possible. In contrary to this formal
operation, and provided all invariants in the tree of trees are met, one
would simply implement this step by replacing each subtree with its root.

Note that `T[Y]` is a proper induced subtree of `T[X]`. Because of that,
this operation is consistent with the restrictions described under the
definition of the difference operation on trees.

```
|-D[1]-|   parent-of   |-D[2]-|   parent-of   |-D[3]-|
|  1   |      ->       |  2   |      ->       |  3   |
|------|               |------|               |------|
```

Each such tree of trees can be used to recreate the initial tree:

```
tree of trees T°            tree T
====================        ===========
T[1] -> T[2] -> T[3]   =>   1 -> 2 -> 3
```

**CLARIFICATION**
Each tree corresponds with **a tree of (sub)trees**:

```
tree T              tree of trees T°
===========         ====================
1 -> 2 -> 3   <=>   T[1] -> T[2] -> T[3]
```