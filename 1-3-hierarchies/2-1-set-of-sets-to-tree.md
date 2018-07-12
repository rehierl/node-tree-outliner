
<!-- ======================================================================= -->
# Hierarchy of sets => Unordered tree

The focus of this discussion is on how to create a node tree `T := (N,E)`
from a (simple) hierarchy of nested sets `H := (V,P)`.

<!-- ======================================================================= -->
## Simple hierarchy => Unordered tree

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
a node tree based on a given simple hierarchy, are the relationships the sets
have with each other. That is, because the definition of such a hierarchy has
no characteristics with regards to the elements in `V`. Consequently, the node
tree to the right has one node per set `(s in P)`, not one node per element
`(v in V)` (i.e. 8 nodes, not 5).

**CLARIFICATION**
Any (simple) hierarchy of nested sets `H := (V,P)` defines
the structure of an unordered node tree `T := (N,E)`.

In order to create a node tree from a given hierarchy,
the following steps must be executed:

1. Determine the relationship of each set by visiting each set
   and by connecting each set with its parent set.
2. Create a node `ni` for each set `si` (i.e. `(#N == #P)`) and
   associate each set with the node it represents (i.e. `(si -> ni)`).
3. If set `si` is the parent of set `sj`, then node `ni` must become
   the parent node of `nj` (i.e. `(si -> sj) => (ni -> nj)`).

Even though the relationship of a set (with all the other sets) is defined by
the elements a set holds, the creation of the nodes and the association of a
set with a node is unrelated to these elements. That is, because a hierarchy
does not reliably hold the information that would allow to determine which
node a set represents. In general, a hierarchy only states what relationship
a set has with all the other sets.

Note that ...

* `V` and `P` are not required to hold the same amount of elements.
* The addition of further elements to the above sets, without changing
  the relationship a set has with all the other sets, will not change
  the structure of the node tree.
* In general, the resulting graph will be a directed graph. That is,
  because the relationship a set has with all the other sets is directed.
* A set is no ancestor to itself. That is, the resulting graph will
  have one root, no loops and no cycles (i.e. a node tree).

**Memory hook**
What counts is what relationship a set has with all the other sets. Other than
that, the elements the sets hold provide no further information that could be
relied upon.

<!-- ======================================================================= -->
## Additional characteristics

Because a simple hierarchy `H := (V,P)` has no characteristics that could
be used in order to consistently create the nodes of a tree `T := (N,E)`,
a simple hierarchy can only describe the structure of a node tree. That is,
such a hierarchy does not contain the information needed to determine which
node a set represents.

In order to allow to make that determination, the missing information needs
to be embedded into the hierarchy. Because of that, a hierarchy needs to have
further characteristics. These are defined by the following requirements:

1. In order to embed the information which node a set represents, the sets
   need to contain the nodes in such a way that, based on any given set, the
   corresponding node can be identified.
   (=> `(N subset-of V)`).
2. In order for the resulting tree to have the same amount of nodes, the
   hierarchy must hold one set per node.
   (=> `(#P == #N)`).
3. The relationships of the sets in the hierarchy must accurately define the
   relationships of the nodes in the tree: If `si` represents `ni`, and if `s1`
   is the parent set of `s2`, then `n1` must become the parent node of `n2`.
   (=> `(si,sj) -> (ni,nj)`).
4. A method must exist that allows to reliably determine, based on any given
   set, which node that set represents.
   (=> `node-of: P -> N`).

Note that these requirements will be referred to as "req-1" to "req-4".

<!-- ======================================================================= -->
## TODO

Note that, if a hierarchy satisfies all of the above requirements, then that
hierarchy provides all the information required to create a complete node tree.
