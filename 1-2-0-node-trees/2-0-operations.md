
<!-- ======================================================================= -->
# Operations on trees

Recall that the overall focus is on the subtrees of a document tree. In
addition to that, each subtree is assumed to be induced by its root node
(i.e. `S := T[r]`, i.e. `S := T[OS(r)]`).

<!-- ======================================================================= -->
## general remarks

Any operation on a tree is by definition also an operation on the tree's graph.
Because of that, and unless stated otherwise, any operation defined to operate
on a graph can in general be used with trees.

Recall that, if two graphs have an edge in common, then both graphs also
have both of the endpoints of such an edge in common. In contrary to that,
two graphs may have one or more vertices, but no edge in common.

The execution of binary operations on graphs must also take the semantics of
both graphs into account. That is, the semantics of two input graphs, for which
such an operation has to be executed, are by default expected to be similar,
if not identical.

Because issues arise, if arbitrary trees are processed (i.e. arbitrary sets of
nodes and arbitrary connections between the nodes), the following conditions
are considered requirements of the operations mentioned below:

(1) The nodes in trees `S` and `T` must be connected in a similar fashion.
That is, if trees `S` and `T` have nodes `a` and `b` in common, and if `S` has
a path `p := aPb`, then that path `p` must also exist in `T`. The main focus is
that `a` can not be an ancestor of `b` in `S` and a descendant of `b` in `T`.

(2) In general, a common node must be a descendant of common ancestors. That
is, if trees `S` and `T` have node `n` in common, and if `n` has node `a` as
an ancestor in `S`, then `a` must also be an ancestor of `n` in `T`. The main
focus is that both trees in general need to have all of the ancestors of a
common node in common.

(3) Node trees `S` and `T` must have the same child order. That is, if trees
`S` and `T` have nodes `a` and `b` in common, and if `b` is the next sibling
of `a` in `S`, then `b` must also be the next sibling of `a` in `T`. The main
focus is that `a` can not be presequent to `b` in `S` and subsequent to `b`
in `T`.

(4) The non-empty intersection between two trees `S` and `T` must be a single
tree. The main focus is that the non-empty intersection between both trees is
a subtree to both.

(5) If the result of a binary operation on two trees `S` and `T` is a graph,
then the resulting graph `R` must be a tree.

In general: Two input trees are expected to be of similar kind and content.
That is, the semantics of the contents in both trees are expected to not be
in conflict with each other.

<!-- ======================================================================= -->
## unary operations

Any tree can be transposed. However, the resulting converse graph `T°` is not
a tree. The converse graph of a tree has the "child-of" semantics, which is
because a child becomes the parent of its former parent.

Similar to that, the complement graph `T*` of a tree is not tree. That is
because the nodes in such a complement graph have in general "more than one
parent" node.

<!-- ======================================================================= -->
## binary operations

The following binary, graph-based operations may be used without limitation:

* equal, unequal, distinct
* disjoint, coupled, overlap
* subgraph/subtree

Two trees `S` and `T` are said to be **related** with each other,
if one is a subtree of the other:

* `(S related-to T)`, if `(S subtree-of T)` or `(T subtree-of S)`
* `(S related-to T) <-> (T related-to S)`

<!-- ======================================================================= -->
## intersection (&, and, isect)

* `(and: (Tree,Tree) -> {Ø,Tree})` or `R := (S & T)`

Two distinct subtrees `S` and `T` of a common super-tree `U` (i.e. `S := U[s]`,
`T := U[t]` and `(s != t)`) can not overlap each other.

To proof that, the following cases need to be distinguished: (Case-1) `s` is an
ancestor of `t`, (Case-2) `t` is an ancestor of `s`, or (Case-3) `s` is not an
ancestor of `t`, and `t` not an ancestor of `s`.

Case-1/2: Subtree `S` is induced by the outer set of node `s` and therefore
includes all the nodes in the outer set of `t`. Because of that, `T` is a
proper induced subtree of `S`. Hence, the intersection between `S` and `T`
is equal to `T`.

* `((S & T) == T)` if `(s ancestor-of t)`
* `((S & T) == S)` if `(t ancestor-of s)`
* note - `(S & T)` is in both cases a subtree of `S` and `T`

Case-3: Subtree `S` is induced by the outer set of node `s` and can therefore
not include any node in the outer set of `t`. Because of that, subtrees `S`
and `T` are disjoint. That is, the intersection between `S` and `T` is empty.

* `((S & T) == Ø)`, if `(s !ancestor-of t)` and `(t !ancestor-of s)`

Consequently, two such subtrees are either disjoint ex-or one is a proper
induced subtree of the other. That is, the requirements (i.e. a non-empty
intersection and unrelated) can not be met. Because of that, no two such
subtrees of a common super-tree can overlap each other.

* `(S disjoint-to T) ex-or (S related-to T)` if `(S != T)`
* if `R := (S & T)`, then `(R in {Ø,S,T})`

Note that, in the context of this discussion, the intersection between two
trees is, due to the above, required to either be empty (i.e. `Ø`) ex-or a
subtree of both input trees (i.e. not a forest of more than one trees).

<!-- ======================================================================= -->
## union (+, or, union)

* `(or: (Tree,Tree) -> Tree)` or `R := (S + T)`

The union of two trees is in general not a tree. That is, depending on both
input trees, the result may be a single tree, a non-empty forest of two trees,
or none of the two (i.e. a non-empty generic graph). Obviously, the goal is a
requirement that the result of a union operation is always a single tree.

A forest of trees is defined as the disjoint union of trees. The union of two
disjoint trees is therefore a disjoint union of trees and thus by definition
a forest. Consequently, both trees `S` and `T` must not be disjoint. That is,
both trees must have a non-empty intersection (i.e. a common subtree).

For two distinct trees `S` and `T` with root nodes `s` and `t`, the following
cases can be distinguished: (Case-1) `S` is a subtree of `T`, (Case-2) `T` is
a subtree of `S`, and (Case-3) both trees overlap each other.

Case-1/2: The result in these cases will be one of the input trees. That is
because a subtree can not add any new element to its super-tree. A subtree
would not be a subtree, if it had an element outside of its super-tree.

* `((S + T) == S)` if `(S == T)`
* `((S + T) == S)` if `(T subtree-of S)`
* `((S + T) == T)` if `(S subtree-of T)`

Case-3: If two trees overlap each other, then none is a subtree of the other.
Each tree therefore has one or more nodes the other tree does not have. Because
of that, the following cases can be distinguished: (Case-4) root `s` is not
equal to and not an ancestor of root `t`, (Case-5) `t` is not equal to and not
an ancestor of `s`, and (Case-6) `s` is an ancestor of `t`, or `t` an ancestor
of `s`.

Case-4/5: 

Note that, in the context of this discussion, the union of two trees is,
due to the above, required to yield a single tree.

<!-- ======================================================================= -->

Case-3: If both trees overlap each other in such a way that none of the root
nodes is a node of the other tree, then the result have a node with two "parent"
nodes (i.e. the root node of the intersection tree).

a non-tree graph. That is, because the resulting graph will have one or more
vertices with two incoming edges.

The order of operations is relevant (i.e. non-associative)

Likewise, and due to the above, `S` and `T` must not overlap each other.

Any tree can be defined as a sequence of union operations
unique sequences?

<!-- ======================================================================= -->
## graph difference (\, sub, diff)
