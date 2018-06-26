
<!-- ======================================================================= -->
# Creating an unordered tree from a hierarchy of sets

```
a hierarchy of sets                            node tree
=========================================  =>  =================

|-A-------------------------------------|       A
| |-B-----------| |-H-| |-C-----------| |      =================
| | |-D-| |-E-| | | 3 | | |-I-| |-F-| | |       B      H   C
| | | 1 | | 2 | | |---| | | 4 | | 5 | | |      ======     ======
| | |---| |---| |       | |---| |---| | |       D  E       I  F
| |-------------|       |-------------| |
|---------------------------------------|
```

Note that labels (`A to F`) are not part of the hierarchy.
These labels only serve as a visual aid, intended to support discussions.

Note that the only information available, which can be used to reliably create
a node tree based on a given hierarchy, are the relationships the sets have
with each other. That is, because the definition of simple hierarchies have no
characteristics with regards to the values/elements in `V`. Consequently, the
node tree to the right has one node per set `s in P`, not one node per value
`v in V` (i.e. 8 nodes, not 5).

**CLARIFICATION**
Any (simple) hierarchy of sets `H := (V,P)` defines
the structure of a rooted (unordered) tree `T := (N,E)`.

In order to create a node tree based on a given hierarchy of sets,
the following steps must be executed:

0. (Set `si` is understood to represent node `ni`).
1. Visit and connect each set with its parent set.
2. A node `ni` must be created for each set `si` (i.e. `(#P == #N)`),
   and each set must be associated with the node it represents.
3. If set `si` is the parent of set `sj`,
   then node `ni` must become the parent of node `nj`.

Even though the relationship of a set (with all the other sets) is defined by
the values/elements the sets hold, the creation of the nodes and the association
of a set with a node is unrelated to these elements. That is, because a simple
hierarchy does not provide the information to reliably determine what the node
is that a set represents. A simple hierarchy only states what relationship some
node has with all the other nodes.

Note that ...

* `V` and `P` are not required to hold the same amount of elements.
* The addition of further elements to the above sets, without changing
  the relationship a set has with all the other sets, will not change
  the structure of the node tree.
* A set is no ancestor to itself. That is, the resulting graph has one
  root, no loops and no cycles (i.e. a node tree).

**Memory hook**
What counts is what relationship a set has with all the other sets. Other than
that, the elements within these sets provide no further information that could
be relied upon.

<!-- ======================================================================= -->
## Additional characteristics

Because a simple hierarchy `H := (V,P)` has no characteristics that could
be used in order to consistently create the nodes of a tree `T := (N,E)`, a
simple hierarchy can only describe the structure of a node tree. That is, a
simple hierarchy does not contain the information needed to determine which
node a set represents.

The information which node a set represents therefore needs to be embedded into
a hierarchy in order for it to describe a complete node tree. Because of that,
a hierarchy needs to have further characteristics. These are defined by the
following requirements, which must all be satisfied:

1. In order to embed the information which node a set represents,
   each element in `V` must represent a node: `(V == N)`.
2. In order for the resulting tree to have the same amount of nodes,
   the hierarchy must have one set per node: `(#P == #V)`.
3. The relationships of the sets in the hierarchy must accurately define the
   relationships of the nodes in the tree: If set `si` represents node `ni`,
   and if set `s1` is the parent set of `s2`, then node `n1` must become the
   parent node of `n2`.
4. A method must exist which allows to determine, based on a given set, which
   node that set represents. This operation is understood to be defined by the
   following function/operation: `node-of: P -> V`. That is, `node-of(s)` will
   return the node `n` that set `s` represents.

`node-of(s) := one-value-in(css-of-set(s))`

Note that these requirements will be referred to as "req-1" to "req-4".

Note that, if a hierarchy satisfies all of the above requirements, then that
hierarchy provides all the information required to create a complete node tree.

**CLARIFICATION**
A hierarchy that completely defines a node tree is strict.
