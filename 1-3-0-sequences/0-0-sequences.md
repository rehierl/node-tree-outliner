
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

Even though sequences can be created in any number of ways, the focus of this
discussion is on the traversal of document trees. To be more accurate, the
focus is on sequences whose elements are the nodes of a tree.

* `T := (N,R)` is a **directed acyclic node tree**
* `T` is not necessarily an ordered node tree
* `N` is the tree's set of nodes
* `(R subset-of N×N)` is the tree's endo-relation
* `((ni,nj) in R)` iff `(ni parent-of nj)`

During the traversal of a tree, each node will be visited no more than once,
and all nodes will be visited one after another. As soon as a node is visited,
the tree traversal can be seen to associate the next available unique ordinal
number with each node. Because of that, a strict total order `P` exists on a
tree's set of nodes `N`. Note that this order will in general be referred to
as the traversal's **node order**, **visit order**, **enter order** - i.e. a
**topological sorting**.

**TODO** - a tree's node order -vs- the traversal's node/visit order
**TODO** - the traversal's visit order -vs- the traversal's enter order
**TODO** - proof that: node order <-> visit order <-> enter order

Put differently, the traversal of a tree can be seen to add/append/associate
each node to/with a sequence of nodes `s` as soon as a node is entered. Once
the traversal of a tree has finished, such sequences will contain all the nodes
(i.e. `(E(s) == N)`) in the tree's enter order. That is, the index associated
with each node represents the ordinal number associated with that node via the
tree traversal's enter order. Note that such a node sequence will in general be
referred to as the **(node) sequence (of the tree)** - i.e. a **trace of nodes**.

In the context of this discussion, a sequence of nodes `s := [n1, n2, ..., nk]`
contains no node more than once. Because of that, the set of nodes `E(s)` is
a set of elements such that `(#E(s) == #s)`. A node sequence can therefore be
understood to define an ordered set of nodes `P, P(s) := (E(s),<)` such that
`(s[i] < s[j])` iff `(i < j)`. And because `P(s)` does not contain even one
pair of incomparable nodes, the node order defined is a strict total order.
Note that sequences of elements, for which `(#E(s) == #s)` is true, will in
general be referred to as **ordered sequences**, or as **linear sequences**.

* `s := [n1, ..., nk]` is a sequence such that `(E(s) == N)`
* `P := (E(s),<)` where `(s[i] < s[j])` iff `(i < j)`
* `P` is an ordered set of nodes in enter order
* `((ni,nj) in P)` iff `(ni entered-before nj)`
* `P` is a strict total order

<!-- ======================================================================= -->
## Sets of ordered sequences (S)

The traversal of a tree is however not limited to creating only one sequence of
nodes. That is because the very same tree traversal can be used to create a node
sequence for the whole tree and one for each (strict) subtree.

As such, the
tree traversal can be understood to add each node to one or more sequences and
therefore to create a set of sequences `S`. Note that such a set of sequences
will in general be referred to as the **set of (node) sequences (of a tree)**.

Put differently, each node within a tree can be understood to represent the
root of a tree. That is, any tree can be seen to contain `#N` subtrees, i.e.
`(#N-1)` strict subtrees and the subtree that begins in the given tree's root.
Because of that, a tree traversal can be understood to create a node sequence
for each subtree.

*  such that `(#S == #N)`

That is, each node `n` can be understood to be associated with its own
node sequence `s`. Because of that, a bijective function `(s: N -> S)` can be
defined which allows to refer to the sequence `s(n)` of node `n`. Note that any
sequence in `S` will be referred to as the **node sequence (of a node)**. Note
also that the node sequence of a tree is identical to the node sequence of its
root.

**TODO** - define "(strict) subtree"

<!-- ======================================================================= -->
## Properties of (s in S)

Obviously, the root of a tree will be entered first and will therefore always
appear as the first node in a tree's node sequence. In general, node `n` will
be the first node of sequence `s` created for the subtree that has `n` as its
root.

As before, the traversal of a tree can be seen to add each node to one or more
sequences as soon as the corresponding node is entered. That is, each node `n`
will be added to `#A(n)+1` sequences, where `A(n)` refers to the set of ancestor
nodes of `n`. Put differently, the number of sequences that contain `n` as an
element is equal to `#p(r,n)`, where `p` is the rooted path that begins in a
tree's root `r` and ends in the corresponding node `n`.

Because of that, the sequence of
a descendant is related to the sequences of its ancestors. That is, all nodes
in `s(d)` of some descendant `d` of node `n` are also nodes in `s(n)`. In short:
`(E(s(d)) strict-subset-of E(s(n)))` iff `(d descendant-of n)`. Furthermore, the
nodes are added to the sequences in the exact same enter order. That is, the
index order of `s(d)` corresponds with the index order of `s(n)`, which is why
the sequence of a descendant is a substring to the sequences of its ancestors.
In short: `(s(d) strict-substring-of s(n))`.

**TODO** - same order of sequences
**TODO** - define "suborder" - order embedding?
**TODO** - compare the node order of a subtree with the node order of a tree

<!-- ======================================================================= -->

The creation of node sequences during the traversal of a tree can be understood
to introduce a **stream-based perspective** on the node sequences of a tree.
That is because

**TODO** - expand - e.g. open/closed sequence?
