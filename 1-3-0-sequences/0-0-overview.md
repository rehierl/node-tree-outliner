
<!-- ======================================================================= -->
# Overview

The following content needs to be understood
to lay out the general context of this chapter.

<!-- ======================================================================= -->
## Ordered sequences (s)

Even though sequences can be created in any number of different ways, the
focus of this discussion is on the traversal of document trees. To be more
accurate, the focus is on sequences whose elements are the nodes of a tree.

* `T := (N,R)` is a **directed acyclic tree of nodes**
* `T` is commonly, but not necessarily an ordered tree
* `N` is the tree's set of nodes
* `(R subset-of N×N)` is the tree's endo-relation
* `sem(R)` := `((ni,nj) in R)` iff `(ni parent-of nj)`

During the traversal of a tree, each node will be visited no more than once,
and all nodes will be visited one after another. As soon as a node is visited,
the tree traversal can be understood to associate the next available ordinal
number with each node. Because of that, a strict total order `P` exists on a
tree's set of nodes `N`.

Note that this order will in general be referred to as the traversal's **node
order**, **visit order**, **enter order** - i.e. a **topological sorting**.

Put differently, the traversal of a tree can be seen to add/append/associate
each node to/with a sequence of nodes `s` as soon as a node is entered. Once
the traversal of a tree has finished, such sequences will contain all the nodes
(i.e. `(E(s) == N)`) in the traversal's enter order. That is, the index of a
node in `s` represents the ordinal number the traversal associates with a node.

Note that such a node sequence will in general be referred to as the **(node)
sequence (of a tree)** - i.e. a **trace of nodes**.

* `(s, seq: T -> N*)` is a function such that
* `s(t)` returns the node sequence of tree `t`
* `s = s(t) = [n1, n2, ..., nk]` where `(s[i] in N)` for all `(i in [1,k])`

In the context of this discussion, a sequence of nodes `s` contains no node
more than once. Because of that, the node sequence of a tree is a sequence
such that `(#s == #E(s))`. A node sequence can therefore be understood to
define an order relation `P, P(s) := (E(s),<)` on the set of nodes such that
`(s[i] < s[j])` iff `(i < j)`. And because `P` does not contain even one pair
of incomparable nodes, the node defined is a strict total order.

Note that a sequence of elements, for which `(#s == #E(s))` is true, will in
general be referred to as an **ordered sequence**, or as a **linear sequence**.

* `s = [n1, ..., nk]` is an ordered sequence of nodes
* `(#s == #E(s))` and `(E(s) == N)` are both true
* `P := (E(s),<)` where `(s[i] < s[j])` iff `(i < j)`
* `P` is the ordered set of nodes in enter order
* `sem(P)` := `((ni,nj) in P)` iff `(ni entered-before nj)`
* `P` is a strict total order

<!-- ======================================================================= -->
## Set of ordered sequences (S)

The traversal of a tree is however not limited to creating only one sequence.
That is because a tree traversal can be used to create a sequence for the whole
tree and one for each (strict) subtree. Consequently, a tree traversal can be
understood to add each node to one or more sequences and therefore to create a
set of sequences `S`.

Note that such a set of sequences will in general be referred to as the **set
of (node) sequences (of a tree)**.

Put differently, each node within a tree can be understood to represent the
root of a subtree for which a node sequence will be created. Because of that,
each tree can be seen to represent `#N` distinct subtrees: `(#N-1)` strict
subtrees and the subtree that begins in the tree's root.

Note that the subtree of a node, which has the given node as its root, will
in general be referred to as the **(sub)tree of a node**. In addition to that,
the sequence created for the subtree, which corresponds with a node, will in
general be referred to as the **node sequence of a node**. The node sequence
of a tree is therefore identical to the node sequence of its root. Furthermore,
the root of a subtree will in general be referred to as the **defining node**
of a subtree/sequence.

* `(t, tree: N -> T)` is a function such that
* `tree(n)` returns the subtree that has `n` as its root
* i.e. `t(n)` returns the subtree's endo-relation

Likewise, ...

* `(r, root: T -> N)` is inverse to `tree()`
* `root(t)` returns the root node `r` of the given tree `t`
* i.e. `(tree(root(t)) == t)` and `(root(tree(r)) == r)` are both true

Furthermore, a tree's root will be entered first during the traversal of a
tree. Because of that, the root of any tree will always be the first node in
the sequence of a tree. In general, node `n` will be the first node of sequence
`s` created for `tree(n)`.

*  `(s[1] == n) <-> (s == seq(tree(n)))`

Consequently, no node sequence created for another subtree will begin with the
exact same node. The sequence created for the subtree of a node will therefore
be unique and distinct from the sequences of any other subtree. The set of
sequences `S` of a tree will therefore hold one sequence per node. That is,
each node `n` can be understood to be associated with its own sequence `s`.

* `(#S == #N)`
* `(s, seq: N -> S) := seq(tree(n))` is a function such that
* `s(n)` returns the node sequence `s` of node `n`

<!-- ======================================================================= -->
## Example sets of sequences

In general, and as soon as some node `n` is entered, the traversal of a tree
can be understood to create the node's sequence `s(n)` and to add it to the
set of sequences `S`. Furthermore, and because node `n` was entered, the tree
traversal initializes `s(n)` by adding `n` to `s(n)` as the first node of
that sequence (i.e. `(s[1] == n)`).

```
node tree T   set of sequences S
===========   ==================
 n1 -> n2     s(n1) := [n1, n2]
              s(n2) := [n2]
```

* (A1) Node `n1` is entered first, which is why
  `s(n1)` needs to be created and initialized.
* (A2) Node `n2` is entered next, which is why
  `s(n2)` needs to be created and initialized.
* (A3) Node `n1` was not yet exited, which is why
  `n2` also needs to be added to `s(n1)`.
* (A4) The next step is to exit `n2`, which is why
  no more nodes will be added to `s(n2)`.
* (A5) The final step is to exit `n1`, which is why
  no more nodes will be added to `s(n1)`.

```
node tree T   set of sequences S
===========   ==================
 n1 -|-> n2   s(n1) := [n1, n2, n3]
     |-> n3   s(n2) := [n2]
              s(n3) := [n3]
```

* (B0) Due to structural similarities, this fragment
  can be understood to begin just after step (A3).
* (B1) The next step is to exit `n2`, which is why
  no more nodes will be added to `s(n2)`.
* (B2) Node `n3` is entered next, which is why
  `s(n3)` needs to be created and initialized.
* (B3) Node `n1` was not yet exited, which is why
  `n3` also needs to be added to `s(n1)`.
* (B4) The next step is to exit `n3`, which is why
  no more nodes will be added to `s(n3)`.
* (B5) The final step is to exit `n1`, which is why
  no more nodes will be added to `s(n1)`.

Based on these examples, the following observations can be made:

* Due to `(s(n)[1] == n)`, no `(s in S)` is ever empty.
* Any `(s in S)` is an infix to the root's node sequence.
* The sequence of a descendant will always be a
  strict infix to the sequences of its ancestors.
* The sequence of a descendant will never be a
  prefix to the sequences of its ancestors.
* The sequence of a descendant may be, but does not have to be
  a strict suffix to one or more sequences of its ancestors
  - e.g. `(s(n3) strict-suffix-to s(n1))`.
* `S` may contain sequences that are disjoint
  - e.g. `(s(n2) disjoint-to s(n3))`.
* If two distinct sequences have one or more nodes in common,
  then one sequence is a strict subsequence of the other.
* Each node will be added to `#A(n)+1` sequences, where
  `A(n)` is the set of ancestors of the corresponding node.

<!-- ======================================================================= -->
## A stream-based perspective

As can also be seen from the above examples, nodes are added to a sequence as
soon as the defining node was entered. In addition to that, the traversal will
continue to add nodes to a sequence until the defining node was exited.

In the context of a tree traversal, any sequence can therefore be understood to
have states associated with it: (1) A sequence is **undefined** for as long as
its defining node has not been entered. (2) A sequence counts as being **open**
for as long as the traversal of a tree is still visiting the descendants of the
corresponding defining node. (3) And finally, a sequence is **closed** as soon
as the defining node of a sequence was exited.

Note that this state-based perspective on sequences will in general be referred
to as the **stream-based perspective**. That is, the above node sequences can,
similar to binary streams, be understood to represent streams of nodes.

In addition to that, and once a defining node is entered, all the nodes of the
corresponding subtree are added to a sequence. That is, this perspective has no
paused and no continued states. Because of that, the all sequences can be seen
to be **consecutive** with regards to the tree traversal's node order.

<!-- ======================================================================= -->
## An interval-based perspective

Due to all sequences in `S` being consecutive with regards to the traversal's
enter order, and because of that order being total, any non-empty subsequence
has a first and a last node. As such, any sequence has a least (first) and a
greatest (last) element.

Put differently, any sequence in `S` can be understood to contain all the nodes
in between its first and last node. That is, all the nodes of a sequence can be
inferred from a sequence's first and last node.

Consequently, all sequences in `S` can be expressed as intervals with regards
to a given tree traversal.

<!-- ======================================================================= -->
## Related ordered sequences

As before the traversal of a tree can be understood to add each node to one or
more sequences. Because of that, the sequence of a descendant always has one
or more nodes in common with the sequences of its ancestors. That is, the node
sequences of descendant nodes are related to the sequences of their ancestors.
Consequently, the relationship of a node with all the other nodes in a tree is
mapped onto the sequences in `S`.

Furthermore, and because any sequence is an infix to the root's node sequence,
all sequences correspond with the tree traversal's enter order. That is, all
sequences represent sub-orders to the traversal's enter order.

This chapter will therefore focus on introducing those definitions that allow
to describe the relationship an ordered sequence in `S` has with all the other
sequences in `S`.
