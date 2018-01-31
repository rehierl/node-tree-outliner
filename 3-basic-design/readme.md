
<!-- ======================================================================= -->
# Overview of the conclusions and definitions

This overview is not meant to be overly accurate: It's just a short summary.

Note that most statements are derived conclusions, or only introduce new names
for particular entities. There are very few definitions that choose one option
out of multiple available options (i.e. not much room for political decisions).

node sequence

* The node sequence (aka. trace of nodes) of a node tree contains all the
  tree's nodes in the corresponding node order.
* The context of a node contains all those nodes that are allowed to have any
  kind of effect on the corresponding node.
* All nodes in the context of a node are presequent to the corresponding node.
  In other words, a node is subsequent to all nodes within its context.
* The words "presequent" (backwards) and "subsequent" (forwards) reflect an
  important switch in perspective.
* A section can initially be defined as a set of nodes.
* The formal approach requires that any node of a tree will be associated with
  one or more sections. In the end, and for practical reasons, any node will be
  associated with one section only.
* The scope of a section is the range of nodes that are associated with it.
* Any sectioning node always declares a single new section. That is, there is a
  1:1 relationship between the set of sectioning nodes and the set of sections.
* The sectioning nodes of a tree are the tree's active nodes. All other nodes
  are said to be the tree's inactive or passive nodes (i.e. they have no effect
  one the outline of a tree).
* The outline of a tree is the structure that holds all sections. Not to
  be misunderstood with a hierarchical listing of section properties (e.g.
  table of contents).

section states

* Any section has three states: initialized, open and closed.
* Any node, sectioning nodes included, that is subsequent to a section's open,
  and presequent to its close event is said to be one of the section's content
  nodes.
* All nodes, no exceptions, must be associated with their sections while they
  are being entered.
* A section is a subsequence of the tree's node sequence.

sectioning nodes

* There are two types of sectioning nodes that can be defined without any
  structural requirement: type-1 (e.g. `<section>`) and type-2 (e.g. `<h1>`).
* The scope of a type-1 section begins with its first child and the scope of a
  type-2 section with its next sibling.
* Sectioning nodes must define where a section begins (open event) and where
  the declared section ends (close event).
* The definition of a type-2 sectioning node must be strict:
  A type-2 section is empty, if there is no next sibling.
* A tree's root node always acts as a type-1 sectioning node.

sequence of siblings

* Associating a node (strict association) with a section is equivalent to
  associating a whole subtree of nodes (implicit associations).
* A section can not end inside of an associated container node. All descendants
  of an associated container are automatically implicitly associated.
* A node that is supposed to be associated with a section, but is not yet
  implicitly associated, must be strictly associated. These nodes are the
  top-level nodes of a section.
* The complete node sequence of a section (subsequence of the tree's node
  sequence) can be derived from a section's reduced node sequence (top-level
  nodes only).
* Mind hook: A section is a sequence of siblings (i.e. the top-level nodes).
* The very first node of a section, always a top-level node, is critical to
  transformations: Associate all nodes while entering is a must.

last nodes

* The default scope of a section is the widest range of nodes possible
  that does not result in any conflict.
* The default scope of any section must end with the section's parent container.
* The parent container of a type-1 section is its sectioning node.
* The parent container of a type-2 section is the parent of its sectioning node.
* The default scopes of multiple sections may end with the same parent container.
* A parent container does not belong to those sections whose default scopes it
  has to end.

subsection

* An inner section (or subsection) is a subsequence of all of its ancestor
  sections. By default, a subsequent section is a subsection of all open
  presequent sections.
* Any sectioning node always declares a new subsection
  (i.e. not some isolated entity).
* By default, any sectioning node defines a rooted ordered tree of sections.
* The `SxN` and `SxS` relations don't have to be defined explicitly.
* Each node can be associated with one section only (i.e. the parent section
  of a node) => one reference per node.
* Any node must be associated with the closest open presequent section.
* In order to re-create the complete node sequence of a section the nodes
  of a section and all the nodes of its inner sections must be concatenated
  in the corresponding node order.

associating sectioning nodes

* Any sectioning node must be associated with the parent section
  of the section it declares: There are multiple reasons for that.
* The very first node of any section always is strictly associated
  with it => critical to transformations.

**... to be continued ...**
