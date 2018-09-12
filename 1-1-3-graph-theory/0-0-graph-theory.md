
<!-- ======================================================================= -->
# Graph Theory

* for the most part notes taken from wikipedia pages
* i.e. pages that are in general dedicated to "graph theory"

general notes

* in graph theory, the "undirected" case seems to be the default
* most commonly, either directed ex-or undirected edges - no mixed graph
* (`{a,b}`) and (`aEb` and `bEa`) are not necessarily equal
* e.g. `aEb` and `bEa` might have different attributes (e.g. weight)

<!-- ======================================================================= -->
## wikipedia, graph theory

* graphs are objects of study in discrete mathematics (dm)
* used to model pairwise relations between objects
* sets of vertices/nodes/points connected via edges/arcs/lines

definition

* `G := (V,E)` - i.e. a binary/endo-relation
* set of vertices `V`, set of edges `(E subset of V×V)`
* unordered if `e = {a,b}`, ordered if `e = (a,b)`
* multigraph - if `E` is a multiset
* simple graph - if `E` is a true set of unordered pairs (no loops)
* the vertices of an edge are said to be ends or end vertices
* order(G) = #V - the number of its vertices
* size(G) = #E - the number of its edges
* degree(v) - the number of connected edges

application

* used to model relations
* e.g. networks of communication
* e.g. flow of computation

**SKIPPED** - history

graph drawing

* vertices as circles, edges as lines/arcs/arrows between them
* a graph however is an abstract, non-visual structure
* i.e. not to be confused with its visual representation
* hint - one graph, multiple visual representations

data structures

* depends on the problem domain
* incidence list - array of pairs of vertices
* adjacency list - lists of neighbors of each vertex
* i.e. `[(a,b), ...]` vs. `[(a,[b]), ...]`
* incidence matrix - `[vertex-to-edge] := {0,1}`
* adjacency matrix - `[vertex-to-vertex] := {0,1}`

subgraphs, induced subgraphs, minors

* subgraph - subset of vertices and edges between them
* i.e. not necessarily all the edges between them
* reason - many graph properties are hereditary
* i.e. a graph has a property iff all subgraphs have it too
* induced subgraph - a subgraph, but all edges in the vertex subset

**SKIPPED** - most of the applications listing

<!-- ======================================================================= -->
## wikipedia, graph (dm)

* object of study in discrete mathematics (dm)
* a set of objects in which some pairs are related
* objects - aka. vertices, nodes points
* pairs of objects - aka. edges/arrows E, arcs/lines A
* depicted as a set of connected dots
* edges may be directed (oriented) or undirected
* consequently, graphs may be directed or undirected

definition

* a graph is an ordered pair `G := (V,E)`
* set of vertices `V`, set of edges `E` or arcs `A`
* undirected, if `e := {a,b}` for all `(e in E)` and some `(a,b in V)`
* i.e. pairs are 2-element subsets of `V`
* directed, if `e := (a,b)` for all `(e in E)` and some `(a,b in V)`
* `E` may be a multiset of edges => multigraph
* `a` and `b` may be referred to as ends or end vertices
* a vertex `x` may exist such that neither `xEa` nor `aEx`
* in general `V`, `E` finite sets and `(#V > 0)`
* `order(G) := #V` and `size(G) := #E`
* `degree(x) := #({ xEa } union { aEx })`
* i.e. loops (i.e. `xEx`) are counted twice

adjacency relation (~)

* induced by the edges of an undirected graph
* i.e. an induced symmetric binary relation `R := (V,~)`
* `(a ~ b), (a adjacent-to b) := (e in E)` for `e := {a,b}`
* adjacent vertices - `a` and `b` in `e := (a,b)`
* `a,b` and `e` are said to be incident
* adjacent edges - e.g. `e1 := (a,b)` and `e2 := (b,c)`
* aka. consecutive arrows

clarified definitions

* undirected graph - `aEb` and `bEa` are considered equal
* i.e. unordered pairs `{a,b}` instead of ordered pairs `(a,b)`
* `G := (V,A)` in case of undirected graphs
* directed graph (aka. digraph) in case of directed edges
* `(x -> y) := (x,y)` an arrow with head `y` and tail `x`
* `(y direct-successor-of x)`, if `xEy`
* aka. `(x direct-predecessor-of y)`
* `(y successor-of x)`, if `xPy`
* aka. `(y reachable-from x)`, `(x predecessor-of y)`
* inverted arrow `yEx` of arrow `xEy`
* `G` is symmetric iff `xEy -> yEx`
* oriented graph, if `xEy`, but not `yEx` (i.e. not both)
* i.e. not necessarily equal to "directed graph"
* mixed graph if `G := (V,E,A)` - i.e. has edges and arcs
* link if `aEb` for `(a != b)`, loop if `aEa`
* multigraph if `( #({ aEb }) > 1 )`
* simple graph - unordered, no multigraph, no loops
* quiver, multi-digraph - i.e. a directed multigraph
* weighted graph - edges have associated weights/values

classes of graphs

* regular graph - each vertex has the same number of neighbors
* k-regular graph - each vertex has degree k
* complete graph - each vertex is connected to all other vertices
* finite graph - `V` and `E` are both finite sets
* connected graph - a path exists for any pair of vertices
* strongly connected - a directed path exists for any pair
* weakly connected - an undirected path exists for any pair
* disconnected graph - not (|strongly|weakly) connected
* bipartite graph - `V` is a union of two disjoint sets
* i.e. the edges lead from one set to the other
* path graph - aka. linear graph - the whole graph resembles a path
* planar graph - can be drawn on a plane without crossing edges
* cycle graph - a path graph that resembles a closed path
* tree - connected with no cycles
* forest - a union of disjoint trees

properties

* null graph - no vertices and no edges
* trivial graph - one vertex, no edges
* edgeless graph - vertices, no edges

A symmetric, loop-less graph `G` is equivalent to a simple undirected graph
`G'` (i.e. `{a,b} in E'` if `aEb` and `bEa`).

<!-- ======================================================================= -->
## wikipedia, graph theory (abstract data type)

* used to implement an undirected or directed graph
* may represent vertices by references (i.e. external)
* may associate values with edges (e.g. reference, weight, etc)

adjacency list

* associate each vertex with the collection of its neighbors
* supports additional vertex properties
* e.g. `Hashmap<V,[V]>`

adjacency matrix

* a square matrix of size/dimensions `[#V, #V]`
* elements indicate whether two vertices are adjacent
* symmetric in case of undirected graphs
* empty diagonal if no loops

incidence matrix

* more general than an adjacency matrix `[#V, #E]`
* i.e. possibly two different sets of vertices
* elements indicate if (a,b) are related (i.e. incident)
