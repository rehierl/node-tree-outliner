
<!-- ======================================================================= -->
# A set-based perspective

```
tag soup          node tree      (simplified)      set of nodes
============  =>  =========  =>  ============  =>  =================

<1>                   1               1            |-S0--------|
  2                   |           =========        |     1     |
  <3> 4 </3>      =========       2   3   5        | ========= |
  5               |   |   |          ===           | 2   3   5 |
</1>              2   3   5           4            |    ===    |
                      |                            |     4     |
                      4                            |-----------|
```

Note box S0, which contains all the nodes of the node tree.
It encloses the node tree's root `1` and all of its descendants.

**CLARIFICATION**
A rooted tree `T := (N,E)` can be understood to define its set of nodes N.

Note that the following discussion focuses on the tree's set of nodes and on
some of its subsets. Thus, the set of edges E is only taken into account as
the formal basis that defines these sets via "nodes that are connected". As
such, the following (sub-)sets are understood to be identified by a node that
acts as the starting point of a formal definition.

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

Each rooted tree has exactly one most significant node, its root node A.

* A root can be understood to define two sets of nodes.
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
A node's inner set S2 encloses its descendants, and its outer set S1 combines
the node's inner set S2 with the node itself.

* An outer set always contains its defining node (i.e. never empty).
* An inner set is empty if, and only if, its defining node is a leaf.
* An empty tree has no node and consequently no outer and no inner set.

The relationship between both sets:

* S2 is a strict subset of S1.
* A node's inner set is embedded into its outer set.
* S1 is super-ordinate to S2 and S2 is sub-ordinate to S1.
* S1 is the parent (i.e. an ancestor) set of S2.
* S2 is the only child (i.e. a descendant) set of S1.
* There is no other (distinct) set in between S1 and S2.

**CLARIFICATION**
The inner set of a node is unique to a node.
No other node has the exact same inner set.

If two nodes `n1` and `n2` are independent from one another (i.e. none of those
is an ancestor of the other), then the inner sets of both nodes have no nodes
in common. That is, such nodes always have different descendants and therefore
different inner sets.

If node `n1` is an ancestor of `n2`, then `n1`'s inner set contains `n2`. And
because `n2`'s inner set does not contain `n2`, the inner sets of both nodes
are different.

**CLARIFICATION**
The outer set of a node is unique to a node.
No other node has the exact same outer set.

That is, because these sets always differ in the defining node.

Note that, the outer set of an ancestor always has one node (i.e. the defining
node) that is not an element of the outer set of any of its descendants. That
is, the outer set of a descendant is embedded into the outer set of an ancestor.

**CLARIFICATION**
Each node defines its very own inner and outer sets of nodes.

One such set can be transformed into the other, if the defining node is added
to, or removed from the corresponding set.

Note the special case of empty inner sets of nodes. However, a node tree can
be understood to have unique inner sets (empty ones included) for each of its
nodes. They can be distinguished from one another via their defining node.

**CLARIFICATION**
Each node can be said to contain all of its descendants.

Other ways to express that statement would be: (1) if node `n1` contains node
`n2`, then `n2` is a node of the subtree that has `n1` as its root. Or (2) the
set of nodes of `n1`'s subtree contains `n2` as an element. Or (3) `n1`'s outer
set of nodes contains `n2`.

<!-- ======================================================================= -->
## Node trees as hierarchies of sets

```
node tree          set of outer sets
=============  =>  ============================

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

* The outer set of a child is a subset of the inner set of its parent.
* The outer set of a child is sub-ordinate to the inner set of its parent.
* Both sets of a node are a subsets to any set of any of the node's ancestors.
* None of those sets contains a node that an ancestor set does not contain.

The above statements should be fairly obvious because any descendant of a node
is also a descendant of the node's ancestors and, as such, also an element of
an ancestor's set.

* The inner set of a node is the union of all of the sets of its descendants.
* The inner set of a node is the union of the outer sets of its child nodes.

Note that, even though both sets have different defining nodes, the outer set 
of a child is identical to the inner set of its parent, if (and only if) the
child's parent node has no other child. Put differently: if the child has no
siblings.

**CLARIFICATION**
The set of sets (H0), that holds all the inner and all the outer sets
of all of the nodes within a node tree, represents a hierarchy of sets.

That is, the set of sets is consistent with the `subset-of` operator because
there are no two sets that overlap each other. For each pair of sets, it can
be determined that they are either independent from one another, or that one
set is a subset of the other.

Note that the same applies to the set of sets (H1), that only contains the
outer set of all the nodes, and the set of sets (H2) that only contains the
inner sets of these nodes (i.e. `H0 := (H1 union H2)`).

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

Note that any subset of H0 also represents a hierarchy of sets.

<!-- ======================================================================= -->
## Hierarchies of sets as node trees

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

**CLARIFICATION**
A hierarchy of sets defines the structure of a rooted (unordered) tree.

* The tree's structure has one node per set (i.e. `#H = #N`).
* The tree's structure is not defined by the actual elements that the sets
  within the hierarchy contain (i.e. `(#{e | (e in h) and (h in H)} != #N)`).
* What counts is what relationship a set has with another set.

Note that, from a strict perspective, the node tree has loops because each
set is by definition a subset to itself. With that in mind, and except for
the root node, each node within the structure that such a hierarchy defines
has exactly two parent nodes: (1) the node itself, and (2) another node.
However, and even under a strict perspective, that structure minus all the
loops is a rooted (unordered) tree.

Note that the structure such a hierarchy defines will not have any cycles.
In order to have cycles, a parent set would also have to be a subset to one
of its descendant sets. That however is impossible because (1) any ancestor
set always has more elements than any of its descendant sets, and (2) the
hierarchy is still a set of sets (i.e. it can not contain two completely
different sets that have identical content).

<!-- ======================================================================= -->
## In search for equivalency

Because the relationships of the sets with all the other sets within a hierarchy
only defines the structure of a tree, a hierarchy is needed that can be defined
based on a given tree, which uniquely describes the initial tree's structure and
its set of nodes. That is, the information which node a set represents must be
embedded into the tree's hierarchy.

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
therefore not allow to reliably recreate the tree. And, because of that, the
hierarchy that may satisfy all the requirements can only be a strict subset
of H0.

Note that the outer set of a node is the set of nodes of the subtree that has
the node as its root (hint: a rooted tree of nodes). In contrary to that, the
inner set of a node is the union of the outer sets of those subtrees that have
the node's child nodes as their root (hint: a forest).

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
per node. That is, if leaf nodes are understood to have unique empty inner sets.
That is, req-0, req-1 and req-2 can be understood to be (loosely) fulfilled.

The inner set of a node obviously contains a subset of nodes that only contains
the child nodes of that node (e.g. `{3,4}`). Because of that, such a subset of
an inner set uniquely identifies each inner set. Even though each inner set has
an identifying subset of child nodes, there is no way to reliably determine the
parent node of those child nodes. The only statement that can be made, solely
based on a hierarchy of inner sets, is that the node of a set is an element of
the subset of child nodes of the set's parent set (e.g. `{1,2}`). Other than
that, it is not possible to identify the corresponding node amongst the child
nodes of a parent set. Further information would be required in order to
reliably make that determination. Consequently, req-3 can not be satisfied.

Note that the set of child nodes of the inner set of a node is a subset to all
of the inner set's ancestor sets. In contrary to that, none of the inner set's
descendant sets contains any of the nodes within that set of child nodes. That
is, the inner set is the least significant set that has this set of child nodes
as a subset.

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
does not contain the root. Consequently, it would be necessary to add the root
node to its inner set, which essentially replaces the root's inner set by the
root's outer set. Even though the hierarchy would then contain all the nodes,
req-3 could still not be fulfilled. That is because, as before, it would not be
possible to reliably distinguish the root node from its child nodes.

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
has one set per node. That is, req-0, req-1 and req-2 are (strictly) fulfilled.

The outer set of a node obviously contains its defining node. Furthermore,
the defining node of each outer set is an element of all of the outer set's
ancestor sets, but not an element of any of the outer set's descendant sets.
In addition to that, an outer set has no other node that is not also an
element of any of the outer set's descendant sets. Consequently, the
hierarchy of outer sets also satisfies req-3.

**CLARIFICATION**
Only the hierarchy of outer sets (H1) fulfills all of the above requirements.

Note that H1 also represents a strict hierarchy of sets.

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
Each rooted (unordered) node tree defines a strict hierarchy of outer sets,
and that hierarchy uniquely describes the rooted (unordered) node tree.

Note that this equivalency will be referred to as
the **set-based perspective** of a tree.

**Memory hook**
Take a piece of paper and use it to draw a rooted node tree. After that, draw
a border around that node tree. Then, draw a border around each subtree. When
done, the set of borders represents the tree's strict hierarchy of outer sets.
