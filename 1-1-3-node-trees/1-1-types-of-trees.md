
<!-- ======================================================================= -->
# Types of trees

subgraph

* subgraph - subsets of vertices and subset of edges
* spanning subgraph - same vertices, fewer edges
* induced subgraph - subset of vertices and all edges in that subset

subtree

* subtree - a connected subgraph of a tree
* subtree of a rooted tree - all edges and vertices descendant to a vertex

<!-- ======================================================================= -->
## wikipedia, spanning tree

* a subgraph of an undirected graph that is a tree
* the tree includes all vertices with a minimum number of edges
* for a given graph, several spanning trees may exist
* a graph may have only one spanning tree - the graph is itself a tree
* a graph must be connected

comments

* somewhat related to hamilton paths
* note that graphs in general do not have to be directed
* directedness in graph theory is more a special case, not the default

<!-- ======================================================================= -->
## wikipedia, trémaux/normal tree

* aka. normal spanning tree
* the spanning tree of an undirected graph, rooted at one vertex
* two vertices are adjacent as ancestor and descendant
* all depth-first search trees are trémaux trees

comments

* not quite clear what the specific characteristics really are
* "ancestor and descendant" ...

<!-- ======================================================================= -->
## wikipedia, recursive tree

* an unordered, non-planar labeled rooted tree
* nodes are labeled using integers in `[1,n]`
* labels increase with distance to the root
* non-planar - children have no order

<!-- ======================================================================= -->
## wikipedia, radial tree

(more a method of visualization)

* the tree's root in the center
* all other nodes on circles/orbits around the root
* 1st level on the 1st outer circle/orbit
* next level on the next outer circle/orbit
* i.e. the orbit of a node corresponds with its node level
