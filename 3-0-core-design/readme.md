
This content holds the core design (i.e. default definitions) of the general
purpose outliner. As such, it does not define any rank-related values (i.e.
a rank-less design).

Note that most statements in that chapter are derived conclusions, or only
introduce new names which are used to refer to specific entities/circumstances.
There are very few definitions that choose one option out of multiple available
options (i.e. not much room for political decisions or personal preferences).

<!-- ======================================================================= -->
# an overview

**TODO**
begs to be updated ...

This overview is not meant to be overly accurate: It's just a "short" summary.

node sequence

* The node sequence (aka. trace of nodes) of a node tree contains all the
  nodes in the tree's order of nodes.
* The context of the current node contains all those nodes that are allowed to
  have any kind of effect on it.
* All nodes in the context of a node are presequent to the corresponding node.
  In other words, a node is subsequent to all the nodes in its context.
* The words "presequent" (backwards) and "subsequent" (forwards) reflect an
  important switch in perspective.
* A section can initially be defined as a set of nodes.
* The formal approach requires that any node of a tree is associated with one
  or more (open) sections. In the end, and for practical reasons, any node will
  be associated with one (open) section only.
* The scope of a section is the range of nodes that are associated with it.
* Any sectioning node always declares a single new section. That is, there is a
  1:1 relationship between the set of sectioning nodes and the set of sections.
* The sectioning nodes of a tree are the tree's active nodes. All other nodes
  are said to be the tree's inactive or passive nodes (i.e. they have no effect
  whatsoever one the outline of a tree).
* In general, and with the exception of parent containers (see "last nodes"),
  any inactive node can be ignored.
* The outline of a tree is the structure that holds all sections. Not to
  be misunderstood with a hierarchical listing of section properties (e.g.
  table of contents).

section states

* Any section has three states: initialized, open and closed.
* Any node, sectioning nodes included, that is subsequent to a section's open,
  and presequent to its close event is said to be a content node of the
  corresponding section.
* All nodes, no exceptions, must be associated while they are being entered.
* Any node can be subsequent to multiple open sections.
* A section, even an empty one, always is a subsequence of the tree's node
  sequence.

sectioning nodes

* There are two types of sectioning nodes that can be defined without any
  structural requirement: type-1 (e.g. `<section>`) and type-2 (e.g. `<h1>`)
  sectioning nodes.
* The scope of a type-1 section begins with its first child and the scope of
  a type-2 section with its next sibling.
* Sectioning nodes must define where a section begins (in terms of an open
  event) and where the declared section has to end by default (close event).
* The definition of a type-2 sectioning node must be strict:
  A type-2 section is empty, if there is no next sibling.
* A tree's root node must always be treated as a type-1 sectioning node.

sequence of siblings

* Associating a node (strict association) with a section is equivalent to
  associating a whole subtree of nodes (implicit associations).
* A section can not end inside of an associated container node. All descendants
  of an associated container are automatically implicitly associated.
* A node that is supposed to be associated with a section, but is not yet
  implicitly associated, must be strictly associated. These nodes are the
  top-level nodes of a section.
* With regards to a specific section, a top-level node has no strictly or
  implicitly associated ancestor node; hence the name.
* The complete node sequence of a section (i.e. a subsequence of the tree's
  node sequence) can be derived from a section's reduced node sequence (i.e.
  a sequence of top-level nodes).
* Mind hook: A section is a sequence of siblings (i.e. its top-level nodes).
* The very first node of a section, which always is a top-level node, is
  critical to transformations.
* Associating all nodes while entering them is a must
  (i.e. not open for debate).

last nodes

* The default scope of a section is the widest range of nodes possible that does
  not result in any conflict.
* The default scope of any section must end with the section's parent container.
* The parent container of a type-1 section is the corresponding sectioning node.
* The parent container of a type-2 section is the parent node of its sectioning
  node.
* The default scopes of multiple sections may end with the same parent container.
* A parent container does not belong to any section whose default scope it has
  to end.

subsection

* An inner section (or subsection) is a subsequence of all of its ancestor
  sections.
* By default, a subsequent section is a subsection to all open presequent
  sections.
* Any sectioning node always declares a new sub-section
  (i.e. not some isolated entity).
* By default, any sectioning node defines a rooted ordered tree of sections.
* The `SxN` relation (i.e. section-contains-node) and the `SxS` relation (i.e.
  section-contains-subsection) don't have to be defined explicitly.
  These result from the definition of sectioning nodes.
* Each node can be associated with one section only (i.e. the parent section
  of a node): multiple references => one reference per node (i.e. formal vs.
  practical perspective).
* A node's parent section is the closest open presequent section.
* In order to re-create the complete node sequence of a section, the nodes
  of a section and all the nodes of its inner sections must be concatenated
  in the corresponding node order.

associating sectioning nodes

* Any sectioning node, no exception, must be associated with the parent
  section of the section it declares: There are multiple aspects involved.
* The very first node of any section always is strictly associated with it,
  which is critical to transformations.
