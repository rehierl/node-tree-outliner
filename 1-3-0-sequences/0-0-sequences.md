
<!-- ======================================================================= -->
# Sequences

* see "mathematics" for the core concept of sequences
* see "formal languages" for string-related aspects
* see "topology" for "every sequence is a net"

<!-- ======================================================================= -->
## Which term is appropriate?

* term "sequence" will be used in the course of this discussion
* in the course of this discussion, an "ordered sequence of nodes"

tuples

* `t := [1, 'a'] := (1,a)`
* an ordered list of "anything"
* in general of finite length

sequences

* `s := [1, 2, ...] := (1,2, ...)`
* an enumerated collection of "anything" of any length
* in general a rule exists such that subsequent elements
  in a sequence can be calculated from presequent ones
* e.g. `an := a(n-2) + a(n-1)` (Fibonacci)

strings

* `s := "abac..." := ['a', 'b', 'a', 'c', ...]`
* traditionally a sequence of characters
* elements are selected from an alphabet
* in computing generalized into a sequence of binary data
* depending on the context, a mutable/immutable sequence

vectors

* `v := [1.0, 2.0, 3.0] := < 1, 2, 3 >`
* in general an element of the real coordinate space (R^n)

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
more than once. Because of that, the set of nodes `E(s)` is a set of elements
such that `(#E(s) == #s)`. A node sequence can therefore be understood to
define an order relation `P, P(s) := (E(s),<)` on the set of nodes such that
`(s[i] < s[j])` iff `(i < j)`. And because `P` does not contain even one pair
of incomparable nodes, the node order defined by such a sequence is a strict
total order.

Note that a sequence of elements, for which `(#E(s) == #s)` is true, will in
general be referred to as an **ordered sequence**, or as a **linear sequence**.

* `s = [n1, ..., nk]` is a sequence of nodes
* `(E(s) == N)` and `(#s == #N)` are both true
* `P := (E(s),<)` where `(s[i] < s[j])` iff `(i < j)`
* `P` is an ordered set of nodes in enter order
* `sem(P)` := `((ni,nj) in P)` iff `(ni entered-before nj)`
* `P` is a strict total order

<!-- ======================================================================= -->
## Set of ordered sequences (S)

The traversal of a tree is however not limited to creating only one sequence.
That is because a tree traversal can be used to create a sequence for the whole
tree and one for each (strict) subtree. Because of that, a tree traversal can
be understood to add each node to one or more sequences and therefore to create
a set of sequences `S`.

Note that such a set of sequences will in general be referred to as the **set
of (node) sequences (of a tree)**.

Put differently, each node within a tree can be understood to represent the
root of a subtree for which a node sequence will be created. Because of that,
each tree can be seen to represent `#N` distinct subtrees: `(#N-1)` strict
subtrees and the subtree that begins in the tree's root.

Note that the subtree of a node, which has the given node as its root, will
in general be referred to as the **(sub)tree of a node**. In addition to that,
the sequence created for the subtree, which corresponds with a node, will in
general be referred to as the **node sequence of a node**. Note also that the
node sequence of a tree is identical to the node sequence of its root.

* `(t, tree: N -> T)` is a function such that
* `tree(n)` returns the (sub)tree that has `n` as its root
* i.e. `t(n)` returns the subtree's endo-relation

Likewise, ...

* `(r, root: T -> N)` is inverse to `tree()`
* `root(t)` returns the root node `r` of the given tree `t`
* i.e. `(tree(root(t)) == t)` and `(root(tree(r)) == r)` are both true

Furthermore, a tree's root will be entered first during the traversal of a
tree. Because of that, the root of any subtree will always be the first node
in the node sequence of a subtree. In general, node `n` will be the first
node of sequence `s` created for `tree(n)`.

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

```
node tree T   set of sequences S
===========   ==================
 n1 -> n2     s(n1) := [n1, n2]
              s(n2) := [n2]
```

* (A1) As soon as the traversal enters the root `n1`, it can be understood
  to create the node sequence `s(n1)` and to add `n1` to that sequence as
  its very first node.
* (A2) After that, the traversal will enter the root's first and only child
  `n2` and will treat that node as the root of a subtree. That is, the
  traversal will create and initialize the node sequence `s(n2)`. However,
  and because the tree traversal has not yet exited `n1`, `n2` must also
  be added to `s(n1)`.
* (A3) Obviously, the next step is to exit `n2`,
  which is why no more nodes will be added to `s(n2)`.
* (A4) Likewise, the next step is to exit `n1`,
  which is why no more nodes will be added to `s(n1)`.

```
node tree T   set of sequences S
===========   ==================
 n1 -|-> n2   s(n1) := [n1, n2, n3]
     |-> n3   s(n2) := [n2]
              s(n3) := [n3]
```

* (B0) Due to the structural similarities, this fragment can be understood
  to begin just after having executed steps A1 through A3. That is, `n3`
  is about to be entered.
* (B1) Entering `n3` is obviously exactly the same as entering any other
  root node. That is, `s(n3)` will be created and initialized with `n3`.
  However, and because the tree traversal has not yet exited, `n1`, `n3`
  must also be added to `s(n1)`.
* (B2) Similar to (A3), the next step is to exit `n3`,
  which is why no more nodes will be added to `s(n3)`.
* (B3) Finally, the last step is to exit `n1`,
  which is why no more nodes will be added to `s(n1)`.

As can be easily seen from these examples, ...

* Any sequence in `S` is an infix to the root's node sequence.
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

Any sequence can therefore be understood to have states associated with it:
(1) A sequence is **undefined** for as long as its defining node has not been
entered. (2) A sequence is **open** for as long as the traversal of a tree
is still visiting the nodes of the corresponding subtree. (3) And finally, a
sequence is **closed** as soon as the defining node of a sequence was exited.

Note that this state-based perspective on the node sequence of a tree will in
general be referred to as the **stream-based perspective**. That is, the above
node sequences can, similar to binary streams, be understood to represent
streams of nodes.

In addition to that, and once a defining node is entered, all the nodes of the
corresponding subtree are added to a sequence. That is, this perspective has
no paused and no continued states. Because of that, the above sequences can be
understood to be **consecutive** or **contiguous** with regards to the tree
traversal's node order.

Note that the sequence of a descendant would otherwise not be infixes to the
the sequences of its ancestors.

<!-- ======================================================================= -->
## Related ordered sequences

As before the traversal of a tree can be understood to add each node to one or
more sequences. Because of that, the sequence of a descendant always has one or
more nodes in common with the sequences of its ancestors. That is, the sequences
of descendant nodes are related to the sequences of their ancestors.

Furthermore, and because any sequence is an infix to the root's node sequence,
all sequences correspond with the tree traversal's enter order. That is, all
sequences represent sub-orders to the traversal's enter order.

The remainder of this chapter will therefore focus on a detailed introduction
of definitions that allow to describe the relationships the ordered sequences
of a tree have with each other.
