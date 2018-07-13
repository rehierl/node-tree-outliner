
<!-- ======================================================================= -->
# Hierarchy of sets => Unordered tree

The focus of this discussion is on how to create a node tree `T := (N,E)`
from a (simple/strict) hierarchy of nested sets `H := (V,P,G)`.

<!-- ======================================================================= -->
## Simple hierarchy => Unordered tree

```
a minimal hierarchy of nested sets             node tree
=========================================  =>  =================

|-A-------------------------------------|       A
| |-B-----------| |-E-| |-F-----------| |      =================
| | |-C-| |-D-| | | 3 | | |-G-| |-H-| | |       B      E   F
| | | 1 | | 2 | | |---| | | 4 | | 5 | | |      ======     ======
| | |---| |---| |       | |---| |---| | |       C  D       G  H
| |-------------|       |-------------| |
|---------------------------------------|
```

Note that labels (`A to F`) are not part of the hierarchy.
These labels only serve as a visual aid, intended to support discussions.

Note that the only information available, which can be used to reliably create
a node tree based on a given hierarchy, are the relationships the sets have
with each other. That is, because the definition of a hierarchy has no
characteristics with regards to the elements in `V`. Consequently, the node
tree to the right has one node per set `(s in P)`, not one node per element
`(v in V)` (i.e. 8 nodes, not 5).

**CLARIFICATION**
Any (simple) hierarchy of nested sets `H := (V,P,G)` defines
the structure of an unordered node tree `T := (N,E)`.

In order to create a node tree from a simple hierarchy,
the following steps must be executed:

1. Create a node `ni` for each set `si` (i.e. `(#N == #P)`) and
   associate each set with the node it represents (i.e. `(si -> ni)`).
2. If set `si` is the parent of set `sj`, then node `ni` must become
   the parent node of `nj` (i.e. `(si,sj) in G => (ni,nj) in E`).

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
* The resulting graph will be a directed graph. That is, because
  the relationship a set has with all the other sets is directed.
* A set is no ancestor to itself. That is, the resulting graph will
  have one root, no loops and no cycles (i.e. a node tree).

**Memory hook**
What counts is what relationship a set has with all the other sets. Other than
that, the elements the sets hold provide no further information that could be
relied upon.

<!-- ======================================================================= -->
## Required characteristics

**CLARIFICATION**
Because a simple hierarchy `H := (V,P,G)` has no characteristics that could
be used to consistently create the nodes of a tree `T := (N,E)`, a simple
hierarchy can only define the structure of a node tree. That is, such a
hierarchy does not contain the information needed to determine which node
a set represents.

In order to allow to make that determination, the missing information needs
to be embedded into the hierarchy. Because of that, a hierarchy needs to have
further characteristics, which are specified by the following requirements:

1. In order to embed the information which node a set represents, the sets
   need to contain the nodes in such a way that, based on any given set, the
   corresponding node can be identified. (=> `(N subset-of V)`).
2. In order for the resulting tree to have the same amount of nodes, the
   hierarchy must hold one set per node. (=> `(#P == #N)`).
3. A method must exist that allows to reliably determine which node a set
   represents. Because of that, the node a set represents must be a node
   of the corresponding set. (=> `node-of: P -> N`).

Note that these requirements will be referred to as "req-1" to "req-3".

**CLARIFICATION**
A strict hierarchy satisfies all of the above requirements,
if the CE each set holds is identical to the node it represents.

(req-1) `(V == N)` => `(N subset-of V)`.
That is, each set is guaranteed to have access to the node it represents.

(req-2) `(#CE(s) == 1)` => `(#P == #N)`.
That is, `(#P == #N)` is guaranteed to be true because
`(#P == #V)` is a consequence of `(#CE(s) == 1)` and `(V == N)`.

(req-3) `node-of := ce-of-set(s)`.
That is, in a strict hierarchy, each set has a non-empty CSS. And because
each CSS holds exactly one element, the node a set represents can be reliably
determined.

<!-- ======================================================================= -->
## Strict hierarchy => unordered tree

```
a strict hierarchy of nested sets              node tree
=========================================  =>  =================

|---------------------------------------|       1
| 1                                     |      =================
| |-------------| |---| |-------------| |       2      5   6       
| | 2           | | 5 | | 6           | |      ======     ======
| | |---| |---| | |---| | |---| |---| | |       3  4       7  8
| | | 3 | | 4 | |       | | 7 | | 8 | | |
| | |---| |---| |       | |---| |---| | |
| |-------------|       |-------------| |
|---------------------------------------|
```

Note that labels are no longer required, because the CE of each set allows
to uniquely identify each set. That is, the CE of each set can be understood
to represent a label for the corresponding set. Because of that, the visual
representation can be made more compact:

```
a strict hierarchy of nested sets              node tree
=========================================  =>  =================

|-1-------------------------------------|       1
| |-2-----------| |-5-| |-6-----------| |      =================
| | |-3-| |-4-| | |---| | |-7-| |-8-| | |       2      5   6
| | |---| |---| |       | |---| |---| | |      ======     ======
| |-------------|       |-------------| |       3  4       7  8
|---------------------------------------|
```

Note that the leaf sets only appear to be empty. The CE of each set is elevated
into the position of a label, but, in contrary to before, each CE remains to be
an element of the corresponding set.

**CLARIFICATION**
Any strict hierarchy of nested sets `H := (V,P,G)` defines
the structure and the nodes of an unordered node tree `T := (N,E)`.

In order to create a node tree from a strict hierarchy,
the following steps must be executed:

1. Determine the node `ni` each sets `si` represents (i.e. `ni = ce(si)`)
   and associate each set with its node (i.e. `(si -> ni)`).
2. If set `si` is the parent of set `sj`, then node `ni` must become
   the parent node of `nj` (i.e. `(si,sj) in G => (ni,nj) in E`).

Note however that the tree's structure is still defined by the relationship
a set has with all the other sets. In contrary to before, the elements within
those sets now hold the previously missing information, which is why the node
of each set can be uniquely determined.
