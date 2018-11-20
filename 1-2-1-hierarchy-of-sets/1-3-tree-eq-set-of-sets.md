
<!-- ======================================================================= -->
# Unordered tree <=> Hierarchy of sets

```
node tree         hierarchy of outer sets         node tree
===========  <=>  =========================  <=>  ===========

     1            |-1---------------------|            1     
===========       | |-2-| |-3-----| |-5-| |       ===========         
 2   3   5        | |---| | |-4-| | |---| |        2   3   5
    ===           |       | |---| |       |           ===
     4            |       |-------|       |            4
                  |-----------------------|
```

**CLARIFICATION**
The strict hierarchy of outer sets `H := (V,P,G)` formed from an unordered
node tree `T := (N,E)` corresponds with that tree. That is, `H` can be used
to recreate `T`.  Because of that, this correspondence will be referred to as
the **set-based correspondence** of a node tree.

(1) Each node is the only CE in its outer set.
That is, each set allows to uniquely determine which node it represents.

* `node-of(s) := ce(s)` for any `(s in P)`

(2) The relationships of each set corresponds with the relationships of its
node. That is, the hierarchy of sets accurately describes the tree's structure.

(2.1) `(ni,nj) in E => (si,sj) in G`
If node `(ni in N)` is the parent node of `nj`, then the outer set `si` of `ni`
will be the parent set of the outer set `sj` of `nj`. That is because there is
no outer set `sk` of node `nk` such that `(si parent-set-of sk)` or
`(sk parent-set-of sj)`. If such an outer set would exist, then `ni` could not
be the parent node of `nj`.

(2.2) `(ni,nj) in E <= (si,sj) in G`
That is because it can be detected that node `(ni in V)` is the node which set
`si` represents. Likewise, it can be detected that set `sj` represents node
`nj`. And because `si` is the parent set of `sj`, node `ni` can be set as the
parent node of node `nj`.

* `(ni,nj) in E <=> (si,sj) in G`

**CLARIFICATION**
For each unordered tree of nodes, only one hierarchy of sets
can be formed such that the initial node tree can be recreated.

That is because ...

* The hierarchy must have one set per node.
  (That is because the relationships of a set defines
  the relationships of the node a set represents).
* The CSS of each set must have one and only one element.
  (That is because it must be possible to uniquely determine
  the node a given set represents).
* The CE of each set must be the node a set represents.
  (That is because it must be possible to determine
  the node a given set represents).
* The set of elements V is equal the set of nodes N.
  (That is a consequence of `(#CSS == 1)` for any set).
* Sets V, P and N hold the same amount of elements.
  That is because each element in V is a CE.
* The relationships of each set must correspond
  with the relationships of the respective node.

Note that a node tree has no further information that could be added to its
hierarchy of sets. All the nodes are already part of the hierarchy and the
hierarchy already reflects all relationships the nodes have with each other.

Note that any other element added to one or more sets will break the hierarchy
and/or increase the size of the CSS of a set. Therefore, and even if the
hierarchy would still be a hierarchy after the addition, it would no longer
be possible to uniquely determine the node each set represents. That is because
the one two-element CSS would no longer allow to detect which node the parent
set of the CSS represents. From the perspective of a simple set of values, both
elements (i.e. the previous CE and the new CE) would then be equally valid.
