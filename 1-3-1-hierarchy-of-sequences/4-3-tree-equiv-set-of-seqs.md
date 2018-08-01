
**TODO** - (open aspects)

<!-- ======================================================================= -->
# Ordered tree <=> Hierarchy of sequences

**CLARIFICATION**
Each rooted ordered tree of nodes represents a hierarchy of sequences,
and each hierarchy of sequences represents a rooted ordered tree of nodes.

**CLARIFICATION**
The hierarchy of sequences of a rooted ordered tree of nodes will be
referred to as the tree's "sequence-based perspective".

<!-- ======================================================================= -->
## Equivalency between trees and hierarchies of sequences

```
outer sequences                   node tree
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
