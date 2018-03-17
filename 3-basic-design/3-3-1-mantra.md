
<!-- ======================================================================= -->
# Mantra

The purpose of a mantra introduced below is to guide ones thoughts to the
aspects that are relevant in a given context (i.e. a psychological tool):

```
< root <       tree/path-of-nodes      > leaf >
> parent-of >                      < child-of <
> contains >                     < belongs-to <

R x N x ... x N x N x ... x N x N x ... x N x L
```

A rooted path defined on a rooted tree begins with the tree's root node
`r in R in N` and connects that root with one of its child nodes `c in N`.
Any other hop connects a parent node `p in N` with one of its child nodes
`c in N` until that path ends in its final node `f in N`. This last node may
itself have further child nodes, or none at all. In the latter case, node `f`
is a leaf node `l in L in N`. In other words, such a path `p := (r,c,...,f)`
is an element of `RD := RxN{+}`.

Note that a rooted path that ends in a leaf node can be referred to as a RTL
(i.e. root-to-leaf) path.

```
R x N x ... x n x c1 x ... x N x L
                x c2 x N x L
```

At any non-leaf node `n`, a different path of any length may branch off: i.e.
paths `p1 := (r,...,n,c1,...,L)` and `p2 := (r,...,n,c2,...,L)` both share
the common prefix `pref := (r,...,n)`, but end in the different suffixes
`s1 := (c1,...,L)` and `s2 := (c2,...,L)`.

All nodes in `pref` are ancestors to any node in `s1` and `s2`.
Also, any node in `s1` or `s2` is descendant to any node in `pref`.
In addition to that, `c1` is a sibling of `c2` and vice versa.

If the corresponding tree of nodes is an ordered tree of nodes, then `c1` is
the previous sibling of `c2`, and `c2` the next sibling of `c1`. This however
depends on the order in which the paths are specified (e.g. upper paths are
presequent to lower paths).

Note that a rooted path `p1` can be understood to be presequent to another path
`p2`, if the last node `f1` of `p1` is presequent to the last node `f2` of `p2`.
That is, the order of rooted paths can be defined based on the order of the
corresponding last nodes.

```
R x N x ... x N x N x ... x N x N x ... x N x L
r x ...                                 ... x l
```

As a result, the `RxN{*}xL` line can be seen to represent a generic rooted
path, or even a complete tree of nodes. Which of these perspectives applies
depends on one's own current point of view.

<!-- ======================================================================= -->
## associations

```
.. x n x ...      (or)          s
     x                          x
     s                    ... x n x ...
```

In both cases, node `n` is strictly associated with section `s`.

```
r x ... x (n:s) x ...
```

In short, `n:s` means that node `n` is strictly (aka. directly, explicitly)
associated with section `s`.

```
r x ... x s x ...
```

And if the only thing that counts is, that some node is strictly associated
with section `s`, then a node identifier may even be dropped.
