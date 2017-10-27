
# Basic aspects

```
Example:
========
<body>
  A
  <h1>B</h1>
  C
</body>
```

* Any node always belongs to some section.

Node `A` belongs to the section introduced by the body element (i.e.
**the body section**). The body section contains node `A`.

* The last section introduced before node `C` is section `B`.
  No other section is introduced before node `C`.
  If that were the case, node `C` would have to belong to this section instead.
* There is no indication that section `B` ends before node `C`.
  If that were the case, node `C` would have to belong to a pre-existing section
  (e.g. the body section).

Node `C` belongs to section `B`.

**TODO** -
Does a heading element and its inner nodes (e.g. `h1` and `B`) belong to the
section that a sectioning element (heading) introduces, or to a section
to which it is subsequent (i.e. to some previous section)?

<!-- ======================================================================= -->
## Node <-> Nodes

* Think in terms of tuples.

The DOM tree is a tree data structure defined in terms of nodes and edges,
i.e. we are bound by the rules of discrete mathematics (graph theory)!

* `n in N` is a node, `N` is the set of all nodes.
* A node may be a root - `r in R subset-of N`
* A node may be a parent - `p in P subset-of N`
* A node may be a child - `c in C subset-of N`
* A node may be a leaf - `l in L subset-of N`
* Edge `e := (p,c) in E subset-of PxC subset-of NxN`
* Each parent is connected with all of its child nodes.
* `E` only contains existing edges.

*In general*

* `P`, `C`, `L` and `R` are all not equal to `N`
* A parent is no leaf. A leaf is no parent.
* `P = N - L` => `n in P <=> n not in L` => `n in L <=> n not in P`
* A child can be a parent or a leaf.
* `CxC subset-of PxC` eq. `PxC contains CxC`
* `PxL subset-of PxC` eq. `PxC contains PxL`
* A root has no parent. A root is no leaf.

*A rooted, ordered tree*

* There must be a single root - `r in (R = {r}) subset-of P`
* The child nodes of a node have some order (left-to-right, first-to-last)

*Path tuples*

For any path `p=(n1,n2,...,nk) in NxNx...xN` such that `ni parent-of ni+1`,
`i in [1,k-1]` and `k in [2,+Inf)` (i.e. top-down, `(ni,ni+1) in E`),
`ni` is an ancestor of `ni+1` and `ni+1` a descendant of `ni`.
(special case - `RxNx...xNxL`, root-to-leaf)

* `TD` represents the set of all top-down paths
* `RD` all paths that begin in a root (`ni in R`)
* `TL` all paths that end in a leaf (`nk in L`)
* `RL` all paths that begin in a root and end in a leaf
* `E in TD`

For any path `p=(n1,n2,...,nk) in NxNx...xN` such that `ni child-of ni+1`
`i in [1,k-1]` and `k in [2,+Inf)` (i.e. bottom-up, `(ni+1,ni) in E`),
`ni` is a descendant of `ni+1` and `ni+1` an ancestor of `ni`.
(special case - `LxNx...xNxR`, leaf-to-root)

* `BU` represents the set of all bottom-up paths
* `BR` all paths that end in a root (`nk in R`)
* `LU` all paths that begin in a leaf (`ni in L`)
* `LR` all paths that being in a leaf and end in a root
* `E not in BU`

*A tree has no cycles*

* The length of a path `p` is the number of nodes involved (`p.len = k`).
* The n-th node of a path is the n-th node in its node sequence.
* `p(i) = ni` for `p=(...,ni-1,ni,ni+1,...)`
* no cycles => `p(i) != p(j)` for any `i,j in [1,k]` and `i != j`

*related to*

* `n1` is strictly related to `nk`, if `p=(n1,nk) in TD or BU`
* synonymous - strictly related to,
  directly related, strictly connected with, in strict relationship with
* `n1` is loosely related to `nk`, if `p=(n1,n2,...,nk) in TD or BU`
* synonymous - loosely related to,
  loosely connected with, in loose relationship with
* `n1` is related to `n2`, if `n1` is strictly or loosely related to `n2`.
* synonymous - related to, connected with, in relationship with
* i.e. (strictly => no nodes in between), (loosely => nodes in between)

*What this should sum up to is this*

* A parent is strictly related to its children.
* A parent is loosely related to its descendants (minus children).
* A parent is related to all of its descendants.

and

* A child is strictly related to its parent.
* A child is loosely related to its ancestors (minus parent).
* A child is related to all of its ancestors.

<!-- ======================================================================= -->
## An inaccurate mantra (1)

* Just a pictogram to guide ones thoughts.
* Yuo cna sitll raed tihs!

```
< root <          path-of-nodes        > leaf >
< parent-of <                      > child-of >

R x N x ... x N x N x ... x N x N x ... x N x L
```

* At any non-leaf node, a path of any length may branch off:

```
            ... x N x N x L
R x N x ... x N x N x ... x N x L
        ... x N x N x N x L
  ... x N x N x N x N x L
```

* `... x N x N x ...` represents an infinite set of paths that share some common
  prefix, but (beginning with some node) branch off into different suffixes.
* `R x N x ... x N x L` represents all the paths of a rooted node tree.

<!-- ======================================================================= -->
## Section (1)

A section is a sequence of nodes.

This implies that the nodes of a section have some order.

* This order is based upon the traversal of the node tree.
* synonymous - introduce, initialize, declare
* synonymous - associate with, establish a relationship with
* synonymous - is associated with, is related to

At some point, an element introduces a new section. From that point on,
nodes will be associated with this section, one after another, until that
is no longer allowed.

* `S` is the set of sections, `N` the set of nodes.
* The `SxN` relation is a two-way, one-to-many (1:N) relationship
* A section is empty, if no nodes are associated with it.
* A node is added to the end of a section, or more accurately
  to the end of its sequence, when a node has to be associated with it.
* The n-th node of a section's sequence is the section's n-th node.
* A non-empty section always has a first and a last node.

A section is
declared by its sectioning node and
defined by its node sequence.

* To distinguish sections from one another, the section's
  sectioning node must be taken into account (e.g. empty section).

Definitions

* `Section Node.parentSection`
* `Node[] Section.innerNodes`

### open and closed sections

* synonymous - open, has started

A section is open, if it is still allowed to associate entities
(nodes, a title, subsections, etc.) with it.

* synonymous - closed, has ended

A section is closed, if no more associations are allowed.

* From that point on, a section is fully defined/qualified
  by the sectioning node and the section's nodes.

### associated resources

* synonymous - allocate, lock, create
* synonymous - release, unlock, free, destroy

Similar to binary streams, certain resources (e.g. memory) must be associated
with a section. These need to be allocated when a section is opened and released
when it is closed.

* Once a section is closed, it can not be re-opened.

Once introduced, a new section object is automatically opened for associations.
As this step will allocate resources, there needs to be a point for each section
at which the resources of a section can be released.

Ultimately, that point is reached for any section when the starting element
(e.g. the body element) has been processed. But, at that point, certain sections
might no longer be accessible. In such a case, resources allocated for sections
that are no longer accessible will remain locked (e.g. memory leaks).

**TODO** -
it must be possible to produce a table-of-contents on the fly (search engines) -
a TOC is just a hierarchical listing of section properties (titles)

<!-- ======================================================================= -->
## Sectioning node (1)

A sectioning node introduces a new section.

* synonymous - sectioning node, sectioning element (HTML speech)
* synonymous - introduce, initialize, declare
* Any node can be classified as a sectioning, or as a non-sectioning node:
  A node either introduces a new section, or it does not.
* A sectioning node introduces a single section
  (not 0, not 2, ..., not N, exactly and always 1).

This definition implies that no section can exist without
first being introduced by some sectioning node.

* `S` is the set of sections, `N` the set of nodes.
* This `NxS` relation is a two-way, one-to-one (1:1) relationship.
* Any section can be identified by its sectioning node.

Definitions

* `SectioningNode Section.declaredBy`
* `Section SectioningNode.declaredSection`

This definition also implies an order between a sectioning node and its section:

* A section can not exist without its sectioning node.
* A sectioning node precedes its section.
* A section is subsequent to its sectioning node.

This definition also implies that some process will have to switch away from
a pre-existing section to the introduced next new section, as soon as the next
sectioning node is reached (i.e. there is some order on a document's set of
sections).

* synonymous - declared before, pre-exists, precedes
* synonymous - next new, declared after, is subsequent to

If there is a preceding section, then there must also be a sectioning node
which precedes it (because that section must also be declared at some point).

* The sectioning node of a preceding section
  precedes the sectioning node of a subsequent section.
* The order on the set of sections is
  equivalent to the order of their sectioning nodes.

This definition does not state that a preceding section must end once the next
sectioning node is reached. Such a section may simply be suspended when the
new section begins and it may be resumed once the new section ends.

* synonymous - suspend, pause
* synonymous - resume, continue

The definition of a specific sectioning node must define (1) which effect it has
on pre-existing sections, and (2) what kind of relationship the new section has
with these.

=> see also - a sequence of nodes subsequent to a node

<!-- ======================================================================= -->
## Current section (1)

Once a section is declared, it automatically becomes the current section. It
remains to be the current section for as long as (1) it did not end, and (2)
no new section was introduced by some other subsequent sectioning node.

* synonymous - current, active, current active

Any subsequent node must always be associated with the current active section,
i.e. determining to which section a node belongs, must always take multiple
aspects into account:

1. Was a new section introduced? =>
   The next subsequent node belongs to the new section, if that is the case.
2. Did the current section end? =>
   The next subsequent node belongs to this section, if that is *not* the case.
3. If the current section, or even multiple previous open sections have ended,
   which of these is the next current section?

At any given time, multiple sections may be open, but only one of these can be
the current active section. All the other open sections are suspended, i.e.
they may be associated with further entities at some later point in time.

* synonymous - inactive, suspended
* Sections that are inactive are still open for associations.

<!-- ======================================================================= -->
## Nodes <-> Sections

Nodes are strictly associated with sections (`NxS`). Once a node is associated
with a section, the section is automatically strictly associated with it (`SxN`).

* Any node can only be strictly associated with a single section.
* More than one node can be strictly associated with the same section.
* The relation `SxN` is a two-way, one-to-many (1:N) relationship.

### nodes -> sections (NxS)

Any node within a tree always strictly belongs to some section.

* `NxS` is left-total.
* The root node always has to be seen as being a sectioning node.

The strict belongs-to relation puts each node into a strict relationship with a
single section: A node either strictly belongs to one section, or it strictly
belongs to a different one (i.e. a node can not strictly belong to two different
sections at the same time).

* A node may however strictly belong to one section and
  loosely belong to multiple other sections at the same time.
* `NxS` is functional

Multiple nodes may still strictly belong to the same section.

### sections -> nodes (SxN)

A section strictly contains a node, if that node strictly belongs to it.

* `SxN` is right-total.

Because multiple nodes may strictly belong to the same section, a section either
strictly contains no node at all, a single node, or more than one nodes.

* `SxN` is *not* functional

A section that itself does not strictly contain any nodes, does not have to be
empty (e.g. a section may consist of subsections only). That is, a seemingly
empty section (i.e. no strict relationship with any node) may still loosely
contain an infinite number of nodes.

<!-- ======================================================================= -->
## Node X belongs to section Y

* synonymous - belongs to, is located inside, is associated with, is related to

A node strictly belongs to a section, if the node is strictly associated with it.

* This definition relies upon a direct relationship between a node and its
  section - i.e. there is some `(n,s) in NxS` such that ...

A node `n` loosely belongs to a section `s`, if there is a path `p=(n,n1,...,nk)`
such that `n descendant-of nk` and `(nk,s) in NxS`.

* Associating a node with a section automatically establishes a loose
  relationship between the section and any of the node's descendants.
* However, the same does not apply to any of the node's ancestors.
* Any section has a *downwards*, but no *upwards* effect.
* synonymous - downwards, inwards, inner
* synonymous - upwards, outwards, outer

A node is related to a section, if it is strictly or loosely related to it.

### Section X contains node Y

* synonymous - contains, is associated with, is related to

A section strictly/loosely contains a node,
if the node strictly/loosely belongs to it.

A section contains a node,
if the section strictly or loosely contains the node.

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

<!-- ======================================================================= -->
## Section (2) - TODO

* `SxS` relation

<!-- ======================================================================= -->
## Sectioning node (2) - TODO

* Does a sectioning element belong to the section it introduces?
* The section of a sectioning element begins inside, or just behind of it.
* A section is subsequent to its sectioning element.

<!-- ======================================================================= -->
## Current section (2), Stack of open sections - TODO

Stack of open sections - the current section is the section at the top of this
stack - not some random section, a specific order -
path in the tree of sections (starts at the root, ends at the current section)

<!-- ======================================================================= -->
## Inner nodes, outer nodes

All inner nodes are descendant to a given node.

* synonymous - descendant nodes, inner nodes

The outer nodes of a node are the nodes that remain of a node tree once (1) the
node itself is and (2) all its inner nodes are removed.

* `outer-nodes := (all-nodes - element - inner-nodes)`
* => *not* synonymous - ancestors, outer nodes
* `#(x) := number-of-set(X)`
* `#(ancestors) <= #(outer-nodes)`

**TODO** -
N-th outer node?

<!-- ======================================================================= -->
## Heading element (1)

A heading element is a sectioning element.

A heading element is parent to all of its child nodes. The inner nodes of a
heading element define the title for the heading's section.

**TODO** -
effect/relationship on/with other sections -
A heading's section begins just after the heading element -
excludes: belongs itself to it section

<!-- ======================================================================= -->
## Parent container X of section Y

Except for the body element,
any node of a document has a parent element.

* Any parent element is a container element.
* Based on the NxN binary relation of a tree data structure.

The parent element of element `X` is the parent container of section `Y`,
if element `X` introduces section `Y` as an outer section.

* The parent container of a section introduced by a heading element is
  the heading's parent element.

If element `X` introduces section `Y` as an inner section, then element `X` is
itself the parent container of section `Y`.

* The parent container of the section introduced by the body element is
  the body element.

This definition is based upon an element's characteristic to
introduce a new section:

* A sectioning element and the section's parent container element are not
  necessarily identical (i.e. these can be different elements).
* A section always begins inside of its parent container.
* This definition is independent of where exactly a section ends.

<!-- ======================================================================= -->
## Relationship between sections

### subsequent

### inner -> outer

### outer -> inner

### formal definitions

Relations that need to be defined using scientific methods:
SxS (parent-of/child-of), `S` is the set of sections

**TODO** -
formalize this
