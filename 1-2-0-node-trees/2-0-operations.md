
<!-- ======================================================================= -->
# Operations on trees

Recall that the overall focus is on the subtrees of a document tree.
In addition to that, each subtree is in general assumed to be induced
by its root node (i.e. `S := T[r]`, i.e. `S := T[OS(r)]`).

Any operation on a tree is by definition an operation on the graph of a tree.
Because of that, and unless stated otherwise, any operation defined to operate
on one or more graphs can in general be used in the context of trees.

Recall that, if two graphs have an edge in common, then both graphs also have
both of the endpoints of that edge in common. In contrary to that, two graphs
may have one or more vertices, but no edge in common.

The execution of binary operations on two or more graphs must also take the
semantics of the input graphs into account. Because of that, the semantics of
the input graphs are by default expected to correspond with each other. That
is, the semantics are expected to be similar, if not identical. Put differently,
the semantics of two or more input graphs are expected to not be in conflict
with each other.

<!-- ======================================================================= -->
## requirements

Because issues arise, if arbitrary trees are processed (i.e. arbitrary sets of
nodes and arbitrary connections between those nodes), the following conditions
are considered to be requirements of the operations mentioned below:

(1) The nodes in trees `S` and `T` must be connected in a similar fashion.
That is, if trees `S` and `T` have nodes `a` and `b` in common, and if `S` has
a path `p := aPb`, then that path `p` must also exist in `T`. The main focus is
that `a` can not be an ancestor of `b` in `S` and a descendant of `b` in `T`.

(2) Node trees `S` and `T` must have the same child order. That is, if trees
`S` and `T` have nodes `a` and `b` in common, and if `b` is the next sibling
of `a` in `S`, then `b` must also be the next sibling of `a` in `T`. The main
focus is that `a` can not be presequent to `b` in `S` and subsequent to `b`
in `T`. (Note that this aspect can obviously only apply to ordered trees).

(3) The non-empty intersection between two trees `S` and `T` must be a tree.
The main focus is that the non-empty intersection between both trees is a
subtree to both and not a forest of two or more subtrees, or even a non-tree
graph.

(4) If the result of a binary operation on trees `S` and `T` is a graph, then
the resulting graph `R` must be a tree. That is, any operation is expected to
return an empty graph, or a single node tree.

<!-- ======================================================================= -->
## unary operations

Any tree can be transposed. However, the resulting converse graph `T°` is not
a tree. The converse graph of a tree has the "child-of" semantics, which is
because a child becomes the parent of its former parent.

Similar to that, the complement graph `T*` of a tree is not a tree. That is
because the nodes in such a complement graph have in general "more than one
parent" node.

<!-- ======================================================================= -->
## binary operations

The following boolean, graph-based operations may be used without limitation:

* equal, unequal, distinct
* disjoint, coupled, subgraph-of, overlap

Tree `S` is a **subtree** of graph `T`, if `S` is a subgraph of `T`:

* `(S subtree-of T) := (S subgraph-of T) and (isTree(S) == true)`
* note - `T` is not required to be a tree

Two trees `S` and `T` are said to be **related** with each other,
if one is a subtree of the other:

* `(S related-to T)`, if `(S subtree-of T)` or `(T subtree-of S)`
* `(S related-to T) <-> (T related-to S)`

Note that this `related-to` definition is more specific than the graph-based
definition since one input graph must be a subtree of the other. However, both
input graphs are in general expected to be node trees.

<!-- ======================================================================= -->
## union (+, or, union)

* `(or: (Tree,Tree) -> Tree)` or `R := (S + T)`

The union of two trees is in general not a tree. That is, depending on both
input trees, the result may be a single tree, a forest of two trees, or a
non-tree graph. The focus will obviously be on the requirement that the result
of a union of trees is a single tree.

A forest of trees is defined as the disjoint union of trees. The union of two
disjoint trees is therefore a disjoint union of trees and thus by definition
a forest. Consequently, both trees `S` and `T` must not be disjoint. That is,
both trees must have a non-empty intersection (i.e. a common subtree).

For two distinct trees `S` and `T` with root nodes `s` and `t`, the following
cases can be distinguished: (Case-1) `S` is a subtree of `T`, (Case-2) `T` is
a subtree of `S`, and (Case-3) both trees overlap each other (i.e. both trees
have a non-empty intersection and are still unrelated with each other).

Case-1/2: The result in these cases will be one of the input trees. That is
because a subtree can not add a new element to the union since all of its
nodes/edges are nodes/edges in its super-tree.

* `((S + T) == S)` if `(S == T)`
* `((S + T) == S)` if `(T subtree-of S)`
* `((S + T) == T)` if `(S subtree-of T)`

Note that this also includes the case in which both trees are equal. That
is because `(S subtree-of T)` and `(T subtree-of S)` are then both true.

Case-3: If two trees overlap each other, then none is a subtree of the other.
And because both trees are required to have a non-empty intersection, each
tree needs to have one or more nodes the other tree does not have. Because
of that, the following cases can be distinguished: (Case-4) root `t` is not
a node in `S`, (Case-5) root `s` is not a node in `T`, and (Case-6) `s` is
a node in `T` and/or `t` a node in `S`.

Case-4/5: If `t` is not a node in the outer set of `s`, then a node in the
non-empty intersection between both trees exists (i.e. the root of the common
subtree) that has two distinct parent nodes that are not common to both trees.
Because of that, the union of such trees would result in a non-tree graph as
that node would need to have two parent nodes in the resulting graph.
Consequently, the root of one tree must be a node in the other.

Case-6: If `s` is a node in `T`, then `S` must have leaf nodes not in `T` -
otherwise, Case-1/2 would apply. (Note that `T` must also have leaf nodes
not in `S`). The result in such a case is guaranteed to be a single tree
because in case of `(t ancestor-of s)`, new descendant nodes will be added
to one or more nodes in `T`.

Note that, in the context of this discussion, the union of two trees is,
due to the above, required to yield a single tree. Because of that, and
in `(S + T)`, **the root of T must be a node in S**.

<!-- ======================================================================= -->
## intersection (&, and, isect)

* `(and: (Tree,Tree) -> {Ø,Tree})` or `R := (S & T)`

Two distinct induced subtrees `S` and `T` of a common super-tree `U` (i.e.
`S := U[s]`, `T := U[t]` and `(s != t)`, such that `s` is the root of `S`
and `t` the root of `T`) can not overlap each other.

To proof that, the following cases need to be distinguished: (Case-1) `s`
is an ancestor of `t`, (Case-2) `t` is an ancestor of `s`, or (Case-3) `s`
is not an ancestor of `t`, and `t` not an ancestor of `s`.

Case-1/2: If `s` is an ancestor of `t`, then subtree `S` includes all the
nodes in `T`. Because of that, `T` is a proper induced subtree of `S`.
The intersection between `S` and `T` is therefore equal to `T`.

* `((S & T) == T)` if `(s ancestor-of t)`
* `((S & T) == S)` if `(t ancestor-of s)`
* i.e. `(S & T)` is in both cases a subtree of `S` and `T`
* `((S & T) != Ø) <-> (S related-to T)`

Case-3: Subtree `S` is induced by the outer set of node `s` and can therefore
not include any node in the outer set of `t`. Because of that, both subtrees
are disjoint. That is, the intersection between `S` and `T` is empty.

* `((S & T) == Ø)` if `(s !ancestor-of t)` and `(t !ancestor-of s)`

Consequently, two such subtrees are either disjoint ex-or one is a proper
induced subtree of the other. That is, the requirements of "overlaps" (i.e.
a non-empty intersection and still unrelated) can not be met. Because of
that, two such subtrees can not overlap each other.

* `(S disjoint-to T) ex-or (S related-to T)` if `(S != T)`
* if `R := (S & T)`, then `(R in {Ø,S,T})`

Note that, in the context of this discussion and due to the above, the
intersection between two trees **must either be empty ex-or a subtree to
both** (i.e. not a forest of more than one trees and not a non-tree graph).

<!-- ======================================================================= -->
## difference (\, sub, diff)

* `(sub: (Tree,Tree) -> {Ø,Tree})` or `R := (S \ T)`

Recall that, in the context of this discussion, the graph difference is based
upon the removal of vertices (i.e. the **vertex-based** definition). That is,
the result is defined as the removal of all the vertices in the 2nd operand
from the 1st operand, including the implicit removal of all the edges incident
to the vertices being removed.

Note that, due to its definition (i.e. remove the elements of the 2nd tree
from the 1st tree) this operation is **not commutative**. That is, the order
of both operands is relevant.

The difference of two trees is in general a forest of trees. That is, depending
on both input trees, the result may be empty, a single tree, or a forest of two
or more trees. Similar as before, the focus will be on the requirement that the
result of such an operation is either empty ex-or a single tree.

Obviously, if both input trees `S` and `T` are disjoint, then the result of
`(S \ T)` is equal to `S`. That is because `T` then has no elements that could
be removed from `S`. Because of that, both trees are in general expected to be
coupled with each other. And because `T` can be understood to be restricted the
common subtree, **T is expected to be a subtree of S**. The root of `T` is thus
expected to be a node in `S`.

* `((S \ T) == S)` if `(T == Ø)`
* `((S \ T) == S)` if `(T disjoint-to S)`

For two distinct trees `S` and `T` with root nodes `s` and `t`, the following
cases can be distinguished: (Case-1) `T` is equal to `S`, (Case-2) `T` is not
an induced subtree of `S` (i.e. `(T != S[t])`), and (Case-3) `T` is an induced
subtree of `S` (i.e. `(T == S[t])`).

Case-1: If `T` is equal to `S`, then the result of `(S \ T)` will be empty.
(Note that `T` can be understood to be an induced subtree of `S`:
`(T == S[t])` where `(s == t)`).

* `((S \ T) == Ø)` if `(T == S)`

Case-2: If `T` is not an induced subtree of `S` (i.e. `(T != S[t])`), then `T`
is guaranteed to have a leaf `l` that is a node, but no leaf in `S`. (Recall
that `T` is thought of as being restricted to the non-empty intersection between
`S` and `T` - i.e. `T == (S & T)`). Because of that, the result of `(S \ T)`
will contain an induced subtree for each child of `l` in `S` (i.e. `S[c]` where
`(c child-of l)`). The result is therefore in general a forest of trees.

However, (1) if `t` is equal to `s`, and (2) if `T` has only one leaf `l`
that is a parent (and therefore no leaf) in `S`, and (3) if `l` only has a
single child `c` in `S`, then the result of `(S \ T)` will be a single tree
(i.e. `R == S[c]`). That particular case however is outside of the scope of
this discussion since the focus is on conditions that are in general true,
rather than on conditions that are true in a very particular case.

Case-3: Because `T` is an induced subtree of `S` (i.e. `(T == S[t])`), `T`
is guaranteed to have all the descendants of `t` in `s`. Because of that, the
result of `(S \ T)` can not contain any tree that is induced by a descendant
of `t` in `S`. Hence, the result is guaranteed to either be empty (i.e. if
`(s == t)`) ex-or a single tree (i.e. `(S \ S[t])`).

Note that, in the context of this discussion, the difference between two trees
is, due to the above, required to either be empty ex-or a single tree. Because
of that, and in `(S \ T)`, **T must be an induced subtree of S**.
