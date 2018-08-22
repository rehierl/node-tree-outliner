
<!-- ======================================================================= -->
# TODO - sequences

you would if you could, but you won't because you can't
- https://en.wikipedia.org/wiki/List_of_unsolved_problems_in_mathematics

a set-based definition of sequences
- Kuratowski's definition
- based on the subset-of relationship

relationship with interval order
- intervals represent parts of an ordered set

sequences define trees - direct edges
- (f: Index -> Index)
- (f := { (a,b) | (b = f(a)) }
- (a,b) = (a child-of b)

sequences define trees - nested intervals
- (f: Index -> Length)
- (a,b) = node sequence of node a has length b
- node sequence of node a is a subsequence of the root's sequence

<!-- ======================================================================= -->
## set of sequences

trees, orders
- define "(strict) subtree", "(strict) suborder"?
- compare node order of a subtree -vs- node order of a tree

drawing borders around subtrees
- a hierarchy of subtrees based on the subtree-of operator
- translates directly into a hierarchy of sets of nodes

ordered sequences
- a tree's node order -vs- a traversal's node/visit/enter order
- proof that: node order <-> visit order <-> enter order
- the issue: a node is a single unit - vs. enter and exit events

properties of (s in S)
- all sequences have the same order
- define "suborder" - order embedding?

define
- set-based operators for ordered sequences?

<!-- ======================================================================= -->
## more than "sequences"

* `s = [ e1, ..., eN ]` for `(s in ×Ti)`
* `(f: (×Ti,Index) -> Element)`
* note - closely related to orders
* note - distinct elements may hold the same value
* i.e. a sequence is a group of elements paired with an order-relation
* sequences represent ordered multisets - nope
* sequences may represent ordered sets
