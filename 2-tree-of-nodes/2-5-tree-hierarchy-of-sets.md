
<!-- ======================================================================= -->
# A set-based perspective

Note that the following discussion is based upon rooted un-ordered trees.

```
tag soup          node tree      (simplified)      set of nodes
============  =>  =========  =>  ============  =>  =============

<1>                   1               1            |-S0--------|
  2                   |           =========        |     1     |
  <3> 4 </3>      =========       2   3   5        | ========= |
  5               |   |   |          ===           | 2   3   5 |
</1>              2   3   5           4            |    ===    |
                      |                            |     4     |
                      4                            |-----------|
```

Note the outer box S0, which contains all the nodes of the tree.
It contains the tree's root node and all of its descendants.

**CLARIFICATION**
A rooted tree `T := (N,E)` can be understood to represent its set of nodes N.

Note that the following discussion focuses on the tree's set of nodes and on
subsets of that set. The set of edges E is therefore only taken into account
as a formal basis that defines these sets via "all the nodes that are connected
in a certain way". As such, the following (sub-)sets are understood to be
identified and defined by a node that acts as the starting point of a formal
definition.

<!-- ======================================================================= -->
## The root's inner/outer set of nodes

```
                 inner and outer sets
set of nodes     of root node 1
=============    ====================

|-S0--------|    |-S1--------------|
|     1     |    |        1        |
| ========= |    | |-S2----------| |
| 2   3   5 |    | | 2    3    5 | |
|    ===    |    | |     ===     | |
|     4     |    | |      4      | |
|-----------|    | |-------------| |
                 |-----------------|
```

Each tree has its root as its most significant node.

* Root `1` can be understood to define two sets of nodes.
* The root's inner set S2 only contains the root's descendants.
* The root's outer set S1 combines its inner set S2 with the root itself.
* A tree's set of nodes is identical to the outer set of its root.

Note that the definitions of the inner and outer sets are based upon mere
observations. They do not define anything new other than names/references
for these particular sets of nodes. Both (sub-)sets exist either way.
(Not as separate entities, but as a part of the tree's set of nodes).

<!-- ======================================================================= -->
## The inner/outer set of a node

Each node within a tree can be understood to represent the root of a subtree.
Any node can therefore be understood to define two sets of nodes: (1) The
inner set S2 of a node contains only the descendants of that node, and (2)
the outer set S1 of a node combines the node's inner set with the node itself.

* `S1 = (node union S2)`
* An outer set always contains its defining node (i.e. never empty).
* An inner set is empty if its defining node is a leaf.
* An empty tree has no node and consequently no outer and no inner set.

The relationship between both sets:

* As a strict subset, S2 is embedded into S1.
* S1 is super-ordinate to S2 and S2 sub-ordinate to S1.
* S1 is the parent (i.e. an ancestor) set of S2.
* S2 is the only child (i.e. a descendant) set of S1.

Note that each set can be transformed into the other,
if the defining node is added to (or removed from) the other set.

**CLARIFICATION**
Each node can be said to contain itself and its descendants.

Other ways to express that statement would be: (1) node `n1` contains node
`n2`, if `n2` is a node of the subtree that has `n1` as its root. Or (2)
`n1`'s outer set contains `n2`.

**CLARIFICATION**
Node `n1` is said to be **disjoint** from `n2`,
if the outer sets of both nodes have no node in common.

* The subtrees of both nodes have no node in common.
* `n1` does not contain `n2`, and `n2` does not contain `n1`.

Note that, if two nodes are disjoint,
then none of those is an ancestor of the other.

<!-- ======================================================================= -->
## Relationship between the sets of different nodes

```
node tree          set of outer sets
=============  =>  =========================

      1            |-A---------------------|
=============      | 1                     |
 2    3    5       | |-B-| |-C-----| |-E-| |
     ===           | | 2 | | 3     | | 5 | |
      4            | |---| | |-D-| | |---| |
                   |       | | 4 | |       |
                   |       | |---| |       |
                   |       |-------|       |
                   |-----------------------|
```

* The outer set of a child node
  is a subset of the inner set of its parent node.
* The outer set of a child node
  is sub-ordinate to the inner set of its parent node.

Note that, even though both sets have different defining nodes, the outer set 
of a child is identical to the inner set of its parent, if the parent has no
other child.

* Both sets of a node are subsets to any set of any of the node's ancestors.
* None of those sets contains a node that an ancestor set does not contain.
* The inner set of a node is the union of the outer sets of its child nodes.

The above statements should be fairly obvious because any descendant of a node
is also a descendant of the node's ancestors and, as such, also an element of
any set of any of the node's ancestors.

<!-- ======================================================================= -->
### Outer sets of different nodes

**CLARIFICATION**
The outer sets of two distinct nodes are either disjoint from one another,
ex-or one outer set is a strict subset of the other.

(0) If node `n1` is an ancestor of `n2`, then the outer set of `n1` has `n1`
as an element, but the outer set of `n2` does not. The outer set of an ancestor
always has more elements than the outer set of a descendant. (Note that the
outer set of a leaf node is not empty).

(1) If node `n1` is an ancestor of `n2`, then any descendant of `n2` is also a
descendant of `n1`. The outer set of `n2` is therefore a strict subset of the
outer set of `n1`. That is, the outer set of `n2` does not have any node that
is not also an element of the outer set of `n1`. The outer set of a descendant
therefore never overlaps the outer set of an ancestor.

(2) If node `n1` is not an ancestor of `n2`, then the outer sets of both nodes
have no nodes in common: the outer sets of both nodes are disjoint.

**CLARIFICATION**
The outer set of a node is unique to a node.
No other node has the exact same outer set.

If the outer sets of two nodes are disjoint, then the outer sets of both nodes
have no nodes in common. That is, if one node is not an ancestor of the other,
then the outer sets of both nodes are different.

If node `n1` is an ancestor of `n2`, then `n1`'s outer set contains `n1`, but
`n2`'s outer set does not. The outer sets of both nodes are therefore different.

<!-- ======================================================================= -->
### Inner sets of different nodes

Note that the arguments needed to proof the following statements are largely
the same as those needed to proof the statements with regards to outer sets.

Note that the inner sets of leaf nodes are empty and that: (a) an empty sets
is disjoint from any other set - (b) an empty set is a subset to any other
set - (c) an empty set is a strict subset to any non-empty set.

**CLARIFICATION**
The non-empty inner sets of two distinct nodes are either disjoint,
ex-or one inner set is a strict subset of the other.

(0) If node `n1` is an ancestor of `n2`, then the inner set of `n1` has
`n2` as an element, but the inner set of `n2` does not. The inner set of an
ancestor always has more elements than the inner set of a descendant. (Note
that the inner set of a leaf node is empty).

(1) If node `n1` is an ancestor of `n2`, then the inner set of `n2` is a strict
subset of the inner set of `n1`. (Note that this is true, even if `n2` is a leaf
node: `n1` has a non-empty inner set, `n2` has an empty inner set).

(2) If node `n1` is not an ancestor of `n2`, then the inner sets of both nodes
have no nodes in common: the inner sets of both nodes are disjoint. (Note that
this is true, even if `n1` and/or `n2` are leaf nodes: an empty inner set is
disjoint from any other set).

Note that the "ex-or" part of the above statement is therefore not true,
if one node is an ancestor of a leaf.

**CLARIFICATION**
The non-empty inner set of a node is unique to a node.
No other node has the exact same non-empty inner set.

If the inner sets of two non-leaf nodes are disjoint, then the inner sets of
both nodes have no nodes in common. That is, if one node is not an ancestor of
the other, then the inner sets of both nodes are different.

If node `n1` is an ancestor of `n2`, then `n1`'s inner set contains `n2`, but
`n2`'s inner set does not. The inner sets of both nodes are different.

**Memory hook**
Take a piece of paper and use it to draw a rooted node tree. After that, draw
a border around that node tree. Then, draw a border around each subtree. When
done, the set of borders represents the tree's hierarchy of outer sets.

<!-- ======================================================================= -->
## Node trees as hierarchies of sets

Assumed that a tree is non-empty (i.e. has a root) ...

* H1 - The set of sets that only contains
       the outer sets of all the nodes of a tree.
* H2 - The set of set that only contains
       the inner sets of all the nodes of a tree.
* H2' - `H2' := (H2 - {})`
* H0  - `H0 := (H1 union H2)`
* H0' - `H0' := (H1 union H2')`

```
          \  Hx  |   |   |   |   |
construct  \     | 1 | 2 | 2'| 0 | 0'
-----------------|---|---|---|---|---
consistent setup | + | + | + | + | + 
-----------------|---|---|---|---|---
hierarchy        | + | - | - | - | + 
```

* H0, H1 and H2 all are consistent setups.
* H0: (1) the inner set of a node is a strict subset of the node's outer set,
  (2) if a node has one child node only, then the node's inner set is identical
  to the child's outer set (which is a strict subset of the parent's outer set),
  and (3) if a node has more than one child node, then the parent's inner set
  always has more nodes than any of the outer sets of its child nodes (it is
  the outer sets of its siblings that distinguishes the outer set of a child
  from the inner set of its parent).
* H0, H1 and H2 always have one root set: (1) the root's outer set in case
  of H0 and H1, or (2) the root's inner set in case of H2.
* H2 is not a hierarchy because H2 always contains the empty set. That is,
  because any non-empty tree always has one or more leaf nodes (i.e. empty
  inner sets). Note that the root set of H2 may be empty.
* H2' is not a hierarchy, because if the node tree only has a single node,
  then H2 only contains the empty set. And because H2' is created from H2 by
  removing the empty set, H2' will itself be the empty set (i.e. no root set).
* H0 is not a hierarchy because the empty set is an element of H2. The empty
  set is therefore also an element of H0.
* In contrary to H2', H0' will always have the outer set of the tree's root
  as its root set. Because of that, H0' is a hierarchy of sets.

**CLARIFICATION**
A hierarchy can be created for any node tree (e.g. H1, H0').

Note that H1 is a subset of H0*.

**CLARIFICATION**
The following expressions are always true:

* `(#H1 = #N)`, `(#H2 <= #N)`, `(#H0 <= #N*2)`
* `(#H2' < #N)`, `(#H0' < #N*2)`

Note that ...

* H2 will only have one set per node, if the tree has a single leaf.
* If a tree has more than one leaf, then there is more than one node whose
  inner set is empty.
* H0 will only have two sets per node, if the tree has a single (root) node.
* Even H0 of a linear tree (a single path of nodes) will have less than two
  sets per node.
* Note that a node's inner set is identical to the outer set of its only child.
* Note that no set of elements/sets can contain an element/set more than once.

<!-- ======================================================================= -->
## Hierarchies as node trees

```
a hierarchy of sets                                node tree
=============================================  =>  =================

|-A-----------------------------------------|       A
| |-B---------------| |-H-| |-C-----------| |      =================
| | |-D-| |-E-----| | | 3 | | |-I-| |-F-| | |       B      H   C
| | | 1 | | |-G-| | | |---| | | 4 | | 5 | | |      ======     ======
| | |---| | | 2 | | |       | |---| |---| | |       D  E       I  F
| |       | |---| | |       |-------------| |         ===
| |       |-------| |                       |          G
| |-----------------|                       |
|-------------------------------------------|
```

Note that the above setup is not a strict setup (e.g. due to sets E and G).
Because of that, the setup is only a simple hierarchy.

**CLARIFICATION**
A simple hierarchy defines the structure of a rooted (unordered) tree.

* The tree's structure has one node per set (i.e. `#H = #N`).
* The tree's structure is not defined by the elements the sets
  contain (i.e. `(#{e | (e in s) and (s in H)} != #N)` may be true).
* The addition of further elements to the above sets (without changing
  the relationship a set has with all the other sets) will not change
  the structure of the node tree.
* What counts is what relationship a set has with all the other sets.

Note that, from a strict perspective, and if the relationship of a node would
be derived solely based on the definition of `subset-of`, then the resulting
tree has loops because each set is by definition a subset to itself. With that
in mind, and except for the root node, each node within the structure that such
a hierarchy defines has exactly two parent nodes: (1) the node itself, and (2)
another node. However, and even under that strict perspective, the structure
minus all the loops is that of a rooted (unordered) tree.

Note that the structure such a hierarchy defines has no cycles. In order to
have cycles, a parent set would also have to be a subset to one of its distinct
inner sets. That however is not possible because (1) any ancestor set always
has more elements than any of its descendant sets, and because (2) the hierarchy
is still a set of sets (i.e. it can not contain two identical elements/sets).

**TODO**
Given a set of elements, (1) how many such hierarchies are possible and/or
(2) what is the maximum number of nodes the resulting tree can possibly have?
(hint: resource management).

<!-- ======================================================================= -->
## Identifying subsets of nodes

**CLARIFICATION**
If N refers to the corresponding set of a node, and Ni to the set of its
i-th child node, then **the identifying subset** (ISS) is the result of
the following set operations:

* `ISS, identifying-subset := N - { n | n in any Ni }`
* `(#ISS = 1)`, if N is an outer set.
* `(#ISS >= 1)`, if N is the inner set of a parent.
* `(#ISS = 0)`, if N is the empty inner set of a leaf.

Note that the tree's structure can be reconstructed even though the identifying
subsets of all parent sets in the previous example are empty. Leaf sets and
their identifying subsets must not be empty, as those leaf sets would otherwise
count as subsets to any other set.

Note that the outer set of a node is the set of nodes of the subtree that has
the node as its root (hint: a rooted tree of nodes). In contrary to that, the
inner set of a node is the union of the outer sets of those subtrees that have
the node's child nodes as their root (hint: a forest).

**CLARIFICATION**
Each inner/outer set of nodes contains a non-empty subset of nodes which none
of its descendant inner/outer sets have. In addition to that, the corresponding
inner/outer set is the least significant inner/outer set that still contains
this non-empty subset.

With regards to H1:

* The outer set of a descendant
  is embedded into the outer set of an ancestor.
* The outer set of a node is the least significant set that
  still contains the outer set's defining node.
* None of the descendant outer sets has this node as an element.

With regards to H2:

* The inner set of a descendant
  is embedded into the inner set of an ancestor.
* The inner set of a node is the least significant set that
  still contains all of the defining node's child nodes.
* None of the descendant inner sets have even one of these
  child nodes as an element.

**CLARIFICATION**
Both characteristics combined allow to use such a non-empty subset in order to
identify a non-empty inner/outer set within the corresponding hierarchy (H1 or
H2).

<!-- ======================================================================= -->
## In search for equivalency

Because the relationships of the sets with all the other sets within a hierarchy
only defines the structure of a tree, a hierarchy is needed that can be defined
based on a given tree, which uniquely describes the initial tree's structure and
the tree's set of nodes. That is, the information which node a set represents
must be embedded into the tree's hierarchy of sets. This hierarchy will then
allow to recreate a node tree based on the tree's hierarchy of sets.

Such a hierarchy must therefore satisfy all of the following requirements:

* (req-0) The elements within the sets of the hierarchy must represent the
  nodes of the initial tree. That is, because these elements provide the means
  to embed the information of which node a set represents into the hierarchy.
* (req-1) The hierarchy must have one set per node. That is, because the tree
  created from it would otherwise have more or less nodes than the initial tree.
* (req-2) The relationships between the sets within the hierarchy must uniquely
  describe the relationships between the nodes of the initial tree.
* (req-3) The hierarchy must allow to determine the node a set represents
  (i.e. the set's defining node).

Even though setup H0 satisfies req-0, it does not satisfy req-1. H0 does
therefore not allow to reliably recreate the tree. And, because of that,
a hierarchy that could satisfy all the above requirements can only be a
strict subset of H0.

```
node tree                H2 - set of inner sets
===================  =>  ================================

 0                        0
===================      |-A----------------------------|
 1      2                |   1       2                  |
=====  ============      |  |-B---| |-C---------------| |
 ...    3      4         |  | ... | |  3       4      | |
       =====  =====      |  |-----| | |-D---| |-E---| | |
        ...    ...       |          | | ... | | ... | | |
                         |          | |-----| |-----| | |
                         |          |-----------------| |
                         |------------------------------|
```

Even though each inner set has an identifying subset of child nodes (e.g.
`{3,4}`), it is not possible to reliably determine the parent node of those
child nodes. The only statement that can be made, solely based on a hierarchy
of inner sets, is that the defining node of an inner set is an element of the
subset of child nodes of the inner set's parent set (e.g. `{1,2}`). Other than
that, it is not possible to identify the corresponding node among the child
nodes of a parent set (i.e. either `1` or `2`). Further information would be
required in order to reliably make that determination. Consequently, req-3
can not be satisfied.

Note that an unordered tree has no node order. Because of that, it can not be
assumed that the inner set's node can be determined by any order. In addition
to that, it can not be assumed that the data which represents a node (e.g. an
ID value) has any kind of relationship with regards to the data that represents
the node's child nodes (e.g. the lowest value amongst those values). That is,
any such data must be considered unique to a node, but random with regards to
all the other nodes.

Note that the hierarchy of inner sets does not contain the root node as an
element of any of its sets. From a strict perspective, it is therefore not
possible to determine which node the root set represents because the hierarchy
does not contain the root as an element. Consequently, it would be necessary to
add the root node to its inner set, which essentially replaces the root's inner
set with its outer set. Even though the hierarchy would then contain all the
nodes, req-3 could still not be satisfied. That is because, as before, it would
not be possible to reliably distinguish the root node from its child nodes.

```
node tree                H1 - hierarchy of outer sets
===================  =>  ================================

 0                         
===================      |-A----------------------------|
 1      2                | 0                            |
=====  ============      |  |-B---| |-C---------------| |
 ...    3      4         |  | 1.. | | 2               | |
       =====  =====      |  |-----| | |-D---| |-E---| | |
        ...    ...       |          | | 3.. | | 4.. | | |
                         |          | |-----| |-----| | |
                         |          |-----------------| |
                         |------------------------------|
```

Note that, even from a strict perspective, the hierarchy of outer sets (H1)
has one set per node. That is, req-0, req-1 and req-2 are (strictly) satisfied.

The outer set of a node contains by definition its defining node. In contrary
to inner sets, the defining node is the only node an outer set has that is not
also an element of any of the outer set's descendant sets. Consequently, the
hierarchy of outer sets also satisfies req-3.

**CLARIFICATION**
From a strict perspective, an unordered node tree can be recreated,
if the tree's hierarchy of outer sets (H1) is available.

<!-- ======================================================================= -->
## Equivalency between trees and hierarchies of sets

```
node tree         hierarchy of outer sets         node tree
===========  <=>  =========================  <=>  ===========

     1            |-1---------------------|            1     
===========       | |-2-| |-3-----| |-5-| |       ===========         
 2   3   5        | |---| | |-4-| | |---| |        2   3   5
    ===           |       | |---| |       |           ===
     4            |       |-------|       |            4
                  |-----------------------|
```

**CLARIFICATION**
Each rooted (unordered) node tree defines a strict hierarchy (H1),
which uniquely describes the rooted (unordered) node tree.

Note that this equivalency will be referred to as
the **set-based perspective** of a tree.
