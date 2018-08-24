
<!-- ======================================================================= -->
# Tree of nodes

* a tree represents the hierarchical nature of a structure
* trees may be visualized as "nested sets"
* the definition of parent/leaf should be child-based, not degree-based
* a degree-based definition is problematic with regards to the tree's root
* a tree should not be allowed to be empty - adds complexity to definitions
* a forest (may be empty) is a union of disjoint trees
* tree-order := descendants are subsequent to ancestors
* ordered tree, child-order := each node has an ordered set of child nodes

<!-- ======================================================================= -->
## wikipedia, tree structure

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
* layered "icicle" diagrams - i.e. stacked rectangles
* outlines, tree views - i.e. indentation-based listing
* nested parenthesis

notes

* each finite tree has a root
* an infinite tree may have a root

<!-- ======================================================================= -->
## wikipedia, tree (set theory)

* tree - a partially ordered set `(T,<)`
* such that - `{ s in T | (s < t) for each (t in T) }` is well-ordered
* frequently only one root - minimal element
* each well-ordered set `(T,<)` is a tree
* trees grow downward - root is the greatest node
* a subtree is downward closed - i.e. subset

<!-- ======================================================================= -->
## wikipedia, tree (graph theory)

* an undirected graph
* any two vertices are connected by exactly one path
* a tree <-> an acyclic connected graph
* a tree - may have more than one root
* a forest - a union of disjoint trees
* a forest - an acyclic graph, not necessarily connected
* rooted tree - has one root only
* directed tree - has directed edges only
* directed rooted tree - a directed tree that has one root only
* arborescence, branching, out-tree - all edges point away from the root
* anti-arborescence, in-tree - all edges point towards the root

tree if one of these equivalent conditions hold

* connected, no cycles
* acyclic, a cycle is formed if any edge is added
* connected, but disconnected if a single edge is removed
* any two vertices can be connected by a unique simple path
* connected, (#V-1) edges
* no simple cycles and (#V-1) edges

more definitions

* internal/inner/branch vertex - `(degree(v) >= 2)`
* external/outer/terminal vertex - `(degree(v) == 1)`
* leaf - a terminal vertex (!!!)
* forest - connected components are trees
* forest - a union of disjoint trees
* forest - an undirected acyclic graph
* discrete graph - vertices only, no edges
* polytree - a DAG whose undirected graph is a tree

rooted tree

* one vertex is designated as "the root"
* edges are either oriented away from the root ex-or towards the root
* free tree - has no designated root
* labeled tree - each vertex has a unique label (e.g. an id number)
* recursive tree - labeled rooted tree where labels respect the tree order
* parent of v - `p` in the rooted path `rp := [r..p,v]`
* except for the root, every vertex has a unique parent
* child of v - `c` in the rooted path `rp := [r..v,c]`
* descendant of v - `d` in the rooted path `rp := [r..v..d]`
* a child is a descendant to its parent
* ancestor of v - `a` in the rooted path `rp := [r..a..v]`
* the root is an ancestor to any other vertex
* sibling vertices have the same parent
* root is external, if it has one child
* note - the degree-based definition of "external"
* height of a vertex - length of the longest downward path `p := [v..l]`
* height of the tree - is the height of its root
* height of a leaf - is zero
* depth of a vertex - length of its rooted path `p := [r..v]`
* depth of the root - is zero

tree-order (!!!)

* a partial ordering on the vertices, such that ...
  `(v < w)` if there is a rooted path `rp := [r..v..w]`

ordered/plane tree (!!!)

* an ordered tree is a rooted tree, such that ...
  each parent node has a first and a last child
* an ordering of children is equivalent to embedding the tree in the plane

<!-- ======================================================================= -->
## wikipedia, tree (data structure)

* a tree is an abstract data type which represents hierarchical structure

basic definitions

* empty tree - a "tree" with no nodes
* root - the top node
* parent `p` - `rp := [r..p,c]`
* child `c` - `rp := [r..p,c]`
* siblings - have the same parent
* descendant to `n` - `rp := [r..n..d]`
* ancestor to `n` - `rp := [r..a..n]`
* leaf - a node with no child nodes
* branch/internal node - a node with children
* degree - number of child nodes
* edge - connection between nodes
* path - sequence of nodes and edges
* depth of node - length of its rooted path
* depth of node - #edges in path(r,n)
* level of node - (1 + depth of node)
* height of node - length of longest downward path
* height of node - is-leaf ? 0 : (1 + max-height(children))
* height of tree - height of its root
* forest - a set of disjoint trees
* subtree - a node and all of its descendants
* subtree - a proper subtree - a proper subset

global definition

* allows to treat the tree as a whole
* e.g. adjacency matrix

recursive definition

* a node that points towards its descendants (out-tree)
* does not necessarily need to have a parent reference
* does not guarantee tree characteristics (!!!)
* e.g. adjacency lists

tree traversal

* walk, walking the tree - visit the nodes one after another
* pre-order - visit parents before their children
* postorder - visit children before their parents
* in-order - left-child, node, right-child
* level-order - a level-by-level breadth-first search

additional statements

* branching factor - #children per node (i.e. each node)
* except for the root, each node has a parent
* no node has more than one parent
* empty trees - affect the complexity of definitions
* trees are drawn growing downwards
* every node can be seen as the root of a subtree
* each node corresponds to a subtree
* clockwise/counterclockwise view on plane trees
* trees are special cases of digraphs
