
<!-- ======================================================================= -->
# Single associations

What effects does it have,
if node `n` is associated with section `s`?

<!-- ======================================================================= -->
## pi := s -> nx

```
r x ... x (n:s) x ...
```

Section `s in S` strictly contains node `n` because it is directly connected
with it. That statement is however a direct result of the `SxN` relation and,
as such, does not state anything new.

<!-- ======================================================================= -->
## pa: (n-k) -> s

```
r x ... x (n-k) x ... x (n-1) x (n:s) x ...
```

A path `pa` can be defined that connects
the ancestors of node `n` with section `s`.

*  `pa := (n-k,...,n,s) in N{+}S`
* `(n-k) ... contains ... (n) belongs-to (s)`

The same applies, if such a path is inverted:

* `pa' := (s,n,...,n-k) in SN{+}`
* `(s) contains (n) ... belongs-to ... (n-k)`

Here, the relations used to create such a path have antonymous semantics
(i.e. `contains` vs. `belongs-to`). Such a path is said to be inconsistent.

<!-- ======================================================================= -->
## clarification

The reason why no clear conclusion can be drawn is, that the ancestors of node
`n` may have any number of nodes that are descendant to the root `r`, but that
are not ancestral (i.e. not in `prefixOf(pa)`) to it. Hence, a path `p` could
be defined which connects some node `o` with section `s`

* `p := (o,...,r,...,n-k,...,n,s) in N{+}S`
* `(o) ... belongs-to ... (r) ... contains ... (nx) belongs-to s`

Obviously, such a path would be even more inconsistent.

<!-- ======================================================================= -->
## pd: s -> (n+k)

```
r x ... x (x:s) x (x+1) x ... x (x+k) x ...
                x (y+1) x ... x (y+l) x ...
```

A path `pd` can be defined that connects
section `s` with nodes that all are descendant to `n`:

* `pd .= (s,x,...,x+k) in SN{+}`
* `(s) contains (x) ... contains ... (x+k)`

The same applies, if such a path is inverted:

* `pd' := (x+k,...,x,s) in N{+}S`
* `(x+k) ... belongs-to ... (x) belongs-to s`

Here, the relations used to create such a path have equivalent semantics!
Such a path is said to be consistent.

<!-- ======================================================================= -->
## clarification

Section `s` loosely contains any descendant of node `x`,
if section `s` strictly contains node `x`.

* `(s strictly-contains x)` and `(s loosely-contains (x+i))`
* `(s contains x)` and `(s contains (x+i))`

Any descendant of node `x` loosely belongs to section `s`,
if node `x` strictly belongs to section `s`.

* `(x strictly-belongs-to s)` and `((x+i) loosely-belongs-to s)`
* `(x belongs-to s)` and `((x+i) belongs-to s)`

Node `y` loosely belongs to section `t`, if `y` is a descendant of node `x`
and if `x` strictly belongs to `t`:

* `(y loosely-belongs-to t)`, if some `x in N` exists
  such that `(x ancestor-of y)` and `(x strictly-belongs-to t)`

Consequently, any node automatically loosely belongs to any section that
strictly contains any of its ancestors. Each node may therefore belong to
any number of sections.

These loose relationships can not be undefined because they will be established
automatically as soon as any ancestor is associated with a section.

The only method to break up these loose relationships is to change the structure
of the node tree. Obviously, that is not allowed because the purpose of these
associations is ultimately to represent the tree's structure as is.

<!-- ======================================================================= -->
## Multiple associations (s)

What effect does it have,
if multiple different nodes are associated with the same section `s`?

```
r x ... x (x):s x (x+1):s x ... x L
                x ... x (y):s x ... x L
                      x ... (z):s x ... x L
```

If some node `x` is strictly associated with section `s`, then any descendant
of `x` is already loosely related to `s`. As a result, descendant nodes of `x`
do not have to be strictly associated with the same section, if the distinction
between a "strict" and a "loose" relationship is not relevant.

Memory hook:
Associating a single node is equivalent to associating a whole subtree of nodes
whose root is the strictly associated node.

With that in mind, and in this context, any rooted path can be reduced to a path
that ends with a strictly associated node, because the remainder of a path, that
passes through such a node, will not change the path's characteristics any
further.

```
r x ... x (x:s)
```

Consequently, a path that is not supposed to fall into the same category must
branch off from some common prefix before the first associated node is reached.
That is, a second path may branch off beginning with the parent of an associated
node and up until the root of the node tree.
