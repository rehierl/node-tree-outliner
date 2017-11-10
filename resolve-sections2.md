
# Sections

* section, a basic definition
* sectioning node
* current section
* Nodes <-> Sections

<!-- ======================================================================= -->
## Section (1)

A section is a sequence of nodes.

This implies that the nodes of a section have some order.

* The order is based upon the notation of an HTML document -
  the tree traversal must respect this order.
* An outliner must assign nodes to sections according to that order.
* synonymous - introduce, initialize, declare
* synonymous - associate with, establish a relationship with
* synonymous - is associated with, is related to

At some point, an element introduces a new section. From that point on,
nodes must be associated with this section, one after another,
until that is no longer allowed.

* `S` is the set of sections, `N` the set of nodes.
* The `SxN` relation is a two-way, one-to-many (1:N) relationship
* A section is empty, if no nodes are associated with it.
* A node is added to the end of a section, or more accurately
  to the end of its sequence, when a node has to be associated with it.
* The n-th node of a section's sequence is the section's n-th node.
* A non-empty section always has a first and a last node.

A section is not a path.

* A section is not necessarily uni-directional.
* `s=(...,ni,ni+1,ni+2,...)` - `ni+1` may be a child of `ni`
  and `ni+2` the next sibling to `ni`.
* A section may consist of siblings only (not parent-of and not child-of).
* The sequence of a section may contain subsequences that are path sequences.
* A section may be equal to a path (an extreme case).

A section is declared by its sectioning node and defined by its node sequence.

* To distinguish sections from one another, the section's sectioning node
  must be taken into account (e.g. empty section).

Definitions

* `Section Node.parentSection`
* `Node[] Section.innerNodes`

### open and closed sections

A section is open, if it is still allowed to associate properties (title, etc.)
and entities (nodes, subsections, etc.) with it.

* synonymous - open, has started
* synonymous - closed, has ended

A section is closed, if no more associations are allowed.

* A closed section is fully qualified/defined.

### associated resources

* synonymous - allocate, lock, create
* synonymous - release, unlock, free, destroy

Similar to binary streams, certain resources (e.g. memory) must be associated
with a section. These need to be allocated when a section is opened and
released when it is closed.

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
* A sectioning node introduces a single section
  (not 0, not 2, ..., not N, exactly and always 1).
* `N` the set of nodes, `S` is the set of sections
* This `NxS` relation is a two-way, one-to-one (1:1) relationship.
* Any section can be identified by its sectioning node.
* Any node can be classified as a sectioning, or as a non-sectioning node
  (a node either introduces a new section, or it does not).

This definition implies an order between a sectioning node and its section:

* A sectioning node is presequent to its section.
* A section is subsequent to its sectioning node.
* A section can not exist without its sectioning node.

This definition implies that some process will have to switch away from a
pre-existing section to the introduced next new section, as soon as the next
sectioning node is reached.

* There is some order on a document's set of sections.
* synonymous - declared before, pre-exists, precedes
* synonymous - next new, declared after, is subsequent to

If there is a presequent section, then there must also be a sectioning node
which precedes it (because that section must also be declared at some point).

* The sectioning node of a presequent section
  is presequent to the sectioning node of a subsequent section.
* The order on the set of sections is
  equivalent to the order of their sectioning nodes.

This definition does not state that a presequent section must end once the next
sectioning node is reached. Such a section may simply be suspended when the
new section begins and it may be resumed once the new section ends.

* synonymous - suspend, pause
* synonymous - resume, continue

The definition of a specific sectioning node must define (1) which effect it has
on presequent sections that are still open, and (2) what kind of relationship
the new section has with these.

Definitions

* `SectioningNode Section.declaredBy`
* `Section SectioningNode.declaredSection`

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

At any given time, multiple sections may be open, but only one of these can
be the current active section. All the other open sections are suspended,
i.e. they may be resumed at some later point in time.

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
* The root node always acts as a sectioning node.

The strict belongs-to relation puts each node into a strict relationship with a
single section: A node either strictly belongs to one section, or it strictly
belongs to a different one.

* A node can not strictly belong to two different sections at the same time.
* A node strictly belongs to (`NxS`) one section and may also
  loosely belong to (`Nx...xNxS`) multiple other sections
  (`Nx...xN in BU` because sections only have a downwards effect).
* `NxS` is functional

Multiple nodes may still strictly belong to the same section.

### sections -> nodes (SxN)

A section strictly contains a node, if that node strictly belongs to it.

* `SxN` is right-total.

Because multiple nodes may strictly belong to the same section, a section
either strictly contains no node at all, a single node, or more than one nodes.

* `SxN` is *not* functional

**TODO** -
A section that itself does not strictly contain any nodes, does not have to be
empty (e.g. a section may consist of a single subsection). That is, a seemingly
empty section (i.e. no strict relationship with any node) may still loosely
contain (`SxNx...xN`) any number of nodes.

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
* A section does not loosely contain any of the node's ancestors.
* Any section has *a downwards*, but *no upwards* effect.
* synonymous - downwards, inwards, inner
* synonymous - upwards, outwards, outer

A node is related to a section, if it is strictly or loosely related to it.

### Section X contains node Y

* synonymous - contains, is associated with, is related to

A section strictly/loosely contains a node,
if the node strictly/loosely belongs to it.

A section contains a node,
if the section strictly or loosely contains the node.
