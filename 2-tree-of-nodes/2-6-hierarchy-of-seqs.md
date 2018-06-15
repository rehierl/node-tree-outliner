
<!-- ======================================================================= -->
# A sequence-based perspective

```
tag soup    node tree    node sequence
========    =========    =============

<A>          A           [ A ]
</A>        ===
```

If a document only has a single element, then the document's node tree only
consists of that root element/node. Consequently, the tree's node sequence has
the tree's root node as its only element.

```
tag soup    node tree    node sequence
========    =========    =============

<A>          A           [ A, B ]
  B         ===
</A>         B 
```

Element A will be entered before B is entered. Hence, and with regards to the
tree's node sequence, B is subsequent to A.

```
tag soup    node tree    node sequence
========    =========    =============

<A>          A           [ A, B, D ]
  B         ======
  D          B  D
</A> 
```

B is entered before D.
The next sibling (D) of a node (B) is therefore subsequent to that node.

```
tag soup        node tree    node sequence
============    =========    ==============

<A>              A           [ A, B, C, D ]
  <B> C </B>    ======
  D              B  D
</A>            ===
                 C
```

B is entered before C, and C before D. C therefore appears in between B and D.
The next sibling (D) of a node (B) is therefore subsequent to that node and to
all of the descendants of that node.

<!-- ======================================================================= -->
## The root's inner/outer sequence of nodes

```
tag soup        node tree          node sequences of A (in enter-order)
============    ===============    ====================================

<A>              A                 [ A, B, C, D, E, F, G ] - NS
  <B> C </B>    ===============     =====================  - S1
  D              B   D   E   G         ==================  - S2
  <E> F </E>    ===     ===
  G              C       F
</A>
```

Each rooted ordered tree of nodes has one most significant node,
its root node (A).

* A root node can be understood to represent two sequences of nodes.
* The root's outer sequence (S1) is its complete node sequence.
* The root's inner sequence (S2) is the concatenation of the complete node
  sequences of its child nodes (concatenated in the order of its child nodes).
* `S1 := ([root] append S2)`
* S1 always begins with the root node.
* S2 always begins with the root's first child.
* The node sequence of a tree is identical to the outer sequence of its root.

Note that the definitions of the inner and outer sequences are based upon mere
observations. They do not define anything new other than names/references for
these particular sequences of nodes. Both sequences exist either way.

**CLARIFICATION**
A node sequence is said to be in enter-order, if all of its nodes are added
(i.e. appended) when entering the nodes. Similar to that, sequences are said
to be in exit-order, if the nodes are added when exiting the nodes.

<!-- ======================================================================= -->
## The inner/outer sequence of a node

Each node within a tree is understood to represent the root of a subtree.
And, because of that, any node can be understood to represent two sequences
of nodes: (S1) the node sequence that begins with the given node (i.e. its
outer sequence), and (S2) the concatenation of the node sequences of its
child nodes (i.e. its inner sequence).

* No outer sequence of a node is ever empty.
* An outer sequence always begins with its defining node.
* An inner sequence is empty if, and only if, its defining node is a leaf.
* An empty tree has no node and consequently no outer and no inner sequence.

The relationship between a node's inner and outer sequences:

* S2 is a strict suffix of S1.
* S1 is the parent (i.e. an ancestor) sequence of S2.
* S2 is the only child (i.e. a descendant) sequence of S1.
* There is no other (distinct) sequence in between S1 and S2.

**CLARIFICATION**
The outer sequence of a node is unique to that node.
No other node has the exact same outer sequence.

That is, because they always differ in the defining node.

**CLARIFICATION**
The inner sequence of a node is unique to that node.
No other node has the exact same inner sequence.

The inner sequences of two nodes are always different
because no two nodes can have identical inner *sets*.

Note that the outer sequence of a node is identical to the inner sequence
of its parent if, and only if, the node has no siblings.

**CLARIFICATION**
A 1:1 relationship exists between a node and its inner and outer sequences.

Note the special case of empty inner sequences of nodes. However, a node tree
could be considered to have unique empty inner sequences for each of its leaf
nodes. These can be distinguished from one another via their defining node.

**CLARIFICATION**
Each node represents its inner and its outer sequence of nodes.

One such sequence can be transformed into the other, if the defining node is
added (or removed) to (or from) the corresponding sequence.

<!-- ======================================================================= -->
## Node trees as hierarchies of sequences

```
tag soup        node tree          outer sequences (in enter-order)
============    ===============    ================================

<A>              A                 A B C D E F G - NS
  <B> C </B>    ===============    ============= - A 
  D              B   D   E   G       === = === = - B, D, E, G
  <E> F </E>    ===     ===            =     =   - C, F
  G              C       F
</A>
```

Note that the above visual representation of sequences can not adequately
represent empty inner sequences. It can not be used to accurately represent
empty inner sequences. Such visual representations can therefore only be
used to define a hierarchy of outer sequences.

The hierarchy of all inner sequences is:

```
   |------------------------------------------|
   |    |--------|           |--------|       |
   |    |    |-| |    |-|    |    |-| |   |-| |
A, | B, | C, | | | D, | | E, | F, | | | G | | |
   |    |    |-| |    |-|    |    |-| |   |-| |
   |    |--------|           |--------|       |
   |------------------------------------------|
```

* The outer sequence of a child is a subsequence
  to the inner sequence of its parent.
* Both sequences of a node are subsequences
  to any of the sequences of the node's ancestors.

With regards to the nodes within such sequences:

* Each node within the two sequences of a node is also
  an element within any of the sequences of the node's ancestors.
* No such sequence contains a node that an ancestor sequence does not contain.

The above statements should be fairly obvious because any descendant of a
node is also a descendant of the node's ancestors and as such an element of
all of the sequences of the node's ancestors.

* The node sequences (inner and outer) of all of a node's descendants
  are subsequences to the sequences of that node.
* The outer sequence of a child is identical to the inner sequence
  of its parent if, and only if, the parent has no other child.
* The outer sequence of a node never has the outer sequence of a
  descendant as its prefix.
* In contrary to that, the outer/inner sequence of a node always
  has the outer/inner sequence of its last child as its suffix.

**CLARIFICATION**
All the inner and outer sequences of all the nodes within an ordered tree
of nodes represents a hierarchy of sequences of nodes.

That is, the set of sequences is consistent with the `subsequence-of` operator
because there are no two sequences that overlap each other. For each pair of
sequences, it can be determined that they are either independent from one
another, or that one sequence is a subsequence of the other.

Note that each rooted ordered tree represents exactly one such hierarchy.

<!-- ======================================================================= -->
## Equivalency between trees and hierarchies of sequences

```
outer sequences
enter-order                       node tree
==============================    =================

A B D G E H C I F - NS             A               
================= - A             =================
  ======= = ===== - B, H, C        B      H   C    
    === =     = = - D, E, I, F    ======     ======
      =           - G              D  E       I  F 
                                  ===
                                   G
```

Given the above set of sequences, and without any additional information (i.e.
which node within a sequence is its defining node), the initial node tree can
be reconstructed. In order to reconstruct the initial tree, one has to know
(1) the parent sequence and (2) the next/previous sibling of each sequence.

The relevant steps to read a tree from such a hierarchy are:

* (1) Determine the root sequence.
* Note that the root sequence alone is not sufficient to reconstruct the tree.
* (2) Determine the parent sequence of each sequence.
* Note that each sequence is shorter than its parent sequence.
* (3) Determine the node order based on the starting position of each sequence.
* Note that each sequence has a unique position within the root sequence.
* Note that the position of each sequence corresponds with the node order.
* Note that this step fixes the order of child nodes within each parent.

Note that, in order to create a rooted ordered tree of nodes from a hierarchy
of sequences, that hierarchy must fulfill certain requirements. For example:

* A hierarchy of N sequences always has one root sequence of length N.
* The longest sequence therefore is the root sequence.
* All other (N-1) sequences have less than N elements.
* Each of the (N-1) subsequences have unique offsets within the root sequence.
* Note that there is one sequence per node.

**CLARIFICATION**
A rooted ordered tree can be created based on a hierarchy of outer sequences,
if the hierarchy contains one sequence per node.

Note that each hierarchy of sequences
represents exactly one rooted ordered node tree.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Each rooted ordered tree of nodes represents a hierarchy of sequences,
and each hierarchy of sequences represents a rooted ordered tree of nodes.

**CLARIFICATION**
The hierarchy of sequences of a rooted ordered tree of nodes will be
referred to as the tree's "sequence-based perspective".
