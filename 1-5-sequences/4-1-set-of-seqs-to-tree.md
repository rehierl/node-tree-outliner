
**TODO** - (open aspects)

<!-- ======================================================================= -->
# Hierarchy of sequences => Ordered tree

<!-- ======================================================================= -->
## Hierarchies as node trees

```
hierarchy of sequences           node tree
===========================  =>  ============

0 1 2 3 4 5 6 7 8 9 - A           A
=========   =====   - B,C        ============
  =   ===     ===   - D,E,F       B        C
        =     =     - G,H        =======  ===
                                  D   E    F
                                     ===  ===
                                      G    H
```

Note that the above hierarchy neither represents a hierarchy of inner (H2),
nor a hierarchy of outer (H1) sequences. That is because root sequence A has
a prefix and no suffix.

**CLARIFICATION**
A hierarchy of sequences defines the structure of a rooted (ordered) tree.

* The tree's structure has one node per set (i.e. `#H = #N`).
* The tree's structure is not defined by the elements the sequences
  contain (i.e. `(#{e | (e in s)  and (s in H)} != #N)` may be true).
* What counts is what relationship a sequence has with all the other sequences.

Note that, from a strict perspective, the resulting tree has loops because each
sequence is by definition a subsequence to itself. With that in mind, and except
for the root node, each node within the structure that such a hierarchy defines
has exactly two parent nodes: (1) the node itself, and (2) another node.
However, and even under that strict perspective, the structure minus all the
loops is that of a rooted (ordered) tree.

Note that the structure such a hierarchy defines has no cycles. In order to
have cycles, a parent sequence would also have to be a subsequence to one of
its descendant sequences. That however is not possible because (1) any ancestor
sequence always has more elements than any of its descendant sequences, and
because (2) the hierarchy is still a set of sequences (i.e. it can not contain
two identical elements/sequences).

**TODO**
Given a sequence of elements, (1) how many such hierarchies are possible and/or
(2) what is the maximum number of nodes the resulting tree can possibly have?
(hint: resource management).
