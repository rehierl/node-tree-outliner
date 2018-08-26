
<!-- ======================================================================= -->
# Unordered tree => Hierarchy of sets

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

Note the outer box S0 which contains all the nodes of the tree.
It contains the tree's root node and all of its descendants.

**CLARIFICATION**
A tree is a binary tuple defined as follows:

* `T := (N,E)` where `(E subset-of NxN)`
* `e := (n1,n2)` such that `(e in E)`,
  iff (`n1` is the parent node of `n2`)
* `N` is the set of nodes
* `E` is the set of edges

Note that this discussion is with regards to directed un-ordered trees.

**CLARIFICATION**
As a whole, any tree can be understood to define its set of nodes.

Note that the following discussion focuses on the tree's set of nodes and on
subsets of that set. The set of edges E is therefore only taken into account
as a formal basis that defines these sets via "all the nodes that are directly
connected". Because of that, the following subsets are understood to be defined
by a node that acts as the starting point of a formal definition.

Note that the definitions of these sets of nodes are based upon observations.
The following definitions therefore merely introduce names for these particular
sets of nodes. Similar to the subset of uneven integers, these subsets don't
exist as separate entities, but as integral parts of the tree's set of nodes.

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
Any node can therefore be understood to define two sets of nodes: (1) The
outer set of a node S1 contains the node and all of its descendants, and
(2) the inner set of a node S2 only contains the descendants of that node.

* A tree's set of nodes is identical to the outer set of its root.
* An outer set always contains its defining node (i.e. never empty).
* An inner set is empty `{}`, iff its defining node is a leaf.

The relationship between both sets:

* `S1 = ({ node } union S2)`
* S1 is a strict super-set of S2.
* S1 is super-ordinate to S2 and S2 is sub-ordinate to S1.
* S1 is the parent (i.e. an ancestor) set of S2.
* S2 is the only child (i.e. a descendant) set of S1.

Note that each set can be transformed into the other,
if the defining node is added to (or removed from) the other set.

**CLARIFICATION**
Each node can be understood to contain itself and its descendants.

Other ways to express that statement are: node `n1` contains node `n2`,
iff (1) `n2` is a node of the subtree that has `n1` as its root,
or (2) `n1`'s outer set contains `n2`.

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

* The inner set of a parent is the union of the outer sets of its child nodes.
* The inner set of a parent is a superset to the outer set of a child.
* The outer set of a child is sub-ordinate to the inner set of its parent.
* Both sets of a descendant are subsets to both sets of an ancestor.
* No set of a descendant contains a node that an ancestor set does not contain.

The above statements should be fairly obvious because any descendant of a node
is also a descendant of the node's ancestors. As such, a descendant is also an
element of both sets of any of the node's ancestors.

* If a parent has one child only, then the parent's inner set is identical to
  the child's outer set. Both sets are strict subsets to the parent's outer set.
* If a parent has more than one child, then the parent's inner set holds more
  nodes than any of the outer sets of its child nodes. That is, the outer set
  of any child is a strict subset of the parents's inner set.
* It is the outer sets of its siblings that distinguishes
  the outer set of a child from the inner set of its parent.

Note that the outer set of a node is the set of nodes of the subtree that has
the node as its root (i.e. a tree). In contrary to that, the inner set of a
node is the union of the outer sets of those subtrees that have the node's
child nodes as their root (i.e. a forest).

<!-- ======================================================================= -->
## The set of outer sets

**CLARIFICATION**
Each outer set contains its defining node.
That is, no node has an empty outer set.
(=> the set of outer sets is a simple setup).

**CLARIFICATION**
The outer sets of two distinct nodes are either disjoint,
ex-or one outer set is a strict subset of the other.
(=> the set of outer sets is a strict setup).

(1) If node `n1` is an ancestor of `n2`, then any descendant of `n2` is also
a descendant of `n1`. The outer set of `n2` is therefore a subset of the outer
set of `n1`. That is, the outer set of `n2` does not contain any node that is
not also an element of the outer set of `n1`.

(2) If node `n1` is an ancestor of `n2`, then the outer set of `n1` has `n1`
as an element, but the outer set of `n2` does not. The outer set of an ancestor
has always more elements than the outer set of a descendant. That is, the outer
set of a descendant is a strict subset of the outer set of an ancestor.

(3) If two nodes are unrelated to one another (i.e. none is an ancestor of the
other), then the outer sets of both nodes are disjoint. That is, both sets have
no nodes in common.

**CLARIFICATION**
The set of outer sets always has exactly one root set.
(=> the set of outer sets is a simple hierarchy).

That is because the set of outer sets always has exactly one root set,
which is because a node tree is by definition a rooted tree of nodes.

Note that any other outer set is a strict subset to the outer set of the root.
That is because any other node in a tree is a descendant of the root node.

**CLARIFICATION**
Each outer set has its defining node as its only CE.
(=> the set of outer sets is a strict hierarchy).

The inner set of a node is the union of the outer sets of its child nodes.
Because of that, the defining node is the only node that remains after
subtracting the inner set of a node from its the outer set.

**CLARIFICATION**
The outer set of a node is unique to a node.
No other node has the exact same outer set.
(=> #P == #V)

(1) If node `n1` is an ancestor of `n2`, then `n1`'s outer set contains `n1`,
but `n2`'s outer set does not. The outer sets of both nodes are different.

(2) If the outer sets of two nodes are disjoint, then the outer sets of both
nodes have no nodes in common. That is, the outer sets of two unrelated nodes
are different.

Note that this is also a consequence of each outer set having its defining
node as its only CE. Which is, because any CSS is disjoint to any other CSS.

**CLARIFICATION**
The **set of outer sets** of a node tree is **a strict hierarchy of sets**.

**Memory hook**
Take a piece of paper and use it to draw a rooted node tree. Next, draw a border
around that node tree. Then, draw a border around each subtree such that no
border crosses another border. When done, the set of borders represents the
tree's hierarchy of outer sets H1.

<!-- ======================================================================= -->
## The set of inner sets

Note that no inner set will contain the root node.

Note that all inner sets of leaf nodes are empty `{}` and that: (a) the empty
set is disjoint to any other set - (b) the empty set is a subset to any other
set - (c) the empty set is a strict subset to any non-empty set - (d) the empty
set is not a strict subset to itself.

**CLARIFICATION**
The inner sets of a leaf nodes are empty.
(=> the set of inner sets is no simple setup).

**CLARIFICATION**
The non-empty inner sets of two distinct nodes are either disjoint,
ex-or one inner set is a strict subset of the other.
(=> the set of inner sets is no strict setup).

(1) If node `n1` is an ancestor of `n2`, then the inner set of `n2` is a subset
of the inner set of `n1`. (Note that this is true, even if `n2` is a leaf node:
`n1` has a non-empty inner set, `n2` has an empty inner set).

(2) If node `n1` is an ancestor of `n2`, then the inner set of `n1` has `n2`
as an element, but the inner set of `n2` does not. The inner set of an ancestor
has always more elements than the inner set of a descendant. That is, the inner
set of a descendant is a strict subset of the inner set of an ancestor. (Note
that this is true, even if `n2` is a leaf node).

(3) If two nodes are unrelated to one another (i.e. none is an ancestor of the
other), then the inner sets of both nodes are disjoint. That is, both sets have
no nodes in common.

**CLARIFICATION**
But what if the inner set of `n1` and/or the inner set of `n2` is empty?

* `(A ex-or B) := (A && !B) || (!A && B)`
* `A` means that "both sets are disjoint"
* `B` means that "one set is a strict subset of the other"

(`n1` and `n2` are both parent nodes) =>
(A ex-or B) is obviously true.

(`n1` and `n2` are both leaf nodes) =>
Both empty inner sets are obviously disjoint. In addition to that, none of the
empty inner sets is a strict subset of the other. Consequently, (A ex-or B) is
true.

(`n1` is a parent, `n2` is a leaf) =>
Both sets are disjoint. However, the empty inner set of `n2` is also a strict
subset of the non-empty inner set of `n1`. Because of that, (A ex-or B) does
not apply. (Note that `n2`'s empty inner set is always a strict subset of
`n1`'s inner set. That is, whether `n1` is an ancestor of `n2` or not).

**CLARIFICATION**
The set of inner sets is not guaranteed to have a non-empty root set.
(=> the set of inner sets is no simple hierarchy).

That is because a node tree that has only one root node will result in a set of
inner sets that only holds the empty set as its only element. Which is because
in that case, the root node is by definition also a leaf node.

**CLARIFICATION**
The CSS of each inner set is not guaranteed to hold one node only.
(=> the set of inner sets is no strict hierarchy).

(1) The CSS of the inner set of a leaf node is obviously empty.

(2) The CSS of the inner set of a parent node may hold once CE per child.
Because of that, the CSS is a non-empty CSS that holds one or more elements.

**CLARIFICATION**
The non-empty inner set of a node is unique to that node.
No other node has the exact same non-empty inner set.

(1) If node `n1` is an ancestor of `n2`, then `n1`'s inner set contains `n2`,
but `n2`'s inner set does not. The inner sets of both nodes are different.

(2) If the inner sets of two non-leaf nodes are disjoint, then the inner sets
of both nodes have no nodes in common. That is, the inner sets of two unrelated
nodes are different.

**CLARIFICATION**
The inner set of a node is not unique to a node.
(=> #P <= #N)

(1) If a tree has more than one leaf node, then more than one node has the
empty set as its inner set. Because of that, the set of inner sets will hold
fewer sets than the tree has nodes.

**CLARIFICATION**
The set of inner sets of a node tree does not represent a strict hierarchy.

<!-- ======================================================================= -->
## derived statements

```
       |-os(n)-----------------|
       | |-css(n)-| |-is(n)--| |
A(n) <---| { .. } | | { .. } |---> D(n)
       | |--------| |--------| |
       |-----------------------|
```

Note that, similar to the inner/outer subset of a set (i.e. `oss(s)`, `iss(s)`),
the CSS/CE of a node's outer set (`css(n)`/`ce(n)` in `os(n)`) can be understood
to bind the outer set of a node to the node's ancestors. Likewise, the outer
sets of the node's descendants are bound to the inner set (`is(n)`) of that node.
