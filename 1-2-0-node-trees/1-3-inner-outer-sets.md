
<!-- ======================================================================= -->
# The inner/outer set of a node/tree

* (/see/ "hierarchy of sets" /)

<!-- ======================================================================= -->
## inner/outer set of a node

The set of inner nodes `IN(n)` of node `n` in a tree `T := (N,E)` will be
referred to as **the inner set (of a node)** `IS(n)`. In contrary to that,
the union of a node with its inner set of nodes will be referred to as
**the outer set (of a node)** `OS(n)`.

* `IS(n) := IN(n) := D(n)`
* `OS(n) := (IS(n) union {n})`
* i.e. `(#OS(n) >= 1)` and `(OS(n) != ON(n))`
* where `ON(n)` is the set of outer nodes of node `n`

Note that the outer set of a tree's root is equal to a tree's complete
set of nodes `N` - i.e. `(OS(r) == N)` if `(r == RN(T))`.

Note that `n` will be referred to as **the defining node** of its inner and
its outer set. That is, both sets are defined as: "All the nodes that can be
reached beginning with, and including (or excluding) the defining node".

`IS(n)` and `OS(n)` only differ in the defining node `n`. Because of that, the
inner set of a node is a strict subset to its outer set. In addition to that,
the outer set of a descendant `d` of node `n` is a strict subset to the outer
sets of its ancestors.

* `(#IS(n) == #OS(n)-1)`
* `(IS(n) strict-subset-of OS(n))`
* `(OS(d) strict-subset-of OS(n))`, if `(d descendant-of n)`

Note that the outer sets of siblings are disjoint. That is because no descendant
of a node is also a descendant of the node's siblings. (The rooted paths of both
nodes split apart in the node's parent). For that to be false, a node would need
to have more than one parent. Hence, the inner set of a node is the disjoint
union of the outer sets of its child nodes.

* `(OS(n) disjoint-to OS(s))`, if `(s sibling-of n)`
* also, `(OS(n) disjoint-to OS(d))`, if `(d descendant-of s)`

Note that, if a parent has one child only, then the parent's inner set is equal
to the outer set of its child. Also, the inner sets of leaf nodes are empty.

* `(IS(n) == OS(c))`, if `(CN(n) == {c})`
* `(IS(l) == {})`, if `(l in LN)` - i.e. `(CN(n) == {})`
* where `CN(n)` is the set of child nodes of node `n`

<!-- ======================================================================= -->
## the set of inner/outer sets of a tree

By definition, the defining node `n` of an outer set `OS(n)` is always an
element of that set and unique to it. That is, no other outer set in a tree
has the exact same defining node. Because of that, any tree `T := (N,E)` can
be understood to have a set of outer sets (aka. **the set of outer sets of a
tree**) of exactly `#N` sets associated with it:

* `OS, OS(T) := { OS(n) | (n in N)  }`
* `(#OS == #N)` - i.e. one outer set per node

Note that, because all outer sets are non-empty, the following applies to all
pairs of sets `(s,t in OS)`:

* `(s disjoint-to t)` ex-or `(s related-to t)`
* `(s disjoint-to t)` ex-or `(s strictly-related-to t)`, if `(s != t)`
* `(s overlaps t)` is always false

In contrary to that, the defining node `n` of an inner set `IS(n)` is never an
element of such a set. Because of that, a non-empty inner set is unique to its
defining node. However, an empty inner set does not necessarily have a unique
defining node. Hence, a tree `T := (N,E)` may also be understood to have a set
of inner sets (aka. **the set of inner sets of a tree**) of possibly fewer than
`#N` sets associated with it:

* `IS, IS(T) := { IS(n) | (n in N) }`
* `(#IS <= #N)` - i.e. not necessarily one set per node

Note that, with regards to the relationships between its sets, `IS(T)` is
not as clear as `OS(T)`. That is because the inner set of any leaf is empty.
(Note that the empty set `{}` is disjoint-to, but still related-to any other
set). Hence, the following applies to all pairs of sets `(s,t in IS)`:

* `(s disjoint-to t)` and/or `(s related-to t)`
* `(s disjoint-to t)` and/or `(s strictly-related-to t)`, if `(s != t)`
* `(s overlaps t)` is always false

<!-- ======================================================================= -->
## a visual representation

**Memory hook**
In order to imagine the set of outer sets `OS(T)`, try the following:

* Draw a node tree onto a piece of paper.
* Surround the whole tree with a border.
* Similar to that, draw a border around the tree of each node.
* Note that any border surrounds a node and all of its descendants.
* Note that there are no two borders that cross each other.
* Each border represents a set of nodes, if all edges are removed.
* The set of borders represents the tree's set of outer sets.

Example:

```
the initial node tree      the resulting set of borders
=====================  =>  ============================

     1                      |-----------------------|
 ----------                 | 1     |-------------| |
 2      3                   | |---| | 3           | |
      -----                 | | 2 | | |---| |---| | |
      4   5                 | |---| | | 4 | | 5 | | |
                            |       | |---| |---| | |
                            |       |-------------| |
                            |-----------------------|
```
