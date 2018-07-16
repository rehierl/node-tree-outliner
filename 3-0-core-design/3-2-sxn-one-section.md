
<!-- ======================================================================= -->
# Single associations

What effects does it have,
if node `n` is associated with section `s`?

<!-- ======================================================================= -->
## pi: s -> ni

```
r x ... x (n:s) x ...
```

Section `s in S` strictly contains node `n` because it is directly connected
with it. That statement is however a direct result of the `SxN` relation and,
as such, does not state anything new.

<!-- ======================================================================= -->
## pa: nk -> s

```
r x ... x nk x ... x n1 x (n:s) x ...
```

A path `pa` can be defined which connects
the ancestors of node `n` with section `s`.

*  `pa := (nk,...,n,s) in N{+}S`
* `nk contains ... n belongs-to s`

These paths can be inverted:

* `pa' := (s,n,...,nk) in SN{+}`
* `s contains n ... belongs-to nk`

Here, the relations used to create such a path have antonymous semantics
(i.e. `contains` vs. `belongs-to`) and, as such, different orientation.
Such a path is therefore said to be semantically inconsistent.

<!-- ======================================================================= -->
## derived statements

The reason why no clear conclusion can be drawn is, that the ancestors of node
`n` may have any number of nodes that are descendant to the root `r`, but that
are not ancestral (i.e. not in `prefixOf(pa)`) to it. Hence, a path `p` could
be defined which connects some node `o` with section `s`

* `p := (o,...,r,...,nk,...,n,s) in N{+}S`
* `o belongs-to ... r contains ... nk belongs-to s`

Obviously, such a path would be even more inconsistent.

<!-- ======================================================================= -->
## pd: s -> nk

```
r x ... x (n:s) x ... x nk x ...
```

A path `pd` can be defined which connects
section `s` with all descendant nodes of `n`:

* `pd .= (s,n,...,nk) in SN{+}`
* `s contains n contains ... nk`

These paths can be inverted:

* `pd' := (nk,...,n,s) in N{+}S`
* `nk belongs-to ... n belongs-to s`

Here, the relations used to create such a path all have the same orientation
(i.e. superordinate-to-subordinate, or subordinate-to-superordinate). Such a
path is therefore said to be semantically consistent.

Note that, if only one relation would be involved, such a path could be
referred to as a "dipath", a directed path (see basics/graph).

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
(downwards): Section `s` loosely contains descendant `y` of node `x`,
if `s` strictly contains `x`.

* `(s strictly-contains x)` and `(s loosely-contains y)`
* `(s contains x)` and `(s contains y)`

Strictly associating a node is equivalent to associating a whole subtree of
nodes. With the root of that subtree being the strictly associated node.

**CLARIFICATION**
(upwards): Descendant `y` of node `x` loosely belongs to section `s`,
if `x` strictly belongs to `s`.

* `(x strictly-belongs-to s)` and `(y loosely-belongs-to s)`
* `(x belongs-to s)` and `(y belongs-to s)`

A node belongs to any section that strictly contains any of its ancestor nodes.
Each node may therefore loosely belong to any number of sections.

These loose relationships can not be undefined because they will be established
automatically by the structure of the node tree as soon as an ancestor is
strictly associated with a section.

The only method to break up those loose relationships is to change the structure
of the node tree. Obviously, that is not allowed because the purpose of the
associations is ultimately to represent the tree's logical structure as is.
