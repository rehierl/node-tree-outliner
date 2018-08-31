
<!-- ======================================================================= -->
# TODO - node trees

* induced subtree -> induced (sub)path
* overlapping hierarchy => more than one parent

thoughts

* sequences are not required, if ...
* a topological sorting can be defined
* based on the relationships of sets

sub-graph, sub-tree

* the union of subtrees
* (strict) subtree as "induced subtrees"
* i.e. induced by its root node
* properly define "sub-graph", "sub-tree"
* disjoint tree

<!-- ======================================================================= -->
inner/outer sets of a node

* construction of the partial order of a tree
* needs the transitive closure
* for each node take its rooted path
* in that sequence of nodes, connect each node ni with all ni+k
* the set of all ni+k of all rooted paths through ni
* represents the inner set of a node

<!-- ======================================================================= -->
sections

how to answer the h1-div-h1-issue?

* most likely via order theory

if sections would cross borders

* the intersections between the relevant sets
* would not represent complete subtrees
* implementations would have to support partial subtrees
* i.e. treat sections as true sets of nodes
* i.e. nodes that have no particular relationship with each other
* i.e. super increased complexity

if sections would not cross borders

* the intersections between the relevant sets
* represent complete subtrees
* subtrees defined by a single root node
* root nodes that are siblings to each other
* implementations could take advantage of reduced granularity
* i.e. treat sections as a list of siblings

what are sections

* the union of sets of nodes defined by single nodes
* i.e. a node and all of its descendants
* the union of complete subtrees
* i.e. subtrees that are siblings to each other
* i.e. forests of equally ranked subtrees
* a sequence of siblings
* i.e. a sequence of child nodes

sections as groups of subtrees

* sections are forests of equally ranked (aka. consecutive) subtrees
* the hierarchy of sections is a hierarchy of forests
* the hierarchy of sections is a hierarchy of sets of root nodes
* i.e. relevant and non-relevant nodes

granularity of sections

* this essentially increases the granularity of sections
* i.e. small isolated nodes vs. larger units as subtrees of nodes
* i.e. the units of a section are groups of nodes
* sections are less fine grained and more granular
