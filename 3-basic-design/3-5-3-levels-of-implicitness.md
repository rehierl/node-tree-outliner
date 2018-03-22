
<!-- ======================================================================= -->
# Levels of implicitness

```
    NxN + SN => NxS, SxN, SxS
 -------------------------------

 R x ... x N x ... x N x ... x L
 x         x         x         x
 U x ... x S x ... x S x ... x S
```

* right/up -> parent-of
* left/down -> child/element-of

<!-- ======================================================================= -->
## SN{+}

Recall the statements with regards to the descendants of associated nodes.

**CLARIFICATION**
(downwards): Section `s` loosely contains descendant `y` of node `x`,
if `s` strictly contains `x`.

Associating a node is equivalent to associating a whole subtree of nodes.
With the root of that subtree being the strictly associated node.

**CLARIFICATION**
(upwards): Descendant `y` of node `x` loosely belongs to section `s`,
if `x` strictly belongs to `s`.

A node belongs to any section with which any of its ancestors is associated.
Each node may therefore belong to any number of different sections.

<!-- ======================================================================= -->
## S{+}N

The `*.parentSection` object properties (i.e. `Node.*` and `Section.*`)
combined define semantically consistent paths, which point from subordinate
subsequent nodes into the direction of superordinate presequent (sectioning)
nodes:

``` 
u x ... x sk x ... x s x ...
```

* node `n` is associated with section `s`
* section `sk` is an ancestor of `s`
* `u` is the universal section

Those properties allow to define the following paths:

* `p := (n,s,...,sk) in NS{+}`
* `n belongs-to s belongs-to ... sk`

These paths can be inverted:

* `p' := (sk,...,s,n) in S{+}N`
* `sk contains ... s contains n`

**CLARIFICATION**
(upwards): Node `n` loosely belongs to section `t`,
if `t` is an ancestor of `s`, and if `n` strictly belongs to `s`.

* `(n strictly-belongs-to s)` and `(n loosely-belongs-to t)`
* `(n belongs-to s)` and `(n belongs-to t)`

A node belongs to all ancestors of the section with which it is associated.

**CLARIFICATION**
(downwards): Section `t` loosely contains node `n`,
if `s` is a descendant of `t`, and if `s` strictly contains `n`.

* `(s strictly-contains n)` and `(t loosely-contains n)`
* `(s contains n)` and `(t contains n)`

A section contains all the nodes of its descendant sections.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
For each path `p in SN{+}` there exists a path `q in S{+}N`.

Note that ...

* all nodes are organized within a rooted ordered tree of nodes
* each node is associated with a section (the root with the universal section)
* any section is a strict or loose subsection of the universal section.

**CLARIFICATION**
Obviously, these paths are not limited to one section, or one node only.
That is, path combinations are possible: `p in S{+}N{+}`.
