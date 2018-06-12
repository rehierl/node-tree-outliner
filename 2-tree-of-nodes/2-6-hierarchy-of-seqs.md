
<!-- ======================================================================= -->
# A sequence-based perspective

```
tag soup   node tree    node sequence
========   ==========   ===============

<A>         A           [ A ]
</A>       ===
```

If a document only has a single element, then the document's node tree only
has that node as its root node. Because of that, the tree's node sequence has
the tree's root node as its only element.

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
The outer sequence of a node is unique to that node.
No other node has the exact same outer sequence.

They always differ in the defining node.

**CONCLUSION**
The inner sequence of a node is unique to that node.
No other node has the exact same inner sequence.

The reasoning is identical to the reasoning with regards to unique inner sets.
that is, because the inner sequence of a node has the exact same elements as
the inner set of that node.

Note the special case of empty inner sequences of nodes.

Note that the outer sequence of a node is identical to the inner sequence of
its parent if, and only if, the node has no siblings.

**CONCLUSION**
Each node represents its inner and its outer sequence of nodes.

One such sequence can be transformed into the other, if the defining node is
added (or removed) to (or from) the beginning of the corresponding sequence.

<!-- ======================================================================= -->
## Node trees as hierarchies of sequences

```
tag soup        node tree           outer sequences
========        ===============     =======================

<A>              A                  A B C D E F G - NS
  <B> C </B>    ===============     ============= - A 
  D              B   D   E   G        === = === = - B, D, E, G
  <E> F </E>    ===     ===             =     =   - C, F
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
tag soup           node tree             outer sequences
===============    =================     ============================

 <A>                   A                 A B D E G H C I F - NS
   <B>             =================     ================= - A
     D              B      H   C           ======= = ===== - B, H, C
     <E> G </E>    ======     ======         = ===     = = - D, E, I, F
   </B>             D  E       I  F              =         - G
   H                  ===
   <C>                 G
     I
     F
   </C>
 </A>
```

**CONCLUSION**
Each rooted ordered tree of nodes represents a hierarchy of sequences,
and each hierarchy of sequences a rooted ordered tree of nodes.

Note that these hierarchies of sequences are consistent with the definition of
subsequences of elements. That is, none of these sequences overlap: One sequence
either is embedded into another sequence, or both sequences have no nodes in
common.

Note that the sequences of sibling nodes have no nodes in common. They are said
to be independent from one another. The same applies to any two sequences that
are located within (independent) sibling trees.

**CONCLUSION**
The hierarchy of sequences of a rooted ordered tree of nodes will be
referred to as the tree's "sequence-based perspective".
