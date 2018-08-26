
**TODO** - (open aspects)

<!-- ======================================================================= -->
# Ordered tree => Hierarchy of sequences

<!-- ======================================================================= -->
## A sequence-based perspective

Note that the following discussion is based upon rooted ordered trees.

```
tag soup      node tree      node sequence
========  =>  =========  =>  =============

<A>            A             [ A ]
</A>          ===
```

If a document has a single element, then the document's node tree has that
element as its only node. The tree's node sequence therefore has the tree's
root node as its only element.

```
tag soup      node tree      node sequence
========  =>  =========  =>  =============

<A>            A             [ A, B ]
  B           ===
</A>           B 
```

A tree's root node will be entered first. Node A is therefore entered before
B. Because of that, B is subsequent to A.

```
tag soup      node tree      node sequence
========  =>  =========  =>  =============

<A>            A             [ A, B, D ]
  B           ======
  D            B  D
</A> 
```

B is entered before D. The next sibling D of node B is therefore subsequent
to its previous sibling B.

```
tag soup          node tree      node sequence
============  =>  =========  =>  ==============

<A>                A             [ A, B, C, D ]
  <B> C </B>      =======
  D                B   D
</A>              ===
                   C
```

B is entered before C, and C before D. C therefore appears in between B and D.
The next sibling D of node B is consequently subsequent to its previous sibling
B and all of its descendants.

Note that each node sequence generated as above represents an ordered set of
nodes. That is because any node within such a sequence appears exactly once.
In addition to that, the position of each node is consistent with the
corresponding node order (e.g. enter-order).

**CLARIFICATION**
A sequence of nodes is said to be in **enter-order**, if all of its nodes
are added (i.e. appended) to the sequence when entering each node. Similar
to that, sequences are said to be in **exit-order**, if the nodes are added
when exiting each node.

Note that any sequence mentioned in the course of this discussion is by
default in enter-order.

<!-- ======================================================================= -->
## The root's inner/outer sequence of nodes

```
tag soup          node tree            node sequences of A
============  =>  ===============  =>  ============================

<A>                A                   [ A, B, C, D, E, F, G ] - NS
  <B> C </B>      ===============       =====================  - S1
  D                B   D   E   G           ==================  - S2
  <E> F </E>      ===     ===
  G                C       F
</A>
```

Each tree has its root as its most significant node.

* Root A can be understood to define two sequences of nodes.
* The root's outer sequence (S1) is the root's complete node sequence.
* The root's inner sequence (S2) is its node sequence without the root itself.
* The node sequence of a tree is identical to the outer sequence of its root.

Note that the definitions of the inner and outer sequences are based upon mere
observations. They do not define anything new other than names/references for
these particular sequences of nodes. Both sequences exist either way.

<!-- ======================================================================= -->
## The inner/outer sequence of a node

Each node within a tree is understood to represent the root of a subtree.
And, because of that, any node can be understood to define two sequences of
nodes: (1) A node's outer sequence S1 is the node sequence of the subtree
that has the node as its root. (2) A node's inner sequence S2 is the node's
outer sequence S2 without the node itself.

* `S1 := (node append S2)`
* An outer sequence always begins with its defining node (i.e. never empty).
* An inner sequence is empty if (and only if) its defining node is a leaf.
* A non-empty inner sequence contains all child nodes of the defining node.
* A non-empty inner sequence begins with the node's first child.
* An empty tree has no node and consequently no outer and no inner sequence.

The relationship between both sequences:

* S2 is a strict suffix of S1.
* A node's inner sequence is embedded into its outer sequence.
* S1 is super-ordinate to S2 and S2 sub-ordinate to S1.
* S1 is the parent (i.e. an ancestor) sequence of S2.
* S2 is the only child (i.e. a descendant) sequence of S1.
* There is no other (distinct) sequence in between S1 and S2.

Note that each sequence can be transformed into the other,
if the defining node is added to (or removed from) the other sequence.

**CLARIFICATION**
Each node can be said to contain all of its descendants.

Other ways to express that statement would be: (1) node `n1` contains node `n2`,
if (and only if) `n2` is an element of the node sequence that `n1` defines. Or
(2) `n1`'s outer sequence contains `n2`.

<!-- ======================================================================= -->
## Relationship between sequences of different nodes

```
node tree            outer sequences
===============  =>  ==========================

 A                   A B C D E F G - A
===============        === = === = - B, D, E, G
 B   D   E   G           =     =   - C, F
===     === 
 C       F
```

Recall that the line-based visualization can not accurately represent empty
inner sequences. Such visual representations can therefore only be used to
represent a tree's hierarchy of outer sequences.

The tree's hierarchy of inner sequences:

```
   |------------------------------------------|
   |    |--------|           |--------|       |
   |    |    |-| |    |-|    |    |-| |   |-| |
A, | B, | C, | | | D, | | E, | F, | | | G | | |
   |    |    |-| |    |-|    |    |-| |   |-| |
   |    |--------|           |--------|       |
   |------------------------------------------|
```

* The outer sequence of a child
  is a subsequence to the inner sequence of its parent.
* the outer sequence of a child
  is sub-ordinate to the inner sequence of its parent.

Note that, even though both sequences have different defining nodes, the outer
sequence of a child is identical to the inner sequence of its parent, if (and
only if) the parent has no other child. That is, the child has no siblings.

* Both sequences of a node are subsequences
  to any sequence of any of the node's ancestors.
* None of those contains a node that an ancestor sequence does not contain.
* The inner sequence of a node is the concatenation of
  all of the outer sequences of its child nodes.

The above statements should be fairly obvious because any descendant of a
node is also a descendant of the node's ancestors and as such an element of
all of the sequences of the node's ancestors.

* (if empty inner sequences are ignored, then ...)
* The outer/inner sequence of a node never has
  the outer/inner sequence of its first child as its prefix.
* The outer/inner sequence of a node always has
  the outer/inner sequence of its last child as its suffix.

That is, if the empty inner sequences of leaf nodes are ignored, then the root
sequence of such a hierarchy has a suffix, but no prefix within the hierarchy.
Put differently, there never are two sequences within a hierarchy that begin
with the same node, but there always are two or more sequences that end with
the same node.

**CLARIFICATION**
The outer sequence of a node is unique to that node.
No other node has the exact same outer sequence.

The outer sequences of two nodes are always different
because no two nodes have identical *outer sets*.

**CLARIFICATION**
The inner sequence of a node is unique to that node.
No other node has the exact same inner sequence.

The inner sequences of two nodes are always different
because no two nodes have identical *inner sets*.

**CLARIFICATION**
Each node defines its very own inner and outer sequences of nodes.

Note the special case of empty inner sequences of nodes. However, a node tree
could be considered to have unique empty inner sequences for each of its leaf
nodes. These can be distinguished from one another via their defining node.

**CLARIFICATION**
The inner sequence of a node is identical to the outer sequence of its
*only child*.

That is because the outer sequence of a descendant is in general only a simple
subsequence (not a strict subsequence) of the inner sequence of an ancestor.

Note that, if the parent has more than one child, this identity does not exist.

<!-- ======================================================================= -->
## Node trees as hierarchies of sequences

**CLARIFICATION**
The set of sequences (H0), that holds all the inner and all the outer sequences
of all of the nodes within a tree, represents a hierarchy of sequences.

That is, the set of sequences is consistent with the `subsequence-of` operator
because there are no two sequences that overlap each other. For each pair of
sequences, it can be determined that they are either independent from one
another, or that one sequence is a subsequence of the other.

Note that the same applies to the set of sequences (H1), which only contains
the outer sequences of all the nodes, and the set of sequences (H2), which
only contains the inner sequences of these nodes (i.e. `H0 = (H1 union H2)`).

Note that even though H0 is only a (simple) hierarchy of sequences, H1 and H2
both are on their own strict hierarchies of sequences. That is because any
ancestor inner/outer sequence has more elements than any of its descendant
inner/outer sequences.

**CLARIFICATION**
The complete hierarchy of a tree (H0) is considered to hold two sequences per
node, which can be distinguished via their defining nodes and some boolean
`isOuterSequence` property. That is, the following two expressions are both
considered to hold: (A) `(#H2 = #N)` and (B) `#H0 = (#H1 + #H2) = #N*2`.

Note however that, from a strict mathematical perspective, both expressions are
wrong. That is because (1) the inner sequence of a child may be identical to the
outer sequence of its parent, and because (2) the inner sequence of any leaf is
the empty sequence. With that in mind, the `=` operator within the above two
expressions would have to be replaced by the `<=` operator for both expressions
to evaluate to `true` under that strict perspective.

**CLARIFICATION**
A node tree represents a hierarchy of sequences (H0).

Note that any subset of H0 represents a forest of such hierarchies. However,
and under certain circumstances, such a subset may still represent a single
hierarchy (e.g. H1 and H2).

Note that the node sequence of any rooted ordered tree represents an ordered
set of values. H0, and any subset of it, automatically represent distinct setups
(/see/ "requirement 1" in "consistent set of sequences" /). However, this can
only be guaranteed if (and only if) the initial tree has neither loops nor
cycles.
