
<!-- ======================================================================= -->
## An inaccurate mantra (1)

* Just a pictogram to guide ones thoughts.
* Yuo can sitll raed tihs! (= try to grasp its essence)

```
< root <          path-of-nodes        > leaf >
> parent-of >                      < child-of <

R x N x ... x N x N x ... x N x N x ... x N x L
```

* `RxNx...xNxL` can be seen to represent all the RTL paths of a tree.
* At any non-leaf node, a path of any length may branch off:

```
            ... x N x N x L
R x N x ... x N x N x ... x N x L
        ... x N x N x N x L
  ... x N x N x N x N x L
```

It depends on the current context how one needs to look at it.

* `...xNxNx...` can be seen to represent an infinite set of paths that all
  share some common prefix (same ancestors), but (beginning with some node)
  branch off into different suffixes (different descendants).
* `Rx...xL` can also be seen to represent a single path only.

<!-- ======================================================================= -->
## An inaccurate mantra (2)

```
< root <           path-of-nodes         > leaf >
< parent-of <                        > child-of >

R x n1 x ... x N x n2 x ... x N x L   (down) belongs to
    x              x
    s1             s1                 (up) contains node
```

* `r in R` can not be associated with any section
  because that section would have no sectioning node.

This extension implies that any descendant of a node `n1`, which is directly
related to a section `s1`, is naturally loosely related to the same section.

* A strict relation `(n2,s1)` is not required,
  because `n2` is, due to `(n1,s1)`, already related to `s1`.
* Any node automatically belongs to a section,
  if that section directly contains any of the node's ancestors.

```
< root <           path-of-nodes         > leaf >
< parent-of <                        > child-of >

R x n1 x ... x N x n2 x ... x N x N x ... x N x L
    x              x
    s1             s2
```

This merely reflects that any descendant of `n2` belongs to section `s1` and
section `s2` at the same time. However, the same does not apply to any
descendant of `n1` that is also descendant of `n2`.
