
<!-- ======================================================================= -->
# A set-based perspective

```
tag soup        node tree    (simplified)   set of nodes
============    =========    ============   =============

<A>                 A             A         |-----------| < S
  B                 |         =========     |     A     |
  <C> D </C>    =========     B   C   E     | ========= |
  E             |   |   |        ===        | B   C   E |
</A>            B   C   E         D         |    ===    |
                    |                       |     D     |
                    D                       |-----------|
```

Note the box (S) that surrounds all the nodes within the node tree,
it contains the node tree's root (A) and all of its descendants.

**CONCLUSION**
A rooted tree `T := (N,E)` represents the set of its nodes (N).

Note that this perspective does not focus on the edges (E) of a tree.

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
observations. They do not define anything new other than names/references
for these particular sets of nodes. Both sets exist either way.

<!-- ======================================================================= -->
## The inner/outer set of a node

Each node within a tree is understood to represent the root of a subtree. And,
because of that, any node can be understood to represent two sets of nodes:
(S1) the set of nodes which contains that node and all of its descendants, and
(S2) the set of nodes which only contains the descendants of that node.

* No outer set of a node is ever empty.
* An outer set always has at least one node (i.e. its defining root node).
* An inner set is empty if, and only if, its defining node has no descendants.
* An empty tree has no node and consequently no outer and no inner set.

The relationship between a node's inner and outer sets:

* The inner set of a node is a subset of the node's outer set.
* S1 is the parent (i.e. an ancestor) set of S2.
* S2 is the only child (i.e. a descendant) set of S1.
* There is no other distinct set in between S1 and S2.

**CONCLUSION**
Each node represents its inner and its outer set of nodes.

One such set can be transformed into the other, if the defining node is added
(or removed) to (or from) the corresponding set.

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
* Both sets of a given node are a subsets
  to any of the sets of the node's ancestors.
* Each node within the two sets of a node is also
  an element within any of the sets of the node's ancestors.
* No such set contains a node that an ancestor set does not contain.

The above statements should be fairly obvious because
any descendant of a node is also a descendant of the node's ancestors
and as such also an element of an ancestor's set.

* The inner set of a node is the union of the outer sets of its child nodes.
* The inner set of a node is the union of all of the sets of its descendants.
* The outer set of a child is identical to the inner set of its parent if,
  and only if, the parent has no other child.

Note the special case of an empty inner set of nodes. Also note that a node
tree has a unique empty inner set for each of its leaf nodes. These empty
sets can be identified via their defining leaf nodes.

<!-- ======================================================================= -->
## Equivalency between trees and hierarchies of sets

```
A node tree                                A hierarchy of sets
====================================       ============================

 <A>                   A                    A
   <B>             =================       |--------------------------|
     D              B      H   C           |  B            H   C      |
     <E> G </E>    ======     ======       | |----------|     |-----| |
   </B>             D  E       I  F        | | D   E    |     | I F | |
   H                  ===                  | |    |---| |     |-----| |
   <C>                 G                   | |    | G | |             |
     I                                     | |    |---| |             |
     F                                     | |----------|             |
   </C>                                    |--------------------------|
 </A>
```

**CONCLUSION**
Each rooted node tree represents a hierarchy of sets,
and each hierarchy of sets a rooted node tree.

Note that these hierarchies of sets are consistent with the definition of sets
of elements. That is, none of these sets overlap: One set either is embedded
into another set, or both sets have no nodes in common.

Note that the sets of sibling nodes have no nodes in common. They are said to
be independent from one another. The same applies to any two sets that are
located within (independent) sibling trees.

**CONCLUSION**
The hierarchy of sets of a rooted tree will be
referred to as the tree's "set-based perspective".

**Memory hook**
Take a piece of paper and draw a rooted node tree onto it. After that, draw a
border around that node tree. Then, draw a border around each subtree. The set
of drawn borders represents the tree's hierarchy of sets.
