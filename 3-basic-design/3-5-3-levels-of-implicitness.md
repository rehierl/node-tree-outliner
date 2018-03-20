
<!-- ======================================================================= -->
# Levels of implicitness

```
    NxN + SN => NxS, SxN, SxS
 -------------------------------

 R x ... x N x ... x N x ... x L
 x         x         x
 U x ... x S x ... x S x ... x S
```

* right/up -> parent-of
* left/down -> child/element-of

<!-- ======================================================================= -->
## SN{+}

Recall the statements with regards to the descendants of an associated node.

**CLARIFICATION**
(downwards): Section `s` loosely contains descendant `y` of node `x`,
if `s` strictly contains `x`.

Strictly associating a node is equivalent to associating a whole subtree of
nodes. With the root of that subtree being the strictly associated node.

**CLARIFICATION**
(upwards): Descendant `y` of node `x` loosely belongs to section `s`,
if `x` strictly belongs to `s`.

A node belongs to any section that strictly contains any of its ancestor nodes.
Each node may therefore loosely belong to any number of sections.

<!-- ======================================================================= -->
## S{+}N

Both `*.parentSection` object properties (i.e. `Node.*` and `Section.*`) can
be combined in order to define semantically consistent paths, which point from
subordinate subsequent nodes into the direction of superordinate presequent
(sectioning) nodes:

```
u x ... x sk x ... x s x ...
```

* node `n` is associated with section `s`
* section `sk` is an ancestor of `s`
* `u` is the universal section

The above object properties allow to define the following paths:

* `p := (n,s,...,sk) in NS{+}`
* `n belongs-to s belongs-to ... sk`

These paths can be inverted:

* `p' := (sk,...,s,n) in S{+}N`
* `sk contains ... s contains n`

**CLARIFICATION**
(upwards): Node `n` loosely belongs to ancestor `t` of section `s`,
if node `n` strictly belongs to section `s`.

* `(n strictly-belongs-to s)` and `(n loosely-belongs-to t)`
* `(n belongs-to s)` and `(n belongs-to t)`

A node belongs to all ancestors of the section with which it is associated.

**CLARIFICATION**
(downwards): Section `s` loosely contains node `n` in section `s`,
if `s` is a descendant of `t`, and if `n` strictly belongs to `s`.

* `(s strictly-contains n)` and `(t loosely-contains n)`
* `(s contains n)` and `(t contains n)`

A section contains all the nodes of its descendant sections.

<!-- ======================================================================= -->
## derived statements

Obviously, these paths are not limited to one section, or one node only.
That is, path combinations combinations are possible: `p in S{+}N{+}`.

<!-- ======================================================================= -->

**TODO**
proof that a path in `SN{+}` exists for each path in `S{+}N` -
this proof would then confirm the conclusions drawn from the initially
defined `SN{+}` paths. that is, because the corresponding statements can
then also be derived from the `S{+}N` paths -
it would also strongly indicate that the design is in itself consistent -
