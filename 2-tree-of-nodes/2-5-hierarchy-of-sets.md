
<!-- ======================================================================= -->
# A set-based perspective

Note that the following discussion is based upon rooted unordered node trees.

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

Note the outer box S0, which contains all the nodes of the node tree.
It encloses the node tree's root `1` and all of its descendants.

**CLARIFICATION**
A rooted tree `T := (N,E)` can be understood to define its set of nodes N.

Note that the following discussion focuses on the tree's set of nodes and
on some subsets of that set. Insofar, the set of edges E is only taken into
account as the formal basis that defines these sets via "connected nodes".
As such, the following (sub-)sets are understood to be identified and defined
by a node that acts as the starting point of a formal definition.

<!-- ======================================================================= -->
## The root's inner/outer set of nodes

```
set of nodes     inner and outer sets of node 1
=============    ==============================

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
for these particular sets of nodes. Both sets exist either way.

<!-- ======================================================================= -->
## The inner/outer set of a node

Each node within a tree can be understood to represent the root of a subtree.
And, because of that, any node can be understood to define two sets of nodes:
(1) A node's inner set S2 encloses its descendants. (2) A node's outer set S1
combines the node's inner set S2 with the node itself.

* `S1 = (node union S2)`
* An outer set always contains its defining node (i.e. never empty).
* An inner set is empty if (and only if) its defining node is a leaf.
* A non-empty inner set contains all child nodes of the defining node.
* An empty tree has no node and consequently no outer and no inner set.

The relationship between both sets:

* S2 is a strict subset of S1.
* A node's inner set is embedded into its outer set.
* S1 is super-ordinate to S2 and S2 sub-ordinate to S1.
* S1 is the parent (i.e. an ancestor) set of S2.
* S2 is the only child (i.e. a descendant) set of S1.
* There is no other (distinct) set in between S1 and S2.

Note that each set can be transformed into the other,
if the defining node is added to (or removed from) the other set.

**CLARIFICATION**
Each node can be said to contain all of its descendants.

Other ways to express that statement would be: (1) node `n1` contains node `n2`
if (and only if) `n2` is a node of the subtree that has `n1` as its root. Or
(2) `n1`'s outer set contains `n2`.

<!-- ======================================================================= -->
## Relationship between sets of different nodes

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

* The outer set of a child
  is a subset of the inner set of its parent.
* The outer set of a child
  is sub-ordinate to the inner set of its parent.

Note that, even though both sets have different defining nodes, the outer set 
of a child is identical to the inner set of its parent, if (and only if) the
parent has no other child. That is, the child has no siblings.

* Both sets of a node are a subsets to any set of any of the node's ancestors.
* None of those contains a node that an ancestor set does not contain.
* The inner set of a node is the union of the outer sets of its child nodes.

The above statements should be fairly obvious because any descendant of a node
is also a descendant of the node's ancestors and, as such, also an element of
any set of any of the node's ancestors.

**CLARIFICATION**
The outer set of a node is unique to a node.
No other node has the exact same outer set.

If two nodes `n1` and `n2` are independent from one another (i.e. none of those
is an ancestor of the other), then the outer sets of both nodes have no nodes
in common. That is, such nodes always have different outer sets.

If node `n1` is an ancestor of `n2`, then `n1`'s outer set contains `n1`. And
because `n2`'s outer set does not contain `n1`, the outer sets of both nodes
are different. Put differently, the outer set of an ancestor always has more
nodes than the outer set of a descendant.

**CLARIFICATION**
The inner set of a node is unique to a node.
No other node has the exact same inner set.

If two nodes `n1` and `n2` are independent from one another (i.e. none of those
is an ancestor of the other), then the inner sets of both nodes have no nodes
in common. That is, such nodes always have different inner sets.

If node `n1` is an ancestor of `n2`, then `n1`'s inner set contains `n2`. And
because `n2`'s inner set does not contain `n2`, the inner sets of both nodes
are different. Put differently, the inner set of an ancestor always has more
nodes than the inner set of a descendant.

**CLARIFICATION**
Each node defines its very own inner and outer sets of nodes.

Note the special case of empty inner sets of nodes. However, a node tree can
loosely be understood to have unique inner sets (empty ones included) for each
of its nodes. They can be distinguished from one another via their defining node.

**CLARIFICATION**
The inner set of a node is identical to the outer set of its
*only child*.

That is, because the outer set of a descendant is in general only a simple
subset (not a strict subset) of the inner set of an ancestor.

Note that, if the parent has more than one child, this identity does not exist.

<!-- ======================================================================= -->
## Node trees as hierarchies of sets

**CLARIFICATION**
The set of sets (H0), that holds all the inner and all the outer sets
of all of the nodes within a tree, represents a hierarchy of sets.

That is, the set of sets is consistent with the `subset-of` operator because
there are no two sets that overlap each other. For each pair of sets, it can
be determined that they are either independent from one another, or that one
set is a subset of the other.

Note that the same applies to the set of sets (H1), which only contains the
outer sets of all the nodes, and the set of sets (H2), which only contains
the inner sets of these nodes (i.e. `H0 = (H1 union H2)`).

Note that even though H0 is only a (simple) hierarchy of sets, H1 and H2 both
are on their own strict hierarchies of sets. That is, because any ancestor
inner/outer set has more elements than any of its descendant inner/outer sets.

**CLARIFICATION**
The complete hierarchy of a node tree (H0) is considered to hold two sets per
node, which can be distinguished via their defining nodes and some boolean
`isOuterSet` property. That is, the following two expressions are both
considered to hold: (A) `(#H2 = #N)` and (B) `#H0 = (#H1 + #H2) = #N*2`.

Note however that, from a strict mathematical perspective, both expressions
are wrong. That is, because (1) the inner set of a child may be identical to
the outer set of its parent, and because (2) the inner set of any leaf is the
empty set. With that in mind, the `=` operator within the above two expressions
would have to be replaced by the `<=` operator for both expressions to evaluate
to `true` under that strict perspective.

**CLARIFICATION**
A node tree represents a hierarchy of sets of nodes (H0).

Note that any subset of H0 represents a forest of such hierarchies. However,
and under certain circumstances, a subset may represent a single hierarchy
(e.g. H1 and H2).

**Memory hook**
Take a piece of paper and use it to draw a rooted node tree. After that, draw
a border around that node tree. Then, draw a border around each subtree. When
done, the set of borders represents the tree's hierarchy of outer sets (H1).

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

Note that the above hierarchy neither represents a hierarchy of inner (H2),
nor a hierarchy of outer (H1) sets. That is, because the identifying subset
(see below) of root sequence A is empty.

**CLARIFICATION**
A hierarchy of sets defines the structure of a rooted (unordered) tree.

* The tree's structure has one node per set (i.e. `#H = #N`).
* The tree's structure is not defined by the elements the sets
  contain (i.e. `(#{e | (e in s) and (s in H)} != #N)` may be true).
* What counts is what relationship a set has with all the other sets.

Note that, from a strict perspective, the resulting tree has loops because each
set is by definition a subset to itself. With that in mind, and except for the
root node, each node within the structure that such a hierarchy defines has
exactly two parent nodes: (1) the node itself, and (2) another node. However,
and even under that strict perspective, the structure minus all the loops is
that of a rooted (unordered) tree.

Note that the structure such a hierarchy defines has no cycles. In order to have
cycles, a parent set would also have to be a subset to one of its descendant
sets. That however is not possible because (1) any ancestor set always has more
elements than any of its descendant sets, and because (2) the hierarchy is still
a set of sets (i.e. it can not contain two identical elements/sets).

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
its set of nodes. That is, the information which node a set represents must be
embedded into the tree's hierarchy of sets. This hierarchy would then allow to
recreate a node tree based on its own hierarchy of sets.

Such a hierarchy must therefore satisfy all of the following requirements:

* (req-0) The elements within the sets of the hierarchy must represent the
  nodes of the initial tree. That is, because these elements provide the only
  means available to embed the information of which node a set represents into
  the hierarchy.
* (req-1) The hierarchy must have one set per node. That is, because the tree
  created from it would otherwise have more or less nodes than the initial tree.
* (req-2) The relationships of all the sets of nodes with all the other sets
  within the hierarchy must represent the structure of the initial node tree.
* (req-3) The hierarchy must allow to determine the node a set represents.

Even though hierarchy H0 satisfies req-0, it does not satisfy req-1. H0 does
therefore not allow to reliably recreate the tree. And, because of that, a
hierarchy that could satisfy all the requirements can only be a strict subset
of H0.

```
node tree                H2 - hierarchy of inner sets
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

Note that the hierarchy of inner sets (H2) can be understood to have one set
per node. That is, if leaf nodes are understood to have unique empty inner
sets. Hence, H2 (loosely) satisfies req-0, req-1 and req-2.

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
