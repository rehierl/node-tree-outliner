
**TODO** - (open aspects)

<!-- ======================================================================= -->
# Equivalency between trees and hierarchies of sets

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
For each unordered tree of nodes, only one hierarchy of sets
can be created that allows to recreate the initial node tree.

That is, because ...

1) The hierarchy must have one set per node.
2) The CSS of each set must have one element only.
3) The CSS of each set must hold the node the set represents.
4) Each node in the initial tree has one parent only.
5) The set of each node must be connected with the appropriate parent set.

Note that any other element added to one or more sets will break the hierarchy
and/or change the CSS of one set. Therefore, and even if the hierarchy would
still be a hierarchy after the addition, it would no longer be possible to
determine the node each set represents. That is, because the one two-element
CSS does not allow to determine whether the node or the new element it contains
is the node the corresponding set represents.

**CLARIFICATION**
Any unordered tree of nodes represents a strict hierarchy of outer sets,
which uniquely defines the corresponding node tree.

Note that this equivalency will be referred to as
the **set-based perspective** of a tree.

<!-- ======================================================================= -->
## TODO

verify that a hierarchy of sets corresponds with a node tree -

**TODO** -
show that the tree created from a tree's hierarchy -
is identical/equivalent to the initial tree -
(n1,n2) in E => (s1,s2) in G -
generalize uniqueness -
must poof: (rel-of-set == rel-of-node) -

**TODO** -
most likely the only such set-of-sets possible -
can that be proven? -
