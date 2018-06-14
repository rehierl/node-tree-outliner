
<!-- ======================================================================= -->
# A sequence-based perspective

```
tag soup    node tree    node sequence
========    =========    =============

<A>          A           [ A ]
</A>        ===
```

If a document only has a single element, then the document's node tree only
consists of that root node. Because of that, the tree's node sequence has
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

The next sibling of a node is subsequent to that node.

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
The next sibling of a node is therefore subsequent to that node and to all of
its descendants.

<!-- ======================================================================= -->
## The root's inner/outer sequence of nodes

```
tag soup        node tree          node sequences of A
============    ===============    =======================

<A>              A                 [ A, B, C, D, E, F, G ] - NS
  <B> C </B>    ===============     =====================  - S1
  D              B   D   E   G         ==================  - S2
  <E> F </E>    ===     ===
  G              C       F
</A>
```

Each rooted ordered tree of nodes has exactly one most significant node, its
root node (A).

* A root node can be understood to represent two sequences of nodes.
* The root's outer sequence (S1) is the root node's complete node sequence.
* The root's inner sequence (S2) is the concatenation of the node sequences
  of its child nodes (concatenated in the order of its child nodes).
* `S1 := ([root] append S2)`
* S1 always begins with the root node.
* S2 always begins with the root's first child.
* The node sequence of a tree is identical to the outer sequence of its root.

Note that the definitions of the inner and outer sequences are based upon mere
observations. They do not define anything new other than names/references for
these particular sequences of nodes. Both sequences exist either way.

<!-- ======================================================================= -->
## The inner/outer sequence of a node

Each node within a tree is understood to represent the root of a subtree.
And, because of that, any node can be understood to represent two sequences
of nodes: (S1) the node sequence that begins with the given node, and
(S2) the concatenation of the node sequences of its child nodes.

* No outer sequence of a node is ever empty.
* Any outer sequence always begins with its defining node.
* An inner sequence is empty if, and only if, its defining node is a leaf.
* An empty tree has no node and consequently no outer and no inner sequence.

The relationship between a node's inner and outer sequences:

* S2 is a suffix of S1.
* S1 is the parent (i.e. an ancestor) sequence of S2.
* S2 is the only child (i.e. a descendant) sequence of S1.
* There is no other distinct sequence in between S1 and S2.

**CONCLUSION**
The outer sequence of a node is unique to that node.
No other node has the exact same outer sequence.

That is, because they always differ in the defining node.

**CONCLUSION**
The inner sequence of a node is unique to that node.
No other node has the exact same inner sequence.

The inner sequences of two nodes are always different because the inner sets
of those nodes are different. The node order would have to be taken into account
if, any only if, two nodes could exist that have identical inner sets. That
however is never the case.

Note the special case of empty inner sequences.

Note that the outer sequence of a node is identical to the inner sequence
of its parent if, and only if, the node has no siblings.

**CONCLUSION**
Each node represents its inner and its outer sequence of nodes.

Note that each sequence can be transformed into the other, if the defining node
is added to (or removed from) the beginning of the corresponding sequence.

<!-- ======================================================================= -->
## Node trees as hierarchies of sequences

```
tag soup        node tree          all outer sequences
============    ===============    ==========================

<A>              A                 A B C D E F G - NS
  <B> C </B>    ===============    ============= - A 
  D              B   D   E   G       === = === = - B, D, E, G
  <E> F </E>    ===     ===            =     =   - C, F
  G              C       F
</A>
```

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
* Each node within the two sequences of a node is also
  an element within any of the sequences of the node's ancestors.
* No such sequence contains a node that an ancestor sequences does not contain.

The above statements should be fairly obvious because any descendant of a node
is also a descendant of the node's ancestors and as such an element of all of
the sequences of the node's ancestors.

* The node sequences (inner and outer) of all of a node's descendants
  are subsequences to the sequences of that node.
* The outer sequence of a child is identical to the inner sequence of its
  parent if, and only if, the parent has no other child.
* The outer sequence of a node never has the outer sequence of a descendant
  as its prefix. In contrary to that, the outer sequence of a node always
  has the outer sequence of one of its child nodes as its suffix.

Note the special case of empty inner sequences of nodes. Also note that a node
tree has unique empty inner sequences for each of its leaf nodes. These empty
sequences can be identified via their defining leaf node.

<!-- ======================================================================= -->
## Equivalency between trees and hierarchies of sequences

```
node tree            outer sequences
=================    ==============================

 A                   A B D G E H C I F - NS
=================    ================= - A
 B      H   C          ======= = ===== - B, H, C
======     ======        === =     = = - D, E, I, F
 D  E       I  F           =           - G
===
 G
```

* In a hierarchy of N sequences, there must be a sequence of length N.
* All other (N-1) sequences must be less than N elements long.
* The longest sequence is the root sequence.

Given the above set of sequences, and without any additional information (i.e.
which node within a sequence is its defining node), the initial node tree can
be reconstructed. In order to reconstruct the initial tree, one has to know
(1) the parent sequence and (2) the next/previous sibling of each sequence.

The relevant steps therefore are:

* (1) Determine the root sequence.
* Note that the root sequence alone is not sufficient to reconstruct the tree.
* (2) Determine the parent sequence of each sequence.
* Note that each descendant sequence is shorter than its parent sequence.
* (3) Determine the node order based on the position of each sequence.
* Note that each sequence has a unique position within the root sequence.
* Note that the position of each sequence corresponds with the node order.
* Note that this last step fixes the order of child nodes within each parent.

**CONCLUSION**
Each rooted ordered tree of nodes represents a hierarchy of sequences,
and each hierarchy of sequences represents a rooted ordered tree of nodes.

Note that these hierarchies of sequences are consistent with the definition
of subsequences of elements. That is, none of these sequences overlap: One
sequence either is embedded into another sequence, or both sequences have
no nodes in common.

Note that the sequences of sibling nodes have no nodes in common. They
are said to be independent from one another. The same applies to any two
subsequences of independent subtrees.

**CONCLUSION**
The hierarchy of sequences of a rooted ordered tree of nodes will be
referred to as the tree's "sequence-based perspective".

<!-- ======================================================================= -->
## What if the node order would correspond with the exit-order instead?

Each node can still be understood to represent two sequences of nodes: (S1) the
sequence that begins with the descendants of a node and that ends in the node
itself, and (S2) the sequence that only contains the node's descendants and
that does not end in the node itself.

Note that, instead of being a suffix, S2 is now a prefix of S1.

Note that the exit-order states that ancestors are subsequent to their
descendants. In contrary to that, the enter-order states that descendants
are subsequent to their ancestors.

```
                     outer sequences      outer sequences
node tree            enter-order          exit-order
=================    =================    ==============================

 A                   A B D G E H C I F    G D E B H I F C A - NS
=================    =================    ================= - A
 B      H   C          ======= = =====    ======= = =====   - B, H, C
======     ======        === =     = =    === =     = =     - D, E, I, F
 D  E       I  F           =              =                 - G
===
 G
```

Given the above set of sequences, and without any additional information (i.e.
which node within a sequence is its defining node), the initial node tree can
still be reconstructed:

* (1) Determine the root sequence.
* (2) Determine the parent sequence of each sequence.
* Note that multiple sequences may have the same position within the root.
* Note that the position of a sequence within its parent is still unique.
* (3) Determine the node order based on the position of each sequence.

Solely based on a hierarchy of sequences, an algorithm can
reliably distinguish between the enter- and the exit-order:

(1, enter-order)

* subsequences have unique positions within the root
* prefix, no - the root never begins with a subsequence
* suffix, yes - the root always ends with a subsequence

(2, exit-order)

* subsequences may have the same position within the root
* prefix, yes - the root always begins with a subsequence
* suffix, no - the root never ends with a subsequence

Note that the root either has no prefix (ex-)or no suffix. Also note
that the same applies to any sequence that has more than one element.

**CONCLUSION**
A rooted ordered tree of nodes can be defined as an ordered list of nodes in
combination with a list of (offset,length) pairs which define the subsequences
with regards to the root sequence.

Note that the offset of each pair is actually not required as (N-1) subsequences
are required. That is, an ordered list of (N) nodes in combination with an
ordered list of (N-1) length values is sufficient to unambiguously define a node
tree.

<!-- ======================================================================= -->
## What if inner sequences are used instead?

```
                     inner sequences    inner sequences
node tree            enter-order        exit-order
=================    ===============    ======================

 A                   B D G E H C I F    G D E B H I F C - NS
=================    ===============    =============== - A
 B      H   C          =====     ===    =====     ===   - B, C
======     ======        =              =               - D
 D  E       I  F
===
 G
```

Assumed that the empty inner sequences of leaf nodes are omitted.

(1, enter-order)

* a sequence has no suffix, if the nodes's last child is a leaf

(2, exit-order)

* a sequence has no prefix, if the node's first child is a leaf
