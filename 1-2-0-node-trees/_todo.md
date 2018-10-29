
<!-- ======================================================================= -->
# TODO - node trees

removal of a node in a tree
!= removal of an object in an ordered set

one characteristic element per set -
i.e. one additional element per descendant

a hierarchy of trees -
i.e. a tree of subtrees

is there any other way to form a class of sets -
such that each set represents the corresponding node -
i.e. the relationship of each set represents the relationship of each node

the start/end tags don't represent the visit of a node -
a node is being visited beginning with its start tag
and until its end tag - i.e. throughout the entire time

tags are like nested parenthesis/intervals

restriction (relations) vs. induced subgraph

define endpoints of a path -
i.e. the start and end vertices

build upon series-parallel graphs/posets

set difference defined as relative complement
i.e. define graph difference as relative complement

any consistent path in a tree is itself a tree

inner/outer set vs. inner/outer nodes

induced subgraphs -
maintain the relationships between the vertices

Note that there is no freedom as to how the set of edges of the resulting graph
is formed. That is, the set of edges is a consequence of the set of vertices in
the resulting graph.

note - graphs are in general "reduced" to subsets of vertices and the implicit
inclusion of all incident edges - i.e. a general pattern - i.e. edges are in
general ignored - i.e. the focus is on sets of vertices

* define a term equivalent to "siblings"? - i.e. snk(v)
* define a term equivalent to "parent"? - i.e. src(v)
* define sets of connected src/snk vertices
* define union (operation) on graphs
* e.g. a disjoint union of maximal components
* induced path
* path graph - aka. linear graph - the whole graph resembles a path
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
