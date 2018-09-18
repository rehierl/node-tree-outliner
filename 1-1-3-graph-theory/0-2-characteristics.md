
<!-- ======================================================================= -->
# Graph characteristics

* notes of pages dedicated to specific aspects

<!-- ======================================================================= -->
## wikipedia, directed graph

* aka. digraph
* each edge in a directed graph has a direction/orientation
* i.e. the edges are ordered pairs of vertices
* arcs A - undirected connections, unordered pairs
* edges E - directed connections, ordered pairs - aka. arrow
* directed multigraph - allow more than one edge per pair
* loops - i.e. aEa - may or may not be allowed

classes

* simple digraph - no loops and max one edge per pair
* symmetric digraph - if aEb, then also bEa
* complete digraph - (aEb and bEa) holds for all pairs
* oriented graph - if aEb, then !bEa
* tournament - a digraph derived from an undirected graph
* acyclic digraph (DAG) - a digraph with no cycles
* weighted digraph - a digraph such that each edge has a weight
* weighted digraph - aka. directed network
* undirected network - aka. weighted graph

terminology

* arrow (x,y) - directed from x to y - tail x, head y
* direct successor y of x, direct predecessor x of y
* ideg, in-degree(x) - the number of head ends adjacent to x
* i.e. the number of arrows that lead into x
* odeg, out-degree(x) - the number of tail ends adjacent to x
* branching factor - the number of arrows that lead away from x
* source - if (ideg == 0) - i.e. no incoming arrows
* sink - if (odeg == 0) - i.e. no outgoing arrows
* (somewhat odd definitions for source/sink)
* (as it includes that any isolated vertex is a source and a sink)
* internal - a vertex that is neither a source, nor a sink
* balanced digraph - if (ideg == odeg) for each vertex

remarks

* directing/orientating an edge - (undirected -> directed)
* i.e. associate a direction/orientation with an edge
* undirecting an edge - (directed -> undirected)
* i.e. remove the orientation of an edge
* similar directed/undirected graph

<!-- ======================================================================= -->
## wikipedia, directed acyclic graph (dag)

* a finite directed graph with no cycles
* there is no path possible that begins and ends in some vertex
* forests - the undirected counterparts

topological ordering

* every dag has a topological ordering
* in general, this ordering is not unique
* unique iff a directed path exists that contains all vertices
* e.g. path graph

**SKIPPED** - parts non-relevant to the discussion

<!-- ======================================================================= -->
## wikipedia, degree

* aka. valency
* deg(v), degree(v) - the number of edges incident to a vertex
* note - a vertex incident to an edge, an edge incident to a vertex
* note - loops are counted twice
* maximum degree - max({ deg(v) | (v in V) }) =: max_deg(G)
* minimum degree - min({ deg(v) | (v in V) }) =: min_deg(G)
* deg(G) := max_deg(G), if (max_deg == min_deg)

degree sequence

* the non-increasing sequence of degrees
* e.g. seq(G) = (5, 3, 3, 2, ....)
* not unique to a graph

vertex related

* isolated vertex, if (deg(v) == 0)
* leaf/end vertex, if (deg(v) == 1)
* k-regular graph, if each vertex has the degree k
* deg(G) = k for a k-regular graph

<!-- ======================================================================= -->
## wikipedia, regular graph

* each vertex has the same number of neighbors
* i.e. every vertex has the same degree
* i.e. same ideg/odeg for digraphs

<!-- ======================================================================= -->
## wikipedia, branching factor

* the number of children at each node
* average branching factor, if not uniform
* i.e. not all nodes have the same number of child nodes

<!-- ======================================================================= -->
## wikipedia, connectivity

* connected - a path exists between any pair of vertices
* i.e. there are no unreachable vertices
* note - each vertex must be a sink and a source
* disconnected - if not connected
* i.e. if there is even one vertex that can not be reached
* a graph with one vertex only counts as being connected

definitions

* two vertices are connected - if a path exists between them
* adjacent vertices - connected via a path of length 1 - i.e. an edge
* component - a maximal connected subgraph
* i.e. each vertex belongs to exactly one component
* i.e. a graph is a union of disjoint components
* weakly connected - the underlying undirected graph is connected
* (simply) connected - (xPy or yPx) for all pairs
* strongly connected - (xPy and yPx) for all pairs

**SKIPPED** - parts non-relevant to the discussion

<!-- ======================================================================= -->
## wikipedia, orientation

* the orientation of an undirected graph
* an assignment of direction to each edge
* i.e. the directed graph of an undirected graph
* i.e. undirected => orientation => directed

oriented graph

* a digraph with no symmetric edges
* oriented if `(!aEb and !bEa) ex-or aEb ex-or bEa` (i.e. asymmetric)
* note - can not have any reflexive edges `aEa`
* a tournament is an orientation of a complete graph
* a polytree is an orientation of an undirected tree
* directed <=!=> oriented

**SKIPPED** - parts non-relevant to the discussion

<!-- ======================================================================= -->
## wikipedia, complete graph (Kn)

* a simple undirected graph
* in which every vertices is connected to all other vertices
* a complete digraph - same with one directed edge per pair
* visualization - all vertices on the same circle

notational

* a `Kn` graph has `n*(n-1)/2` edges
* a regular graph of degree `(n-1)`
* K1 - a 1-vertex edgeless graph
* K2 - a 2-vertex path graph
* K3 - a 3-vertex triangular graph

<!-- ======================================================================= -->
## wikipedia, dense graph

* dense graph - the number of edges is close to the maximum
* i.e. almost a complete graph
* sparse graph - has very few edges
* only vague distinction between both

<!-- ======================================================================= -->
## wikipedia, tournament

* a digraph obtained by assigning a direction to each edge
* in an undirected complete graph
* i.e. the orientation of a complete graph
* used in voting theory, social choice theory, ...

**SKIPPED** - parts non-relevant to the discussion

<!-- ======================================================================= -->
## wikipedia, polytree

* aka. oriented tree, singly connected network
* an acyclic digraph whose underlying undirected graph is a tree
* i.e. gain an undirected tree by removing the directon of each edge
* e.g. an arborescence - i.e. rooted directed trees
* note - every polytree is a multitree - i.e. not necessarily rooted

<!-- ======================================================================= -->
## wikipedia, planar graph

* a graph that can be embedded in a plane
* i.e. no intersecting/crossing edges
* drawing - plane graph, planar embedding of the graph
* defined as mapping from a node to a point on the plane

**SKIPPED** - parts non-relevant to the discussion
