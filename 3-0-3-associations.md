
<!-- ======================================================================= -->
# Associations

A process of some sort is required to visit the nodes of a tree in some
particular order (=> tree traversal). As a result, there is some node in a
non-empty tree, that will be visited first and some node that will be visited
last. Consequently, any node, except for the first and last nodes themselves,
is subsequent to the first and presequent to the last node (=> node sequence).

* `ns := [n1,...,nk]`, `ni in N`, `ns in N^k`
* `n1` was visited first and `nk` was visited last

At some point in the above process, nodes will be visited that introduce a new
section (=> sectioning nodes).

* Any sectioning node always declares/introduces a single new section.
* No section can exist without first being declared by its sectioning node.
* There is a one-to-one (i.e. 1:1) relationship between the sectioning nodes
  and the sections they declare.
* Any section can be identified by its sectioning node.

Once a sectioning node is reached, any subsequent node may be associated with
the sectioning node's section.

* A sectioning node is insequent, and therefore not subsequent, to itself.
* A sectioning node binds its section to presequent nodes/sections.
* Nodes will potentially be associated with multiple predeclared sections.

Naturally, some rules are required that allow to determine with which section,
or multiples thereof, a node must be associated. For the moment, it can only be
assumed that such rules exist.

If the these rules allow to determine that some node `n` must be associated
with some section `s`, then node `n` must be added to section `s` as one of
its elements. From that point on, `(s related-to n)` is true.

* A section is related to a node (and vice versa)
  as soon as the node is added to the section.
* No section can contain a node multiple times.

Because nodes are visited in some particular order and because nodes are
associated with sections in an order that is based upon the visit order, the
general definition of a section can be clarified as a sequence of nodes:

* `s := [n1,...,nk]` and `(ni != nj)` for `i,j in [1,k]` and `(i != j)`
* Any non-empty section always has a first and a last node.

However, the order of nodes within a section must reflect the order of nodes
within the tree of nodes. After all, any section is intended to accurately
represent some part of the node tree.

<!-- ======================================================================= -->
## Mantra

What effects does it have,
if some node `ni` is associated with some section `s`?

```
< root <                path-of-nodes                 > leaf >
> parent-of >                                     < child-of <
> contains >                                    < belongs-to <

... x (ni-k) x ... x (ni-1) x ni x (ni+1) x ... x (ni+k) x ...
                              x
                              s
```

### pi := s -> ni

Due to the strict association between section `s` and node `ni`, it can be
stated right away, that section `s` strictly contains node `ni`.

**no conclusion**

That statement is however a direct result of the `SxN` relation and, as such,
does not state anything new.

### pa: (ni-k) -> ni -> s

A path `pa` can be defined that connects
the ancestors of node `ni` with section `s`.

*  `pa := ((ni-k),...,(ni),s) in N{+}S`
* `(ni-k) ... contains ... (ni) belongs-to (s)`

The same applies, if such a path is inverted:

* `pa' := (s,(ni),...,(ni-k)) in SN{+}`
* `(s) contains (ni) ... belongs-to ... (ni-k)`

Here, the relations used to create such a path have antonymous semantics (i.e.
`contains` vs. `belongs-to`)! Such a path is said to be inconsistent.

**no conclusion**

A path `p` could be defined that connects
some node `n` (descendant to `r`, but not ancestral to `ni`) with section `s`

* `p := (n,...,r,...,(ni-k),...,(ni),s) in N{+}S`
* `(n) ... belongs-to ... (r) ... contains ... (ni) belongs-to s`

Obviously, such a path would be even more inconsistent.

### pd: s -> ni -> (ni+k)

A path `pd` can be defined that connects
section `s` with nodes that all are descendant to node `ni`:

* `pd .= (s,(ni),...,(ni+k)) in SN{+}`
* `(s) contains (ni) ... contains ... (ni+k)`

The same applies, if such a path is inverted:

* `pd' := ((ni+k),...,(ni),s) in N{+}S`
* `(ni+k) ... belongs-to ... (ni) belongs-to s`

Here, the relations used to create such a path have equivalent semantics!
Such a path is said to be consistent.

**conclusion**

A section, that is strictly related to a node is
also loosely related to any descendant of that node:

* `(s related-to ni)` and `(s related-to (ni+j))`

Consequently, any node is loosely related to any section that is
strictly related to any of the node's ancestors:

* `(ni related-to s)` and `((ni+j) related-to s)`
* `(ny related-to t)` for any `t in S`, if `nx in N` exists
  such that `(nx ancestor-of ny)` and `(nx related-to t)`

<!-- ======================================================================= -->
## Mantra

What effects does it have,
if some node `ni` is associated with section `s` and
if some node `nj` (descendant to `ni`) is associated with section `t`?

```
< root <                path-of-nodes                 > leaf >
> parent-of >                                     < child-of <
> contains >                                    < belongs-to <

... x N x ni x N x ... x N x nj x N x ...
          x                  x
          s                  t
```
