
<!-- ======================================================================= -->
# A sequence-based perspective

```
tag soup   node tree    node sequence
========   ==========   ===============

<A>         A           [ A ]
</A>       ===
```

If a document only has a single element, then the document's node tree only has
that node as its root node. Because of that, the tree's node sequence has the
tree's root node as its only element.

```
tag soup   node tree    node sequence
========   ==========   ===============

<A>         A           [ A, B ]
  B        ===
</A>        B 
```

Element A will be entered before B is entered. With regards to the tree's node
sequence, B is subsequent to A.

```
tag soup   node tree    node sequence
========   ==========   ===============

<A>         A           [ A, B, D ]
  B        ======
  D         B  D
</A> 
```

The next sibling of a node is subsequent to that node.

```
tag soup        node tree    node sequence
========        ==========   ===============

<A>              A           [ A, B, C, D ]
  <B> C </B>    ======
  D              B  D
</A>            ===
                 C
```

B is entered before C, and C before D. C therefore appears in between B and D.

<!-- ======================================================================= -->
## The root's inner/outer sequence of nodes

```
tag soup        node tree           node sequences of A
========        ===============     =======================

<A>              A                  [ A, B, C, D, E, F, G ] - NS
  <B> C </B>    ===============      =====================  - S1
  D              B   D   E   G          ==================  - S2
  <E> F </E>    ===     ===
  G              C       F
</A>
```

Each rooted ordered tree of nodes has exactly one most significant node, its
root node (A).

* A root node can be understood to represent two sequences of nodes.
* The root's outer sequence (S1) is the root's complete node sequence.
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

Each node within a tree is understood to represent the root of a subtree. And,
because of that, any node can be understood to represent two sequences of nodes:
(S1) the node sequence that begins with the given node, and
(S2) the concatenation of the node sequences of its child nodes
(concatenated in the order of its child nodes).

* No outer sequence of a node is ever empty.
* An outer sequence always has at least one node (i.e. its defining root node).
* An inner sequence is empty if, and only if, its defining node is a leaf node.
* An empty tree has no node and consequently no outer and no inner sequence.

The relationship between a node's inner and outer sequences:

* The inner sequence of a node is a suffix of the node's outer sequence.
* S1 is the parent (i.e. an ancestor) sequence of S2.
* S2 is the only child (i.e. a descendant) sequence of S1.
* There is no other distinct sequence in between S1 and S2.

**CONCLUSION**
Each node represents its inner and its outer sequence of nodes.

One such sequence can be transformed into the other, if the defining node is
added (or removed) to (or from) the beginning of the corresponding sequence.

**CONCLUSION**
Each node represents and contains all of its descendants.

<!-- ======================================================================= -->
## Node trees as hierarchies of sequences

```
tag soup        node tree           (inner) node sequences
========        ===============     =======================

<A>              A                  [ A, B, C, D, E, F, G ] - NS
  <B> C </B>    ===============         ==================  - A 
  D              B   D   E   G             ===      ===     - B, E
  <E> F </E>    ===     ===
  G              C       F
</A>
```

The hierarchy of all inner node sequences is:

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
  to the inner sequence of the child's parent.
* Both sequences of a given node are subsequences
  to any of the sequences of the node's ancestors.
* Each node within the two sequences of a node is also
  an element within any of the sequences of the node's ancestors.
* No such sequence contains a node that an ancestor sequences does not contain.

The above statements should be fairly obvious because
any descendant of a node is also a descendant of the node's ancestors
and as such also an element of an ancestor's sequence.

* The node sequences (inner and outer) of all of a node's descendants all
  are subsequences to that node's node sequences.
* The outer sequence of a child is identical to the inner sequence of its
  parent if, and only if, the parent has no other child.

Note the special case of empty inner sequences of nodes. Also note that a node
tree has unique empty inner sequences for each of its leaf nodes. These empty
sequences can be identified via their defining leaf node.

<!-- ======================================================================= -->
## Equivalency between trees and hierarchies of sequences

```
A node tree                                A hierarchy of sequences
====================================       ============================

 <A>                   A                   A B D E G H C I F - NS
   <B>             =================         =============== - A
     D              B      H   C               =====     === - B, C
     <E> G </E>    ======     ======               =         - E
   </B>             D  E       I  F        
   H                  ===                  
   <C>                 G                   
     I                                     
     F                                     
   </C>                                    
 </A>
```

**CONCLUSION**
Each rooted ordered tree of nodes represents a hierarchy of sequences,
and each hierarchy of sequences a rooted ordered node tree.

Note that these hierarchies of sequences are consistent with the definition of
subsequences of elements. That is, none of these sequences overlap: One sequence
either is embedded into another sequences, or both sequences share no nodes.

Note that the sequences of sibling nodes have no nodes in common. They are said
to be independent from one another. The same applies to any two sequences that
are located within (independent) sibling trees.

**CONCLUSION**
A tree's hierarchy of sequences of a rooted ordered tree of nodes will be
referred to as the tree's "sequence-based perspective".
