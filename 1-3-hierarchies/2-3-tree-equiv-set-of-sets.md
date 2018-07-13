
<!-- ======================================================================= -->
# Node tree <-> Hierarchy of sets

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
Any unordered tree of nodes represents a strict hierarchy of outer sets,
which uniquely defines the corresponding node tree.

Note that this equivalency will be referred to as
the **set-based perspective** of a tree.

**CLARIFICATION**
The strict hierarchy of outer sets `H := (V,P,G)` created from a node tree
corresponds with the initial node tree `T := (N,E)`. That is, any unordered
node tree can be recreated based on its hierarchy of sets.

(1) Each node is the only CE of its outer set.
That is, each set allows to detect which node it represents.

* `node-of(s) := ce(s)` for any `(s in P)`

(2) The relationship of each set corresponds with the relationship of its node.
That is, the hierarchy of sets accurately describes the tree's structure.

(2.1) `(ni,nj) in E => (si,sj) in G`
If node `(ni in N)` is the parent node of `nj`, then the outer set `si` of `ni`
will be the parent set of the outer set `sj` of `nj`. That is because there is
no outer set `sk` of node `nk` such that `(si parent-set-of sk)` or
`(sk parent-set-of sj)`. If such an outer set existed, then `ni` would not be
the parent node of `nj`.

(2.2) `(ni,nj) in E <= (si,sj) in G`
That is because it can be detected that node `(ni in V)` is the node which set
`si` represents. Likewise, it can be detected that set `sj` represents node `nj`.
And because `si` is the parent set of `sj`, node `ni` can be set as the parent
node of node `nj`.

* `(ni,nj) in E <=> (si,sj) in G`

**CLARIFICATION**
For each unordered tree of nodes, only one hierarchy of sets
can be created such that the initial node tree can be recreated.

That is because ...

* The hierarchy must have one set per node.
* The CSS of each set must have one element only.
* The CE of each set must be the node a set represents.
* The set of elements V will therefore be the set of nodes N.
* And because each element in V is a CE,
  sets V, P and N will hold the same amount of elements.
* Finally, the relationship of each set must correspond
  with the relationship of each node.

Note that a node tree holds in general no further information that could be
added to the hierarchy of sets. The nodes are all part of the hierarchy and
the hierarchy reflects all the dependencies the nodes have with each other.
That is, any additional information that could be added to the hierarchy
would have to originate from outside of the node tree.

Note that any other element added to one or more sets will break the hierarchy
and/or increase the size of the CSS of a set. Therefore, and even if the
hierarchy would still be a hierarchy after the addition, it would no longer be
possible to determine the node each set represents. That is because the one
two-element CSS would then no longer allow to detect which node the parent set
of the CSS represents. From the perspective of a simple set of values, both
elements would be equally valid.
