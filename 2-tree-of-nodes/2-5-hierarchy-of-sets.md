
<!-- ======================================================================= -->
# A set-based perspective

```
tag soup        node tree    (simplified)    set of nodes
============    =========    ============    =================

<1>                 1             1          |-S0--------|
  2                 |         =========      |     1     |
  <3> 4 </3>    =========     2   3   5      | ========= |
  5             |   |   |        ===         | 2   3   5 |
</1>            2   3   5         4          |    ===    |
                    |                        |     4     |
                    4                        |-----------|
```

Note box S0 that contains all the nodes of the node tree.
It encloses the node tree's root A and all of its descendants.

**CLARIFICATION**
A rooted tree `T := (N,E)` represents its set of nodes N.

Note that the following discussion focuses on the tree's set of nodes and on
some of its subsets. The set of edges E is therefore only taken into account
as the basis which defines these sets of nodes.

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

* An outer set always contains its defining node - i.e. never empty.
* An inner set is empty if, and only if, its defining node is a leaf.
* An empty tree has no node and consequently no outer and no inner set.

The relationship between the outer and the inner sets of a node:

* S2 is a strict subset of S1 - i.e. S2 is embedded into S1.
* A node's inner set is embedded into the node's outer set.
* S1 is super-ordinate to S2 and S2 sub-ordinate to S1.
* S1 is the parent (i.e. an ancestor) set of S2.
* S2 is the only child (i.e. a descendant) set of S1.
* There is no other (distinct) set in between S1 and S2.

Note that the outer set of a node is the set of nodes of the subtree that has
the node as its root (hint: a rooted tree of nodes). In contrary to that, the
inner set of a node is the union of those outer sets that have the node's child
nodes as their root (hint: a forest).

**CLARIFICATION**
The inner set of a node is unique to a node.
No other node has the exact same inner set.

If two nodes `n1` and `n2` are independent from one another (i.e. none of those
is an ancestor of the other), then the inner sets of both nodes have no nodes
in common. That is, such nodes always have different descendants and therefore
different inner sets.

If node `n1` is an ancestor of `n2`, then `n1`'s inner set of nodes contains
`n2`. And because `n2`'s inner set does not contain `n2`, the inner sets of
both nodes are different.

**CLARIFICATION**
The outer set of a node is unique to a node.
No other node has the exact same outer set.

That is, because these sets always differ in the defining node.

Note that, the outer set of an ancestor always has one node (i.e. the defining
node) that is not an element of the outer set of any of its descendants. That
is, the outer set of a descendant is embedded into the outer set of an ancestor.

**TODO**
Note that the inner set of an ancestor always has one node (i.e. the defining
node) that is not an element of the inner set of its descendants. That is,
the inner set of a descendant is embedded into ...
To be more clear, the inner set of an
ancestor always has more elements than the inner set of a descendant.

**CLARIFICATION**
Each node defines its inner and its outer set of nodes.

One such set can be transformed into the other, if the defining node is added
to, or removed from the corresponding set.

Note the special case of empty inner sets of nodes. However, a node tree can
be understood to have unique inner sets (empty ones included) for each of it
nodes. They can be distinguished from one another via their defining node.

**CLARIFICATION**
Each node can be said to contain all of its descendants.

Other ways to express the same statement would be: (1) if node `n1` contains
node `n2`, then `n2` is a node of the subtree that has `n1` as its root. Or (2)
the set of nodes of `n1`'s subtree contains `n2` as an element. Or (3) `n1`'s
outer set of nodes contains `n2`.

<!-- ======================================================================= -->
## Node trees as hierarchies of sets

```
node tree        the tree's set of outer sets
=============    ============================

      1          |-A---------------------|
=============    | 1                     |
 2    3    5     | |-B-| |-C-----| |-E-| |
     ===         | | 2 | | 3     | | 5 | |
      4          | |---| | |-D-| | |---| |
                 |       | | 4 | |       |
                 |       | |---| |       |
                 |       |-------|       |
                 |-----------------------|
```

* The outer set of a child is a subset of the inner set of its parent.
* The outer set of a child is sub-ordinate to the inner set of its parent.
* Both sets of a node are a subsets to any of the sets of the node's ancestors.
* No such set contains a node that an ancestor set does not contain.

The above statements should be fairly obvious because any descendant of a node
is also a descendant of the node's ancestors and, as such, also an element of
an ancestor's set.

* The inner set of a node is the union of all of the sets of its descendants.
* The inner set of a node is the union of the outer sets of its child nodes.

Note that, even though both sets have different defining nodes, the outer set 
of a child is identical to the inner set of its parent, if (and only if) the
child's parent node has no other child. Put differently, if the child has no
siblings.

**CLARIFICATION**
The set of sets (H0), that holds all the inner and all the outer sets
of all of the nodes of a node tree, represents a hierarchy of sets.

That is, the set of sets is consistent with the `subset-of` operator because
there are no two sets that overlap each other. For each pair of sets, it can
be determined that they are either independent from one another, or that one
set is a subset of the other.

Note that the same applies to the set of sets (H1), that only contains the
outer set of all the nodes, and the set of sets (H2) that only contains the
inner sets of these nodes (i.e. `H0 := (H1 union H2)`).

**CLARIFICATION**
A node tree represents a hierarchy of sets of nodes (H0).

Note that any subset of H0 also represents a hierarchy of sets.

**CLARIFICATION**
The complete hierarchy of a node tree (H0) is considered to hold two sets per
node, which can be distinguished via their defining node and some boolean
`isOuterSet` property. That is, the following two expressions are both
considered to hold: (A) `(#H2 = #N)` and (B) `#H0 = (#H1 + #H2) = #N*2`.

Note however that, from a strict mathematical perspective, both expressions
are wrong. That is, because (1) the inner set of a child may be identical to
the outer set of its parent, and because (2) the inner set of any leaf is the
empty set. With that in mind, the `=` operator within the above two expressions
would have to be replaced by the `<=` operator for both expressions to evaluate
to `true` under that strict perspective.

<!-- ======================================================================= -->
## Hierarchies of sets as node trees

```
hierarchy of sets                                node tree
=============================================    =================

|-A-----------------------------------------|     A
| |-B---------------| |-H-| |-C-----------| |    =================
| | |-D-| |-E-----| | | 3 | | |-I-| |-F-| | |     B      H   C
| | | 1 | | |-G-| | | |---| | | 4 | | 5 | | |    ======     ======
| | |---| | | 2 | | |       | |---| |---| | |     D  E       I  F
| |       | |---| | |       |-------------| |       ===
| |       |-------| |                       |        G
| |-----------------|                       |
|-------------------------------------------|
```

**CLARIFICATION**
A hierarchy of sets defines the structure of a rooted (unordered) tree.

* The tree's structure has one node per set.
* The structure is not defined by the actual elements the sets contain.
* What counts is what relationship a set has with another set.

**TODO**
Note that, from a strict perspective, the node tree has loops because each
set is by definition a subset to itself. With that in mind, and except for
the root node, each node within the structure a hierarchy of sets defines
has exactly two parent nodes: (1) the node itself, and (2) another node.
However, that structure minus all the loops is a rooted (unordered) tree.

Note that the structure a hierarchy of sets defines can not have any cycles.
In order to have cycles, a parent set would also have to be a subset to one
of its descendant sets. That however is impossible because (1) any ancestor
set always has more elements than any of its descendant sets, and (2) the
hierarchy is a set of sets (i.e. it can not contain two different sets that
have identical content).

<!-- ======================================================================= -->
## Equivalency between trees and hierarchies of sets

```
node tree         hierarchy of outer sets         node tree
===========  <=>  =========================  <=>  ===========

     1            |-1---------------------|            1     
===========       | 1                     |       ===========         
 2   3   5        | |-2-| |-3-----| |-5-| |        2   3   5
    ===           | | 2 | | 3     | | 5 | |           ===
     4            | |---| | |-4-| | |---| |            4
                  |       | | 4 | |       |
                  |       | |---| |       |
                  |       |-------|       |
                  |-----------------------|
```

**CLARIFICATION**
Each rooted (unordered) node tree defines a strict hierarchy of outer sets,
and each strict hierarchy of sets defines a rooted (unordered) node tree.

Note that this equivalency will be referred to as **the set-based perspective**.

**Memory hook**
Take a piece of paper and use it to draw a rooted node tree. After that, draw
a border around that node tree. Then, draw a border around each subtree. When
done, the set of borders represents the tree's hierarchy of outer sets.
