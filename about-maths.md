
# Relations

The DOM tree is a tree data structure defined in terms of nodes and edges,
i.e. we are bound by the rules of discrete mathematics (graph theory)!

* Think in terms of tuples.
* (..., iif ...) := (... if, and only if, ...)

See also

* [en.wikipedia.org, graph theory](https://en.wikipedia.org/wiki/Graph_theory)
* [en.wikipedia.org, binary relation](https://en.wikipedia.org/wiki/Binary_relation)
* [en.wikipedia.org, tree structure](https://en.wikipedia.org/wiki/Tree_structure)
* [en.wikipedia.org, tree (graph theory)](https://en.wikipedia.org/wiki/Tree_%28graph_theory%29)
* [en.wikipedia.org, tree (data structure)](https://en.wikipedia.org/wiki/Tree_%28data_structure%29)

<!-- ======================================================================= -->
## Nodes and edges

```
<- root <-          path-of-nodes          -> leaf ->
<- parent-of                              child-of ->

... x N x N x ... x N x N x ...
```

* `n in N` is a node, `N` is the set of all nodes
* Each node `n1` (parent) is connected with another node `n2` (child)
* Edge `e := (n1,n2) = (p,c) in E subset-of NxN`
* Each node may be a parent - `p in P` and `P subset-of N`
* Each node may be a child - `c in C` and `C subset-of N`
* Each node may be a leaf - `l in L` and `L subset-of N`
* `P = N - L` => `n in P <=> n not in L` => `n not in P <=> n in L`
* A parent is no leaf, a leaf is no parent.
* A child can itself be a parent or a leaf.
* `P`, `C` and `L` are all not equal to `N`
* `PxL subset-of NxN` and `PxCxL subset-of NxNxN`
* One node must be the root - `r in P` and `(n,r) not in PxC` (has no parent)
* A reference to a node's parent node is required => rooted tree
* The child nodes of each node are ordered => ordered tree,
  left-to-right, first-to-last

For any path `p=(n1, n2, ..., nk) in NxNx...xN` such that `ni parent-of ni+1`
and `i in [1,k]` (i.e. top-down, e.g. root-to-leaf), `ni` is an ancestor of
`ni+1` and `ni+1` a descendant of `ni`.

For any path `p=(n1, n2, ..., nk) in NxNx...xN` such that `ni child-of ni+1`
and `i in [1,k]` (i.e. bottom-up, e.g. leaf-to-root), `ni` is a descendant of
`ni+1` and `ni+1` an ancestor of `ni`.

* strictly related to := directly related to
* loosely related to := there are nodes in between
* `a` is related to `b` if `a` is strictly, or loosely related to `b`.
* A parent is strictly related to its children.
* Any node is related to all of its ancestors.
* A child is strictly related to its parent.
* Any node is related to all of its descendants.

<!-- ======================================================================= -->
## Sections

```
<- root <-        path-of-nodes         -> leaf ->
<- parent-of                           child-of ->

... x N x N x ... x N x N x ...  (down) belongs-to
      x                      
      S                         (up) contains-node
```

* `s in S` is a section, `S` is the set of all sections
* The tree traversal connects each node with a section
  => first, last => order => `s = (n1,n2,...ni) in NxNx...xN`.
* In general, sections may have any length => `i in [0,+Infinity)`
* All sections in `S` may have any length => different lengths
* If `(n,s) in NxS`, then `s(k) = n` for some `k in [1,+Infinity)`
* Any node is directly (strictly) related to a section => `NxS`, left-total
* If `(n,s) in NxS`, then `(s,n) in SxN` (not left-total, empty section)
* The nodes of a section do not have to be located on the same path
  (special case - a single HTML node, a container with a single node, etc.).
* Two empty sections are not necessarily identical
  => each section depends on a sectioning node (introduces/declares a section)
  => two different sectioning nodes may each introduce its own empty section

strictly related-to

* A node strictly belongs to a section, iif it is strictly related to it.
* A node is located inside of a section, if it strictly belongs to it.
  However, a node may also be seen to be located inside of a section, if it
  loosely belongs to it - this depends on someone's point of view.
* A section strictly contains a node, iif the node is related to it => `SxN`.

loosely related-to

* Any descendant `d` of node `n`, which is strictly related to section `s`
  (i.e. `(n,s) in NxS`), *loosely belongs to* `s`.
* A section `s` loosely contains node `n`, iif `n` loosely belongs to `s`.

```
example
=======
... section-A begins here
<parent-B>          => is located inside
  <descendant-C>    => is located inside
  </descendant-C>
</parent-B>
... section-A ends here
```
* Any ancestor `a` of node `n`, which is strictly related to section `s`
  (i.e. `(n,s) in NxS`), *does not loosely belong to* `s`.
* However, `a` may still be strictly related to it (i.e. `(a,s) not in NxS`).

```
example
=======
<root>        => does not belong to section-A
... section-A begins here
  <node-B>    => is located inside
  </node-B>
... section-A ends here
</root>
```

<!-- ======================================================================= -->
## Conclusion

<!-- ======================================================================= -->
## A memory hook

```
<- root <-          path-of-nodes          -> leaf ->
<- parent-of                              child-of ->

... x N x N x ... x N x N x ...    (down) belongs-to
      x             x
... x S x S x ... x S x S x ...    (up) contains-node

<- parent-section                      sub-section ->
```
