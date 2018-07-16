
<!-- ======================================================================= -->
# Levels of implicitness

```
   NxN + SN => NxS, SxN => SxS
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

**CLARIFICATION (1)**
(downwards): Section `s` loosely contains descendant `y` of node `x`,
if `s` strictly contains `x`.

Associating a node is equivalent to associating a whole subtree of nodes. With
the root of that subtree being the strictly associated node. Consequently, the
relevant section remains to be open until all descendants have been associated.
That is, a section can not be closed inside of an associated subtree.

**CLARIFICATION (2)**
(upwards): Descendant `y` of node `x` loosely belongs to section `s`,
if `x` strictly belongs to `s`.

A node belongs to any section with which any of its ancestors is associated.
Each node may therefore belong to any number of different sections.

Note that the sections to which a node belongs, all are related with each other.
That is because all sections are open (due to 1) when the descendant node has
to associated. Put differently, no section `s1` in the set of sections `S`, to
which a node belongs, is independent to section `s2 in S`, if `(s1 != s2)`.

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

**CLARIFICATION (3)**
(upwards): Node `n` loosely belongs to section `t`,
if `t` is an ancestor of `s`, and if `n` strictly belongs to `s`.

* `(n strictly-belongs-to s)` and `(n loosely-belongs-to t)`
* `(n belongs-to s)` and `(n belongs-to t)`

A node belongs to all ancestors of the section with which it is associated.

**CLARIFICATION (4)**
(downwards): Section `t` loosely contains node `n`,
if `s` is a descendant of `t`, and if `s` strictly contains `n`.

* `(s strictly-contains n)` and `(t loosely-contains n)`
* `(s contains n)` and `(t contains n)`

A section contains all the nodes of its descendant sections.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
For each path `p` in `SN{+}` there exists a path `q` in `S{+}N` (one parent
section), or even multiple such paths (formal associations), such that both
paths begin with the same section and end in the same node.

Note that ...

* paths in `S{+}N` result by design from those in `SN{+}`.
* all nodes are organized within a rooted ordered tree of nodes.
* each node is associated with a section (the root with the universal section).
* any section is a strict or loose subsection of the universal section.

Note that ...

* paths don't necessarily have the same length (e.g. in number of hops):
  `#p,#q in [1,*)`, `((#p < #q) or (#p == #q) or (#p > #q))`. Which is,
  because the length of `p in SN{+}` depends on the node tree, and the
  length of `q in S{+}N` on the section tree.
* more paths may even exist in `S{+}N{+}`.

**CLARIFICATION**
Obviously, a design must support that, all statements which can be made based
on a given path, can also be derived from a different path.

Otherwise, the design can not be understood to be in itself consistent. That is,
because the statements which can then be derived from such paths will contradict
each other. Consequently, such paths allow to point out design errors.

<!-- ======================================================================= -->

**TODO**
proof (by design?) that a path in `SN{+}` exists for each path in `S{+}N` -
and by that, proof that those paths allow to make the same statements -
this would confirm the conclusions drawn from the initially defined
`SN{+}` paths. that is because the corresponding statements can then
also be derived from the `S{+}N` paths -
this would suggest/indicate that the design is in itself consistent -
this would also serve as a formal basis for 2D/3D height maps -

**TODO**
S{+}N -
a node belongs to a section, which belongs to all of its ancestor sections -
the root section contains all its descendant sections, one of which must
contain the initial node (the latter is guaranteed by design to be true) -

**TODO**
the downwards direction contains t1 and t2 sections -
like any other descendant of the root node, all the child nodes of the root
node are strictly or loosely (s/l) associated with the root section -
all the nodes in the downwards path are s/l associated with the root section -
all the nodes in the downwards path are t1 or t2 sectioning nodes (the latter
is not exactly relevant) and may be s/l associated with additional t2 sections,
whose sectioning nodes are not in that path -
if that path has a t2 sectioning node, then that path ends with,
or inside of that sectioning node -

**TODO**
S{+}N -
start with SN, continue with SSN, then SSSN (-> S...SN) -

**TODO**
is there an easier way? -
e.g. via the definition of hierarchy -
e.g. definition of "set" and "subset" -

**TODO**
SN{+} -
a node belongs to a parent node,
which belongs to its ancestor nodes -
the root node contains all its descendant nodes,
one of which has to contain the initial node
