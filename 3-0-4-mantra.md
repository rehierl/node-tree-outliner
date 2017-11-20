
<!-- ======================================================================= -->
# Mantra

The purpose of the mantra introduced below is to guide ones thoughts to the
basic principles of the corresponding relations:

```
< root <          path-of-nodes        > leaf >
> parent-of >                      < child-of <
> contains >                     < belongs-to <

R x N x ... x N x N x ... x N x N x ... x N x L
```

A rooted path defined on a rooted tree begins with the tree's root node
`r in R in N` and connects that root with one of its child nodes `c in N`. Any
other jump in such a path connects a node `n in N` with one of its child nodes
`c in N`. Such a path may end at any node `n`, or it may continue until a leaf
node `l in L in N` is reached. In other words, such a path `p` is an element of
`RD := RxN{+}`.

```
R x N x ... x p1 x c1 x ... x N x L
                 x c2 x N x L
```

At any non-leaf node `p1`, a different path of any length may branch off: i.e.
paths `p1 := (R,...,p1,c1,...,L)` and `p2 := (R,...,p1,c2,...,L)` both share
the common prefix `pref1 := (R,...,p1)` but end in a different suffix. Hence,
all nodes in `pref1` are ancestors to any nodes in `s1 := suffixOf(p1,#p1-#pref)`
and `s2 := suffixOf(p2,#p2-#pref)`. Also, any node in `s1` is descendant to any
node in `pref1`. Likewise, any node in `s2` is descendant to any node in `pref`.
And finally, `c1` is a sibling of `c2`.

```
R x N x ... x n x p1 x c1 x ... x N x L
                x p2 x c3 x N x L
```

Even though path `p3 := (R,...,c3,...L)` does share a common prefix
`pref2 := (R,...,n)` with path `p1`, `c1` is not a sibling of `c3`.

```
R x N x ... x N x N x ... x N x N x ... x N x L
r x a x ...                         ... x z x l
```

As a result, the `RxN{*}xL` line can be seen to represent a specific rooted
path, or even a complete tree of nodes. Which of these perspectives applies
depends on one's own current point of view.

<!-- ======================================================================= -->
## Extension

What effects does it have,
if some node `nx` is associated with some section `s`?

```
< root <                path-of-nodes                 > leaf >
> parent-of >                                     < child-of <
> contains >                                    < belongs-to <

                     s                         (down) contains
                     x
... x (nx-k) x ... x nx x ... x (nx+k) x ...   (up) belongs-to
                        x ... x (ny+l) x ...
```

### pi := s -> nx

Due to the strict association between section `s` and node `nx`, it can be
stated right away, that section `s` strictly contains node `nx`.

**no conclusion**

That statement is however a direct result of the `SxN` relation and, as such,
does not state anything new.

### pa: (nx-k) -> nx -> s

A path `pa` can be defined that connects
the ancestors of node `nx` with section `s`.

*  `pa := ((nx-k),...,(nx),s) in N{+}S`
* `(nx-k) ... contains ... (nx) belongs-to (s)`

The same applies, if such a path is inverted:

* `pa' := (s,(nx),...,(nx-k)) in SN{+}`
* `(s) contains (nx) ... belongs-to ... (nx-k)`

Here, the relations used to create such a path have antonymous semantics
(i.e. `contains` vs. `belongs-to`)! Such a path is said to be inconsistent.

**no conclusion**

A path `p` could be defined that connects
some node `n` (descendant to `r`, but not ancestral to `nx`) with section `s`

* `p := (n,...,r,...,(nx-k),...,(nx),s) in N{+}S`
* `(n) ... belongs-to ... (r) ... contains ... (nx) belongs-to s`

Obviously, such a path would be even more inconsistent.

### pd: s -> nx -> (nx+k)

A path `pd` can be defined that connects
section `s` with nodes that all are descendant to node `nx`:

* `pd .= (s,(nx),...,(nx+k)) in SN{+}`
* `(s) contains (nx) ... contains ... (nx+k)`

The same applies, if such a path is inverted:

* `pd' := ((nx+k),...,(nx),s) in N{+}S`
* `(nx+k) ... belongs-to ... (nx) belongs-to s`

Here, the relations used to create such a path have equivalent semantics!
Such a path is said to be consistent.

<!-- ======================================================================= -->
## Conclusion

A section, that is strictly related to a node is
also loosely related to any descendant of that node:

* `(s related-to nx)` and `(s related-to (nx+i))`

Consequently, any node is automatically loosely related to any section
that is strictly related to any of the node's ancestors:

* `(nx related-to s)` and `((nx+i) related-to s)`
* `(ny related-to t)` for any `t in S`, if `nx in N` exists
  such that `(nx ancestor-of ny)` and `(nx related-to t)`

These loose relationships can not be undefined because they will be established
as soon as a node is directly associated with a node. The only way to undefine
these loose relationships would be to change the structure of the node tree.
Obviously, that is not allowed because the purpose of these kind of associations
is ultimately to accurately represent a tree's structure.

As a result, it is not necessary to explicitly associate a node `d` with section
`s`, if `d` is descendant to an ancestral node `a` which itself is strictly
associated with said section. An explicit association is not necessary because
`d` is already loosely related to `s`.

Likewise, 

<!-- ======================================================================= -->
## Extension

What effects does it have,
if some node `nx` is associated with section `s` and
if some node `ny` (descendant to `nx`) is associated with section `t`?

```
< root <                path-of-nodes                 > leaf >
> parent-of >                                     < child-of <
> contains >                                    < belongs-to <

          s                  t                 (down) contains
          x                  x
... x N x nx x N x ... x N x ny x N x ...      (up) belongs-to
                 x ... x N x nz x ...
```

This merely reflects that any descendant of `n2` belongs to section `s1` and
section `s2` at the same time. However, the same does not apply to any
descendant of `n1` that is also descendant of `n2`.
