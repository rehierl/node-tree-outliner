
<!-- ======================================================================= -->
# TODO - node trees

* define connected component
* define union/intersection/diff for graphs/trees
* see - operations on sets
* vertex/node/edge disjoint graphs/trees
* vertex/node-disjoint -> edge-disjoint
* define the leaf-set of a node/tree

directed tree

* ordered pair of nodes -> tree order
* the tree order of a tree is built upon the node order in each edge

<!-- ======================================================================= -->
## paths -> subtree

* a path is a graph and a tree
* i.e. induced subtree -> induced subpath
* a tree is a hierarchy of sets -> a path is a hierarchy of sets
* e.g. start with rooted paths

rethink that thought - from (induced) paths

* similarities with the removal-based definition of "subsequence"
* removal of vertices and edges from the transitive closure of a sequence
* i.e. not just from its cover relation
* any subsequence can be considered an "induced subsequence".

<!-- ======================================================================= -->
## path -> sequence

* a path is a sequence
* a (ordered) sequence is a hierarchy of sets
* i.e. sets that all are strictly related (~ 1st dimension)
* i.e. a tree adds disjoint subsets (~ 2nd dimension)

<!-- ======================================================================= -->
## traversal -> sequence

* the tree traversal defines a sequence
* a rooted path is somewhat perpendicular to the node sequence

traversal vs. node tree

* are sequences required, if the traversal is consistent with the tree?
* i.e. a node sequence must fit into the hierarchy of sets
* i.e. the traversal is defined base on the relationships of the sets

traversal vs. set hierarchy

* how does the hierarchy of sets of an ordered sequence
* blend into the hierarchy of sets of an ordered tree?

<!-- ======================================================================= -->
## sections

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
