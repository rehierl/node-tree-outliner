
<!-- ======================================================================= -->
# Types of trees

subgraph

* subgraph - subsets of vertices and subset of edges
* spanning subgraph - same vertices, fewer edges
* induced subgraph - vertex subset and all edges in that subset

subtree

* subtree - a connected subgraph of a tree
* subtree of a rooted tree - all edges and vertices descendant to a vertex

<!-- ======================================================================= -->
## wikipedia, recursive tree

* an unordered, non-planar labeled rooted tree
* nodes are labeled using integers in `[1,n]`
* labels increase with distance from the root
* non-planar - children have no order

<!-- ======================================================================= -->
## wikipedia, trémaux/normal tree

* aka. normal spanning tree
* a spanning tree of an undirected graph rooted at one vertex
* two vertices are adjacent as ancestor and descendant
* all depth-first search trees are trémaux trees

comments

* not quite clear what the specific characteristics really are
* "ancestor and descendant" ...

<!-- ======================================================================= -->
## wikipedia, spanning tree

* a subgraph of an undirected graph that is a tree
* the tree includes all vertices with minimum number of edges
* a graph may have several spanning trees
* a graph may have only one spanning tree - the graph is itself a tree
* a graph must be connected

comments

* somewhat related to hamilton paths
* note that graphs in general do not have to be directed
* directedness in graph theory is more a special case, not the default
