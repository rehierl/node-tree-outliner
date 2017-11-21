
<!-- ======================================================================= -->
# Mantra

The purpose of a mantra introduced below is to guide ones thoughts to the
relevant relations:

```
< root <          path-of-nodes        > leaf >
> parent-of >                      < child-of <
> contains >                     < belongs-to <

R x N x ... x N x N x ... x N x N x ... x N x L
```

A rooted path defined on a rooted tree begins with the tree's root node
`r in R in N` and connects that root with one of its child nodes `c in N`.
Any other hop connects a parent node `p in N` with one of its own child nodes
`c in N` until that path ends in its final node `f in N`. This last node may
itself have further child nodes, or none at all. In the latter case, node `f`
is a leaf node `l in L in N`. In other words, such a path `p := (r,c,...,f)`
is an element of `RD := RxN{+}`.

```
R x N x ... x n x c1 x ... x N x L
                x c2 x N x L
```

At any non-leaf node `n`, a different path of any length may branch off: i.e.
paths `p1 := (r,...,n,c1,...,L)` and `p2 := (r,...,n,c2,...,L)` both share
the common prefix `pref := (r,...,n)`, but end in the different suffixes
`s1 := suffixOf(p1,#p1-#p)` and `s2 := suffixOf(p2,#p2-#p)`.

All nodes in `p` are ancestors to any nodes in `s1` and `s2`. Also, any node
in `s1` or `s2` is descendant to any node in `p`. In addition to that, `c1`
is a sibling of `c2` and vice versa.

If the corresponding tree of nodes is an ordered tree of nodes, then `c1` is
the previous sibling of `c2`, and `c2` the next sibling of `c1`. This however
depends on the order in which the paths are specified (e.g. upper paths are
presequent to lower paths).

```
R x N x ... x N x N x ... x N x N x ... x N x L
r x a x ...                         ... x z x l
```

As a result, the `RxN{*}xL` line can be seen to represent a specific rooted
path, or even a complete tree of nodes. Which of these perspectives applies
depends on one's own current point of view.

<!-- ======================================================================= -->
## Single association

What effects does it have,
if some node `nx` is associated with some section `s`?

```
< root <                path-of-nodes                 > leaf >
> parent-of >                                     < child-of <
> contains >                                    < belongs-to <

                     s                         (down) contains
                     x
... x (nx-k) x ... x nx x ... x (nx+k) x ...   (up) belongs-to
                        x ... x (nx+l) x ...
```

### pi := s -> nx

Section `s in S` strictly contains node `nx` because it is directly connected
with it. That statement is however a direct result of the `SxN` relation and,
as such, does not state anything new.

### pa: (nx-k) -> nx -> s

A path `pa` can be defined that connects
the ancestors of node `nx` with section `s`.

*  `pa := (nx-k,...,nx,s) in N{+}S`
* `(nx-k) ... contains ... (nx) belongs-to (s)`

The same applies, if such a path is inverted:

* `pa' := (s,nx,...,nx-k) in SN{+}`
* `(s) contains (nx) ... belongs-to ... (nx-k)`

Here, the relations used to create such a path have antonymous semantics
(i.e. `contains` vs. `belongs-to`). Such a path is therefore said to be
inconsistent.

The reason why no clear conclusion can be drawn at this point is, that the
ancestors of node `nx` may have any number of nodes that are descendant to the
root `r`, but are not ancestral (i.e. not in `prefixOf(pa)`) to it. Despite
that, a path `p` could be defined which connects such node `n` with section `s`

* `p := (n,...,r,...,nx-k,...,nx,s) in N{+}S`
* `(n) ... belongs-to ... (r) ... contains ... (nx) belongs-to s`

Obviously, such a path would be even more inconsistent.

### pd: s -> nx -> (nx+k)

A path `pd` can be defined that connects
section `s` with nodes that all are descendant to `nx`:

* `pd .= (s,nx,...,nx+k) in SN{+}`
* `(s) contains (nx) ... contains ... (nx+k)`

The same applies, if such a path is inverted:

* `pd' := (nx+k,...,nx,s) in N{+}S`
* `(nx+k) ... belongs-to ... (nx) belongs-to s`

Here, the relations used to create such a path have equivalent semantics!
Such a path is said to be consistent.

<!-- ======================================================================= -->
## CONCLUSION

Because of that, a section that strictly contains a node does also loosely
contain any descendant of that node:

* `(s contains nx)` and `(s contains (nx+i))`
* `(s related-to nx)` and `(s related-to (nx+i))`

Consequently, any node is automatically loosely related to any section
that is strictly related to any of the node's ancestors:

* `(nx related-to s)` and `((nx+i) related-to s)`
* `(ny related-to t)` for any `t in S`, if `nx in N` exists
  such that `(nx ancestor-of ny)` and `(nx related-to t)`

The loose relationships can not be undefined because they will be established
as soon as any ancestral node is directly associated with some section.

The only way to undefine these would be to change the structure of the node
tree. Obviously, that is not allowed because the purpose of these kind of
associations is ultimately to represent the tree's structure as is.

<!-- ======================================================================= -->
## Simplifications

```
                     s
                     x
... x (nx-k) x ... x nx x ... x (nx+k) x ...
```

To simplify the notation,
assume that the following fragment has the exact same meaning:

```
... x (nx-k) x ... x (nx):s x ... x (nx+k) x ...
```

That is, `(nx):s` (or simply `nx:s`) means that node `nx` is directly
(aka. strictly, explicitly) associated with section `s`.

```
... x N x ... x N x s x N x ... x N x ...
```

If the only thing that counts is that some node is strictly associated with
section `s`, then the node identifier may even be dropped completely.

<!-- ======================================================================= -->
## Multiple associations

```
             x (ny+1):s x ...
... x (nx):s x ... x (nx+k):s x ...
             x ... x ... x (nz+j):s x ...
```

If some node `nx` is explicitly associated with section `s`, then any descendant
node `(nx+k)` is already loosely associated with it. If the distinction
between "strict" and "loose" is not required, then node `(nx+k)` does not have
to be strictly associated with section `s`. Under these circumstances, the above
fragment is equivalent to: `... x (nx):s x ...`.

```
... x N x ... x n x c1:s x ... x N x ...
                  x c2:s x ...
```

If no other node in the whole tree is strictly associated with section `s`, then
node `n` is the section's sectioning node. 

asdf

```
... x N x ... x n1 x c1:s x ... x N x ...
              x n2:s x ...
```

asdf

```
... x N x ... x n1 x c1:s x ... x N x ...
              x n2:s x ...
```

<!-- ======================================================================= -->
## Multiple sections

What effects does it have,
if some node `nx` is associated with section `s` and
if some descendant node `ny` is associated with section `t`?

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
