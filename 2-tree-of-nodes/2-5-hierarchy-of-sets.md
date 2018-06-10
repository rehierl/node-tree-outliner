
<!-- ======================================================================= -->
# The set-based perspective of a tree

```
sequence        node tree    (simplified)   set of nodes
============    =========    ============   =============

<A>                 A             A         |-----------| < S
  B                 |         =========     |     A     |
  <C> D </C>    =========     B   C   E     | ========= |
  E             |   |   |        ===        | B   C   E |
</A>            B   C   E         D         |    ===    |
                    |                       |     D     |
                    D                       |-----------|
```

Note the box (S) that surrounds all the nodes of within the above tree,
it contains the tree's root node (A) and all of its descendants.

**CONCLUSION**
A rooted tree `T := (N,E)` can be understood
to represent the set of its nodes (N).

Note that this perspective of a tree does not focus on a tree's edges (E).

<!-- ======================================================================= -->
## The root's inner/outer set of nodes

```
set of nodes            (extended)
=============           =========================

|-----------| < S       |----------------------| < S1
|     A     |           |  A                   |
| ========= |           | |-------------| < S2 |
| B   C   E |           | | B    C    E |      |
|    ===    |           | |     ===     |      |
|     D     |           | |      D      |      |
|-----------|           | |-------------|      |
                        |----------------------|
```

Each rooted tree has exactly one most significant node, its root node (A).

* A root node can be understood to represent two sets of nodes.
* The root's outer set (S1) holds the root and all of its descendants.
* The root's inner set (S2) only contains the root's descendants.
* That is, S2 does not contain the root itself.
* A tree's set of nodes is identical to its root's outer set.

Note that the definitions of the inner and outer sets are based upon mere
observations. They do not define anything new other than references for
these particular sets of nodes.

<!-- ======================================================================= -->
## The inner/outer set of a node

Each node within a tree is understood to represent the root of a subtree. And,
because of that, any node can be understood to represent two sets of nodes:
(S1) the set of nodes which contains that node and all of its descendants, and
(S2) the set of nodes which only contains the node's descendants.

* No outer set of a node is ever empty.
* An outer set always contains at least one node (i.e. its defining root node).
* An inner set is empty if, and only if, its defining node has no descendants.
* An empty tree has no node and consequently no outer and no inner set.

The relationship between a node's inner and outer sets:

* The inner set of a node is a subset of the node's outer set.
* S1 is the parent set (i.e. an ancestor) of S2.
* S2 is the only child set (i.e. a descendant) of S1.
* There is no other set in between S1 and S2.

**CONCLUSION**
Each node represents its inner and its outer set of nodes.

One such set can be transformed into the other, if the defining node is added
(or removed) to (or from) the given set. Because of that, it is also possible
to loosely speak of "the" set of nodes a node represents.

**CONCLUSION**
Each node represents and contains all of its descendants.

<!-- ======================================================================= -->
## Node trees as hierarchies of sets

```
set of nodes        (extended)          (complete)
===============     ===============     ============================

 A                   A                   A
|-------------|     |-------------|     |--------------------------|
| B    C    E |     | B   C     E |     |  B     C        |  E   | |
|     ===     |     |    |---|    |     | |--|  |------|  | |--| | |
|      D      |     |    | D |    |     | |--|  |  D   |  | |--| | |
|-------------|     |    |---|    |     |       | |--| |  |------| |
                    |-------------|     |       | |--| |           |
                                        |       |------|           |
                                        |--------------------------|
```

* The outer set of a child is a subset of the inner set of its parent.
* Any of the two sets of a given node is a subset
  of any of the sets of the node's ancestors.
* Each node within the sets of a node is also
  an element of any of the sets of the node's ancestors.
* No such set contains a node that an ancestor set does not contain.

The above statements should be fairly obvious because
any descendant of a node is also a descendant of the node's ancestors.

* The inner set of a node is the union of all of the sets of its descendants.
* The inner set of a node is the union of the outer sets of its child nodes.
* The outer set of a child may be identical to the inner set of its parent.
  (If, and only if, the parent node has no other child node).

Note the special case of an empty inner set of nodes. Also note that a node
tree has a unique empty inner set for each of its leaf nodes. These empty
sets can be identified via their defining leaf nodes.

<!-- ======================================================================= -->
## Equivalency between trees and hierarchies of sets

```
A hierarchy of sets           <=>   A tree of nodes
===========================         ========================================

 A                                       A                   <A>
|-------------------------|         =============            | <B>
|  B             C        |          B     H  C              | | D
| |---------|   |-------| |         ======   ======          | | <E> G </E>
| | D  E    |   |     F | |          D  E     I  F           | </B>
| |   |---| |   |       | |   <=>      ===             <=>   | H
| |   | G | | H | I     | |             G                    | <C>
| |   |---| |   |       | |                                  | | I
| |---------|   |-------| |                                  | | F
|-------------------------|                                  | </C>
                                                             </A>
```

**CONCLUSION**
Each node tree represents a hierarchy of sets of elements, and
each hierarchy of sets of elements represents a node tree.

Note that these hierarchies of sets of elements are consistent with the
definition of sets of elements. That is, none of these sets overlap: One set
either is completely embedded into another set, or both sets have no nodes in
common.

Note that the sets of elements of sibling nodes have no nodes in common. They
are said to be independent from one another. The same applies to any two sets
that are located within (independent) sibling trees.

**CONCLUSION**
The hierarchy of sets of a tree will be referred to as the
"set-based perspective" of a tree.

**Memory hook**
Take a piece of paper and draw a rooted node tree onto it. Then, draw a border
around that node tree. And finally, draw a border around each and every of the
tree's subtrees. The set of drawn borders represents the tree's hierarchy of
sets.
