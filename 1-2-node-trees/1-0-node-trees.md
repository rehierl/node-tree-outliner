
<!-- ======================================================================= -->
# Tree of nodes

* represents the hierarchical nature of a structure

<!-- ======================================================================= -->
## tree/hierarchy structure

* nodes- the vertices of the tree's graph
* branches - the edges of the tree's graph
* leaf/end nodes - nodes without children
* root/starting node - has no superior
* parent node - closest superior on the rooted path
* siblings - share the same parent node
* uncles - siblings of the parent
* ancestor - connected to all lower-level nodes
* descendant - the connected lower-level nodes

visualized as

* classical node-link diagrams
* nested sets - use enclosure/containment to show parenthood (!!!)
* layered "icicle" diagrams - stacked rectangles
* outlines, tree views - lists that use indentation
* nested parenthesis

notes

* each finite tree has a root
* an infinite tree may have a root

<!-- ======================================================================= -->
## tree, set theory

<!-- ======================================================================= -->
## tree, graph theory

* an undirected graph
* any two vertices are connected by exactly one path
* a tree <-> an acyclic connected graph
* a tree - may have more than one root
* a forest - a disjoint union of trees
* a forest - an acyclic graph, not necessarily connected
* rooted tree - has one root only
* directed tree - only has directed edges
* directed rooted tree - a directed tree that has one root only
* arborescence, branching, out-tree - all edges point away from the root
* anti-arborescence, in-tree - all edges point towards the root

tree if one of these equivalent conditions hold

* connected, no cycles
* acyclic, a cycle is formed if any edge is added
* connected, but disconnected, if a single edge is removed
* any two vertices can be connected by a unique simple path
* connected, (#V-1) edges
* no simple cycles and (#V-1) edges

and some more definitions

* internal/inner/branch vertex - `(degree(v) >= 2)`
* external/outer/terminal vertex - `(degree(v) == 1)`
* leaf - a terminal vertex
* forest - connected components are trees
* forest - a disjoint union of trees
* forest - an undirected acyclic graph
* discrete graph - vertices only, no edges
* polytree - a DAG whose undirected graph is a tree

rooted tree

* one vertex is designated as "the root"
* edges are either oriented away from the root ex-or towards the root
* free tree - has no designated root
* labeled tree - each vertex has a unique label (e.g. an id number)
* recursive tree - labeled rooted tree where labels respect the tree order
* parent of v - `p` in the rooted path `rp := [r,..,p,v]`
* except for the root, every vertex has a unique parent
* child of v - `c` in the rooted path `rp := [r,..,v,c]`
* descendant of v - `d` in the rooted path `rp := [r,..,v,..,d]`
* a child is a descendant to its parent
* ancestor of v - `a` in the rooted path `rp := [r,..,a,..,v]`
* the root is an ancestor to any other vertex
* sibling vertices have the same parent
* root is external, if it has one child
* note - the degree-based definition of "external"
* height of a vertex - length of the longest downward path `p := [v,..,l]`
* height of the tree - is the height of its root
* height of a leaf - is zero
* depth of a vertex - length of its rooted path `p := [r,..,v]`
* depth of the root - is zero

**tree-order**

* the partial ordering on the vertices
* `(v < w)` if there is a rooted path such that `[r,..,v,..,w]`

**ordered/plane tree**

* a rooted tree that has an ordering for its child vertices
* an ordering of children is equivalent to embedding the tree in the plane

<!-- ======================================================================= -->
## tree, data structure

<!-- ======================================================================= -->
## subgraph, subtree

subgraph

* subgraph - subsets of vertices and subset of edges
* spanning subgraph - same vertices, fewer edges
* induced subgraph - vertex subset and all edges in that subset

subtree

* subtree - a connected subgraph of a tree
* subtree of a rooted tree - all edges and vertices descendant to a vertex

<!-- ======================================================================= -->
## Recursive tree

* an unordered, non-planar labeled rooted tree
* nodes are labeled using integers in `[1,n]`
* labels increase with distance from the root
* non-planar - children have no order

<!-- ======================================================================= -->
## Normal/Trémaux tree

<!-- ======================================================================= -->
## Spanning tree
