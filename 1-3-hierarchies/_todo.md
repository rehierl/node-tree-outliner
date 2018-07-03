
<!-- ======================================================================= -->
# TODOs

* strict hierarchy => (#V == #P)?
* are length values similar to rank values?

element-of vs. subsequence-of

* `s = [1, [2, 3], 4]`, `t = [2, 3]`
* `t` is an element of `s = [1, t, 4]`
* that is, an element in `s` has `t` as its value
* `s = [1, 2, 3, 4]`, `t = [2, 3]`
* `t` is an infix/subsequence of `s`

<!-- ======================================================================= -->

**CLARIFICATION**
The following expressions are always true:

* `(#H1 = #N)`, `(#H2 <= #N)`, `(#H0 <= #N*2)`
* `(#H2* < #N)`, `(#H0* < #N*2)`

Note that ...

* H1 always holds one set per node.
* H2 will only hold one set per node, if the tree has a single leaf.
* H2 will hold less than `#N` sets, if the tree has more than two leafs.
* H2* always holds less than `#N` sets.
* H0 will only hold two sets per node, if the tree has a single node.
* H0 will hold less sets than twice the number of nodes (i.e. `#N*2`),
  if the tree is linear (i.e. a single rooted path of nodes).
* H0 will hold less than `#N*2` sets, if the tree has more than one leaf.
* H0* always holds less than `#N*2` sets.
* Note that a node's inner set is identical to the outer set of its only child.
* Note that no set of elements/sets can contain an element/set more than once.

<!-- ======================================================================= -->
## Relationship between the elements in V and P

(warning - not sure, if the following is error-free
or even if it covers all possible cases)

Note that this section is with regards to the requirements
which a given set of sets P thrusts upon the set of elements V.

```
|-A-------|   |-B-----------|   |-C---------------------|
| 1 |-A-| |   | |-A-| |-B-| |   | |-A-| |-B-----------| |
|   | 2 | |   | | 1 | | 2 | |   | | 1 | | |-C-| |-D-| | |
|   |---| |   | |---| |---| |   | |---| | | 2 | | 3 | | |
|---------|   |-------------|   |       | |---| |---| | |
                                |       |-------------| |
                                |-----------------------|
```

(if each set is only allowed to hold a single element)

A hierarchy is minimal, if none of the elements in V can be removed without
changing the structure of the hierarchy and/or without violating any of the
hierarchy's requirements (e.g. no empty set, one root set).

(1) V must have one (unique) element per leaf set `l in L`

* `L := { l | (l in P) and (l is a leaf set) }`
* because H is not allowed to contain empty sets
* each leaf set `l` must have a unique element in V
* because it would otherwise not be possible
  to distinguish the leaf sets from one another
* `(#L <= #V)` must be true

(2) V must have one (unique?) element per parent `p in P1`

* `P1 := { p | (p in P) and (p is a parent) and (p has one child only) }`
* because it would otherwise not be possible to distinguish
  such a parent `p` from parent `q in P1` if `(p != q)`
* `(#L + #P1 <= #V)` must be true

<!-- ======================================================================= -->
## In search for equivalency

```
          \  Hx  |   |   |   |   |
construct  \     | 1 | 2 | 2*| 0 | 0*
-----------------|---|---|---|---|---
simple hierarchy | + | - | - | - | + 
-----------------|---|---|---|---|---
strict hierarchy |   | - | - | - |   
```

Even though the consistent setup H0 satisfies req-1, it does not satisfy req-2.
H0 does therefore not allow to reliably recreate the tree. And, because of that,
a hierarchy that could satisfy all the above requirements can only be a strict
subset of H0.

```
node tree                H2 - set of inner sets
===================  =>  ================================

 0                        0
===================      |-A----------------------------|
 1      2                |   1       2                  |
=====  ============      |  |-B---| |-C---------------| |
 ...    3      4         |  | ... | |  3       4      | |
       =====  =====      |  |-----| | |-D---| |-E---| | |
        ...    ...       |          | | ... | | ... | | |
                         |          | |-----| |-----| | |
                         |          |-----------------| |
                         |------------------------------|
```

H2 is not a hierarchy because this set of sets contains the empty set. As
such, H2 is not even a strict setup. In addition to that, H2 and H2* are
not guaranteed

Even though each non-empty inner set has a characteristic subset of child nodes
(e.g. `{3,4}`), it is not possible to reliably determine the parent node of
those child nodes.

The only statement that can be made, solely based on a hierarchy
of inner sets, is that the defining node of an inner set is an element of the
subset of child nodes of the inner set's parent set (e.g. `{1,2}`). Other than
that, it is not possible to identify the corresponding node among the child
nodes of a parent set (i.e. either `1` or `2`). Further information would be
required in order to reliably make that determination. Consequently, req-3
can not be satisfied.

Note that an unordered tree has no node order. Because of that, it can not be
assumed that the inner set's node can be determined by any order. In addition
to that, it can not be assumed that the data which represents a node (e.g. an
ID value) has any kind of relationship with regards to the data that represents
the node's child nodes (e.g. the lowest value amongst those values). That is,
any such data must be considered unique to a node, but random with regards to
all the other nodes.

Note that the hierarchy of inner sets does not contain the root node as an
element of any of its sets. From a strict perspective, it is therefore not
possible to determine which node the root set represents because the hierarchy
does not contain the root as an element. Consequently, it would be necessary to
add the root node to its inner set, which essentially replaces the root's inner
set with its outer set. Even though the hierarchy would then contain all the
nodes, req-3 could still not be satisfied. That is because, as before, it would
not be possible to reliably distinguish the root node from its child nodes.

```
node tree                H1 - hierarchy of outer sets
===================  =>  ================================

 0                         
===================      |-A----------------------------|
 1      2                | 0                            |
=====  ============      |  |-B---| |-C---------------| |
 ...    3      4         |  | 1.. | | 2               | |
       =====  =====      |  |-----| | |-D---| |-E---| | |
        ...    ...       |          | | 3.. | | 4.. | | |
                         |          | |-----| |-----| | |
                         |          |-----------------| |
                         |------------------------------|
```

Note that, even from a strict perspective, the hierarchy of outer sets (H1)
has one set per node. That is, req-0, req-1 and req-2 are (strictly) satisfied.

The outer set of a node contains by definition its defining node. In contrary
to inner sets, the defining node is the only node an outer set has that is not
also an element of any of the outer set's descendant sets. Consequently, the
hierarchy of outer sets also satisfies req-3.

**CLARIFICATION**
From a strict perspective, an unordered node tree can be recreated,
if the tree's hierarchy of outer sets (H1) is available.

<!-- ======================================================================= -->

Obviously, these requirements already lay out the main properties of such a
hierarchy. However, the question of how to determine the node a set represents
is still unanswered. So far, the only aspect that is clear about it is this:
Each set must contain the node it represents as one of its elements.

But, other than that, how does one identify that particular node within the
corresponding set of nodes? After all, the root set will hold all the nodes
because each other set will be a strict subset of it (i.e. `(r == V)` for
root set `(r in P)`). So which node within the root set is the root node?

<!-- ======================================================================= -->
## Identifying subsets of nodes

* `(#ISS = 1)`, if N is an outer set.
* `(#ISS >= 1)`, if N is the inner set of a parent.
* `(#ISS = 0)`, if N is the empty inner set of a leaf.

Note that the tree's structure can be reconstructed even though the identifying
subsets of all parent sets in the previous example are empty. Leaf sets and
their identifying subsets must not be empty, as those leaf sets would otherwise
count as subsets to any other set.

Note that the outer set of a node is the set of nodes of the subtree that has
the node as its root (hint: a rooted tree of nodes). In contrary to that, the
inner set of a node is the union of the outer sets of those subtrees that have
the node's child nodes as their root (hint: a forest).

**CLARIFICATION**
Each inner/outer set of nodes contains a non-empty subset of nodes which none
of its descendant inner/outer sets have. In addition to that, the corresponding
inner/outer set is the least significant inner/outer set that still contains
this non-empty subset.

With regards to H1:

* The outer set of a descendant
  is embedded into the outer set of an ancestor.
* The outer set of a node is the least significant set that
  still contains the outer set's defining node.
* None of the descendant outer sets has this node as an element.

With regards to H2:

* The inner set of a descendant
  is embedded into the inner set of an ancestor.
* The inner set of a node is the least significant set that
  still contains all of the defining node's child nodes.
* None of the descendant inner sets have even one of these
  child nodes as an element.

**CLARIFICATION**
Both characteristics combined allow to use such a non-empty subset in order
to identify a non-empty inner/outer set within the corresponding hierarchy
(H1 or H2).

<!-- ======================================================================= -->
## Equivalency between trees and hierarchies of sets

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
Each rooted (unordered) node tree defines a strict hierarchy (H1),
which uniquely describes the rooted (unordered) node tree.

Note that this equivalency will be referred to as
the **set-based perspective** of a tree.

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
