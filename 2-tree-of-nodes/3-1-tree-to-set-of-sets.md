
<!-- ======================================================================= -->
# Creating a hierarchy of sets for an unordered node tree

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
A tree is a binary tuple defined as follows:

* `T := (N,E)`
* `N` is the set of nodes and `E` the set of edges
* `e := (n1,n2)`, `e in E`, `E subset-of NxN`
* `(n1,n2) in E` is true, if `(n1 parent-of n2)` is true

Note that this discussion is with regards to rooted un-ordered trees.

**CLARIFICATION**
As a whole, a tree can be understood to define its set of nodes.

Note that the following discussion focuses on the tree's set of nodes and on
subsets of that set. The set of edges E is therefore only taken into account
as a formal basis that defines these sets via "all the nodes that are connected
in a certain way". Because of that, the following (sub-)sets are understood to
be defined by a node that acts as the starting point of a formal definition.

Note that the definitions of these sets of nodes are based upon observations.
They do not define anything new other than names/references for these particular
sets of nodes. These (sub-)sets don't exist as separate entities, but as a part
of the tree's set of nodes.

<!-- ======================================================================= -->
## The inner/outer set of a node

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

Each node within a tree can be understood to represent the root of a subtree.
Any node can therefore be understood to define two sets of nodes: (1) The outer
set of a node S1 contains the node and all of its descendants, and (2) the inner
set of a node S2 only contains the descendants of that node.

* A tree's set of nodes is identical to the outer set of its root.
* An outer set always contains its defining node (i.e. never empty).
* An inner set is empty, if its defining node is a leaf.

The relationship between both sets:

* `S1 = (node union S2)`
* As a strict subset, S2 is a strict subset of S1.
* S1 is super-ordinate to S2 and S2 sub-ordinate to S1.
* S1 is the parent (i.e. an ancestor) set of S2.
* S2 is the only child (i.e. a descendant) set of S1.

Note that each set can be transformed into the other,
if the defining node is added to (or removed from) the other set.

**CLARIFICATION**
Each node can be said to contain itself and its descendants.

Other ways to express that statement are: (1) node `n1` contains node `n2`,
if `n2` is a node of the subtree that has `n1` as its root. Or (2) `n1`'s
outer set contains `n2`.

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

* The outer set of a child is a subset of the inner set of its parent.
* The outer set of a child is sub-ordinate to the inner set of its parent.
* Both sets of a node are subsets to any set of any of the node's ancestors.
* None of those sets contains a node that an ancestor set does not contain.
* The inner set of a node is the union of the outer sets of its child nodes.

The above statements should be fairly obvious because any descendant of a node
is also a descendant of the node's ancestors and, as such, also an element of
any set of any of the node's ancestors.

* If a node has one child only, then the node's inner set is identical to
  the child's outer set, which are strict subsets of the node's outer set.
* If a node has more than one child, then the node's inner set has always
  more nodes than any of the outer sets of its child nodes.
* It is the outer sets of its siblings that distinguishes the outer set
  of a child from the inner set of its parent.

<!-- ======================================================================= -->
### Outer sets of different nodes

**CLARIFICATION**
The outer sets of two distinct nodes are either disjoint,
ex-or one outer set is a strict subset of the other.

(0) If node `n1` is an ancestor of `n2`, then any descendant of `n2` is also a
descendant of `n1`. The outer set of `n2` is therefore a subset of the outer
set of `n1`. That is, the outer set of `n2` does not have any node that is not
also an element of the outer set of `n1`.

(1) If node `n1` is an ancestor of `n2`, then the outer set of `n1` has `n1`
as an element, but the outer set of `n2` does not. The outer set of an ancestor
always has more elements than the outer set of a descendant. That is, the outer
set of a descendant is a strict subset of the outer set of an ancestor.

(2) If node `n1` is not an ancestor of `n2`, and `n2` not an ancestor of `n1`,
then the outer sets of both nodes are disjoint.

Note that no node in a tree has an empty outer set.

**CLARIFICATION**
The outer set of a node is unique to that node.
No other node has the exact same outer set.

If the outer sets of two nodes are disjoint, then the outer sets of both nodes
have no nodes in common. That is, both outer sets are different.

If node `n1` is an ancestor of `n2`, then `n1`'s outer set contains `n1`, but
`n2`'s outer set does not. The outer sets of both nodes are different.

**CLARIFICATION**
Node `n1` is said to be **disjoint** from `n2`,
if the outer sets of both nodes are disjoint.

* The subtrees of both nodes have no nodes in common.
* `n1` does not contain `n2`, and `n2` does not contain `n1`.
* `n1` is not an ancestor of `n2`, and `n2` not an ancestor of `n1`.

Note that two nodes in a tree are either disjoint,
ex-or one node is an ancestor of the other.

**CLARIFICATION**
Node `n1` is said to be **coupled** with `n2`,
if the outer sets of both nodes are not disjoint.

* coupled <=> not disjoint

<!-- ======================================================================= -->
### Inner sets of different nodes

Note that the arguments needed to proof the following statements are largely
the same as those needed to proof the statements with regards to outer sets.

Note that the inner sets of leaf nodes are empty and that: (a) the empty set is
disjoint from any other set - (b) the empty set is a subset to any other set -
(c) the empty set is a strict subset to any non-empty set - (d) the empty set
is not a strict subset to itself.

**CLARIFICATION**
The non-empty inner sets of two distinct nodes are either disjoint,
ex-or one inner set is a strict subset of the other.

(0) If node `n1` is an ancestor of `n2`, then the inner set of `n2` is a subset
of the inner set of `n1`. (Note that this is true, even if `n2` is a leaf node:
`n1` has a non-empty inner set, `n2` has an empty inner set).

(1) If node `n1` is an ancestor of `n2`, then the inner set of `n1` has `n2`
as an element, but the inner set of `n2` does not. The inner set of an ancestor
always has more elements than the inner set of a descendant. That is, the inner
set of a descendant is a strict subset of the inner set of an ancestor. (Note
that this is true, even if `n2` is a leaf node).

(2) If node `n1` is not an ancestor of `n2`, and `n2` not an ancestor of `n1`,
then the inner sets of both nodes are disjoint. (Note that this is true, even
if `n1` and/or `n2` are leaf nodes: an empty inner set is disjoint from any
other set).

Note that, similar to ex-or statement with regards to the outer sets, this ex-or
statement is true for all non-empty inner sets. But what if both of inner sets
are empty at the same time? And what if only one of those inner sets is empty?

* `(A ex-or B)` is true, if `(A && !B) || (!A && B)` is true
* `A` means that "both sets are disjoint"
* `B` means that "one set is a strict subset of the other"

(`n1` and `n2` are both parent nodes):
As both sets are non-empty, the above statement is true (see 0-2).

(`n1` and `n2` are both leaf nodes):
Both empty inner sets are disjoint. In addition to that,
none of the empty inner sets is a strict subset of the other.

(`n1` is a parent, `n2` is a leaf):
Both sets are disjoint. However, the empty inner set is also a strict subset
of the non-empty inner set. Because of that, both sub-statements (A and B) may
be true at the same time. The ex-or statement is therefore not true in general,
if the empty inner sets of leaf nodes are included. Consequently, the ex-or
statement must exclude the empty inner sets of leaf nodes.

**CLARIFICATION**
The non-empty inner set of a node is unique to that node.
No other node has the exact same non-empty inner set.

If the inner sets of two non-leaf nodes are disjoint, then the inner sets of
both nodes have no nodes in common. That is, if one node is not an ancestor of
the other, then the inner sets of both nodes are different.

If node `n1` is an ancestor of `n2`, then `n1`'s inner set contains `n2`, but
`n2`'s inner set does not. The inner sets of both nodes are different.

<!-- ======================================================================= -->
## Node trees as hierarchies of sets

Assumed that a tree is non-empty (i.e. has a root node) ...

* H1 - The set of sets which only contains
       the outer sets of all the nodes in the tree.
* H2 - The set of sets which only contains
       the inner sets of all the nodes in the tree.
* H2* - `H2* := (H2 - {})`
* H0  - `H0 := (H1 union H2)`
* H0* - `H0* := (H1 union H2*)`

Note that in H0 (a set of sets), the inner set of a parent is merged with the
outer set of its single child. That is, H0 contains one set which represents
the parent's inner set and the child's outer set.

**CLARIFICATION**
Unordered trees define (simple) hierarchies of sets: H1, (H2*), H0*.

```
          \  Hx  |     |     |     |     |     |
setup      \     | H1  | H2  | H2* | H0  | H0* | (comment)
-----------------|-----|-----|-----|-----|-----|-----------------------
consistent setup | +   | +   | +   | +   | +   | (strict-) subset-of
-----------------|-----|-----|-----|-----|-----|-----------------------
strict setup     | +   | -   | +   | -   | +   | does not contain {}
-----------------|-----|-----|-----|-----|-----|-----------------------
simple hierarchy | +   | -   | -/+ | -   | +   | has one root set only
```

consistent setup:

* H1, H2, H2*, H0 and H0* are by definition consistent setups.

strict setup:

* H2 and H0 contain the empty set, because any non-empty tree
  always has one or more leaf nodes, which have empty inner sets.
* By definition, H1, H2* and H0* do not contain the empty set.
* H1, H2* and H0* represent strict setups.

simple hierarchy:

* H1 and H0* always have exactly one root set (i.e. the root's outer set).
* H2* is not a hierarchy, because if the node tree only has a single node,
  then H2* will be an empty set of sets. If however the node tree has two
  or more nodes, then H2* will also always have exactly one root set.
* H1 and H0* always represent simple hierarchies.
* H2* represents a simple hierarchy only if `(#N > 1)`.

**Memory hook**
Take a piece of paper and use it to draw a rooted node tree. After that, draw
a border around that node tree. Then, draw a border around each subtree. When
done, the set of borders represents the tree's hierarchy of outer sets H1.

<!-- ======================================================================= -->

H1

* the defining node of an outer set is an element of the outer set
  and an element of all outer sets that are ancestral to it
* the defining node of an outer set is not an element of any
  descendant outer set
* the CSS of an outer set is never empty,
  it always contains the defining node as its only element
* `(css(s) = 1)` is guaranteed for any `s in P`
* H1 is by design a strict hierarchy

H2*

* the CSS of the inner set of a parent node
  has one or more nodes, i.e. the parent's child nodes
* H2* does not contain the empty inner set of a leaf node
* H2* is not a strict hierarchy

H0*

* the CSS of the inner set of a parent node,
  that has one child only, contains the child node
* the CSS of the inner set of a parent node,
  that has more than one child, is empty because
  H0* still contains the outer sets of these child nodes
* the CSS of the outer set of a leaf node contains the leaf node
* H* does not contain the inner set of a leaf node (empty set)
* H0* is not a strict hierarchy
