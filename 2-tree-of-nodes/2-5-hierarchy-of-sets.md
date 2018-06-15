
<!-- ======================================================================= -->
# A set-based perspective

```
tag soup        node tree    (simplified)    set of nodes
============    =========    ============    =================

<A>                 A             A          |-----------| < S
  B                 |         =========      |     A     |
  <C> D </C>    =========     B   C   E      | ========= |
  E             |   |   |        ===         | B   C   E |
</A>            B   C   E         D          |    ===    |
                    |                        |     D     |
                    D                        |-----------|
```

Note the box (S) that surrounds all the nodes of the node tree.
It contains the node tree's root (A) and all of its descendants.

**CLARIFICATION**
A rooted tree `T := (N,E)` represents its set of nodes (N).

Note that this perspective ignores the edges (E) of the tree.

<!-- ======================================================================= -->
## The root's inner/outer set of nodes

```
set of nodes         inner and outer sets of A
=================    =============================

|-----------| < S    |----------------------| < S1
|     A     |        |  A                   |
| ========= |        | |-------------| < S2 |
| B   C   E |        | | B    C    E |      |
|    ===    |        | |     ===     |      |
|     D     |        | |      D      |      |
|-----------|        | |-------------|      |
                     |----------------------|
```

Each rooted tree has exactly one most significant node, its root node (A).

* A root node is said to represent two sets of nodes.
* The root's outer set (S1) contains the root itself and all of its descendants.
* The root's inner set (S2) contains the root's descendants, but not the root.
* A tree's set of nodes is identical to the outer set of its root.

Note that the definitions of the inner and outer sets are based upon mere
observations. They do not define anything new other than names/references
for these particular sets of nodes. Both sets exist either way.

<!-- ======================================================================= -->
## The inner/outer set of a node

Each node within a tree can be understood to represent the root of a subtree.
And, because of that, any node can be understood to represent two sets of nodes:
(S1) the set of nodes which contains that node and all of its descendants (i.e.
its outer set), and (S2) the set of nodes which only contains the descendants
of that node (i.e. its inner set).

* No outer set of a node is ever empty.
* An outer set always contains its defining node.
* An inner set is empty if, and only if, its defining node is a leaf.
* An empty tree has no node and consequently no outer and no inner set.

The relationship between a node's inner and outer sets:

* S2 is a strict subset of S1.
* S1 is the parent (i.e. an ancestor) set of S2.
* S2 is the only child (i.e. a descendant) set of S1.
* There is no other (distinct) set in between S1 and S2.

**CLARIFICATION**
The outer set of a node is unique to that node.
No other node has the exact same outer set.

That is, because these sets always differ in the defining node.

**CLARIFICATION**
The inner set of a node is unique to that node.
No other node has the exact same inner set.

If two nodes `n1` and `n2` are independent from one another (i.e. none of those
is an ancestor of the other), then the inner sets of both nodes have no nodes
in common. That is, such nodes always have different descendants and therefore
different inner sets.

If node `n1` is an ancestor of `n2`, then `n1`'s inner set of nodes contains
`n2`. And because `n2`'s inner set does not contain `n2`, the inner sets of
both nodes are different. To be more clear, the inner set of an ancestor always
has more elements than the inner set of a descendant.

Note that the outer set of a node is identical to the inner set
of its parent if, and only if, the node has no siblings.

**CLARIFICATION**
A 1:1 relationship exists between each node and its inner and outer sets.

Note the special case of empty inner sets of nodes. However, a node tree could
be considered to have unique empty inner sets for each of its leaf nodes. These
can be distinguished from one another via their defining leaf nodes.

**CLARIFICATION**
Each node represents its inner and its outer set of nodes.

One such set can be transformed into the other, if the defining node is added
(or removed) to (or from) the corresponding set.

**CLARIFICATION**
Each node can be said to contain all of its descendants.

That is, because each node represents its inner set of nodes. Put differently,
the subtree a node defines contains all of the node's descendants.

<!-- ======================================================================= -->
## Node trees as hierarchies of sets

```
node tree        all inner sets
=============    ========================

      A           A
=============    |----------------------|
 B    C    E     |  B     C         E   |
     ===         | |--|  |------|  |--| |
      D          | |--|  |  D   |  |--| |
                 |       | |--| |       |
                 |       | |--| |       |
                 |       |------|       |
                 |----------------------|
```

Note that the visual representation can not adequately represent the outer
set of a node. It would be difficult to identify the defining node of an
outer set, if all of its nodes would be within the corresponding set.

* The outer set of a child is a subset of the inner set of its parent.
* Both sets of a node are a subsets to any of the sets of the node's ancestors.
* No such set contains a node that an ancestor set does not contain.

The above statements should be fairly obvious because any descendant of a node
is also a descendant of the node's ancestors and, as such, also an element of
an ancestor's set.

* The inner set of a node is the union of all of the sets of its descendants.
* The inner set of a node is the union of the outer sets of its child nodes.

**CLARIFICATION**
All the inner and outer sets of a tree represent a hierarchy of sets.

That is, the set of sets is consistent with the `subset-of` operator because
there are no two sets that overlap each other. For each pair of sets, it can be
determined that they are either independent from one another, or that one set
is a subset of the other.

**CLARIFICATION**
Any tree represents a hierarchy of outer sets and a hierarchy of inner sets.

(Recall that each leaf node represents a unique empty inner set).

<!-- ======================================================================= -->
## Equivalency between trees and hierarchies of sets

```
a hierarchy of inner sets          node tree            tag soup          
============================       =================    ==============    

 A                                  A                   <A>
|-----------------------------|    =================      <B>
|  B              H    C      |     B      H   C            D
| |------------| |--| |-----| |    ======     ======        <E> G </E>
| |  D    E    | |--| | I F | |     D  E       I  F       </B>
| | |--| |---| |      |-----| |       ===                 H
| | |--| | G | |              |        G                  <C>
| |      |---| |              |                             I                                  
| |------------|              |                             F                                  
|-----------------------------|                           </C>                                 
                                                        </A>
```

Note that, this visual representation of a set of sets represents a hierarchy
of inner sets. The empty inner sets of nodes G, I and F are missing for display
purposes. A proper definition of the set hierarchy would obviously have to
include one set (empty or not) per node.

**CLARIFICATION**
A hierarchy of sets represents a rooted (unordered) tree.

Note that the tree which can be created based on a given hierarchy of sets is
unique to that hierarchy. That is, each such hierarchy represents one tree and
one tree only.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Each rooted node tree represents a hierarchy of sets,
and each hierarchy of sets a rooted node tree.

**CLARIFICATION**
The hierarchy of sets of a rooted tree will be
referred to as the tree's "set-based perspective".

**Memory hook**
Take a piece of paper and draw a rooted node tree onto it. After that, draw a
border around that node tree. Then, draw a border around each subtree. The set
of borders represents the tree's hierarchy of outer sets.
