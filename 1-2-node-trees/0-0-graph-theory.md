
<!-- ======================================================================= -->
# Graph Theory

* prime objects of study in discrete mathematics
* used to model pairwise relations between objects
* sets of vertices/nodes that are connected by edges
* a binary relation `R := (V,V,G)` defines a graph
* a graph is an abstract, non-visual structure
* not to be confused with its visual representation

definition

* `G := (V,E)` <=> `R := (A,B,G)` if `(A == B)`
* `E subset-of (V X V)` is the (multi)set of edges
* `e in E := (a,b)` tuples are referred to as edges
* i.e. both vertices are said to be ends or end vertices
* i.e. both vertices are said to be adjacent
* a vertex `a in V` may not be an end to any edge
* i.e. there may be no `aEb` or `bEa`
* i.e. `a` is not necessarily connected

in the context of this discussion ...

* `G` (i.e. `V`) is assumed to be non-empty, `E` may be empty
* simple graph := `E` is no multiset, no loops
* `G` is a finite simple graph

<!-- ======================================================================= -->
## definitions

* `order(G) := #V`, `size(G) := #E`
* symmetric := if `aEb`, then also `bEa`
* link := `aEb` if `(a != b)`, loop := `aEa`

degree

* `in-degree(v in V) := #{ (a,v) | aEb }`
* `out-degree(v in V) := #{ (v,b) | vEb }`
* `degree(v) := in-degree(v) + out-degree(v)`
* note - loops on `v` (i.e. `vEv`) are counted twice
* `degree(a,b) := #{ (a,b) | aEb } + #{ (b,a) | bEa }`

<!-- ======================================================================= -->
## directed, undirected

* directed/undirected graph is determined by the graph/relation's semantics
* the main focus of this discussion is on directed graphs

undirected

* `aEb` and `bEa` are considered to be equal
* the vertices in an edge appear to be equal
* edges `{a,b}` appear to be 2-element sets
* edges have no specific orientation

directed, digraph

* `aEb` and `bEa` are considered to be unequal
* the vertices in an edge are understood to be "unequal"

edges/arrows

* `(a,b)` is also referred to as "arrow" from `a` to `b`
* `a` reflects the arrow's tail, and `b` the arrow's `head`
* `b` is a direct successor of `a`
* `a` is a direct predecessor of `b`
* `b` is a successor-of and reachable-from `a`,
  if a path exists that leads from `a` to `b`

mixed

* most commonly - either directed xor undirected edges
* however, (`{a,b}`) and (`aEb` and `bEa`) are not necessarily equal
* that is, `aEb` and `bEa` might have different attributes (e.g. weight)
* mixed graph - has both, directed and undirected edges

<!-- ======================================================================= -->
## adjacent to (~)

* with regards to undirected graphs

adjacent vertices

* `(a ~ b), (a adjacent-to b)` is true, if `{a,b} in E`
* `a` and `b` are adjacent to one another
* synonymous - adjacent, strictly related

adjacent edges

* e.g. `e1 := (a,b)` and `e2 := (b,c)`
* two adjacent/consecutive edges share a common vertex

<!-- ======================================================================= -->
## orientation, tournament

* orientation := assign a "direction" to the edges of an undirected graph
* may also refer to the resulting graph of such an operation
* i.e. the "orientation of an undirected graph"
* undirected => orientation => directed

oriented graph

* oriented if `(!aEb and !bEa) xor aEb xor bEa`
* some use "oriented graph" synonymous to "directed graph"
* note - from a strict perspective, both therms are not equivalent

acyclic orientation

* an orientation that does not form any directed cycle

tournament

* take an undirected complete graph
* assign a direction to each edge
* i.e. an orientation of a complete graph

<!-- ======================================================================= -->
## path

* directed graph, digraph => directed path, dipath
* dipath => all edges in the same direction

common notation

* `p := [a, (a,b), b, (b,c), c, ...] "or" [v0,e0,v1,e1, ...]`
* `p := [e0,e1,...] "or" [v0,v1,v2, ...]`
* the vertex in between two neighboring edges is common to both edges

simplified notation

* `aPb := [a, ..., b]`
* a path exists such that it begins in `a` and ends in `b`

notable definitions

* walk - a sequence of edges, no restriction
* open walk - start and end vertex is different
* closed walk - same first and last vertex
* trail - no repeated edges, repeated vertices allowed
* tour - a closed trail
* simple path - no repeated vertices

loops and cycles

* loop - a path such that `p := [a,a]` (i.e. `aEa`)
* cycle - a path such that `p := [a,...,a]` (i.e. a closed walk)
* 1-cycle - a cycle of length one - `p := [a,a]` - (i.e. a loop)
* 2-cycle - a cycle of length two - `p := [a,b,a]`

mixed

* vertex-independent/disjoint paths := to paths have no vertex in common
* edge-independent/disjoint paths := two paths have no edge in common
* `vertex-disjoint -> edge-disjoint`
* distance between vertices := length of shortest path
* diameter of a connected graph := "length of longest path"

<!-- ======================================================================= -->
## connected

connected vertices

* two vertices are connected, if `(aPb or bPa)` is true
* disconnected - not connected

connected graph

* connected graph - for any two vertices `aPb` must be true
* i.e. there are no unreachable vertices
* note the implication - each vertex must be a sink and a source
* note that this refers to the graph as a whole
* disconnected - not connected

weakly/strongly connected

* given a directed graph
* weakly connected - turning the directed edges into undirected edges
  produces an undirected connected graph
* (simply) connected - for any two vertices `(aPb or bPa)` is true
* strongly connected - for any two vertices `(aPb and bPa)` is true

mixed

* two vertices are adjacent, if a path exists such that (#p == 1)
* connected component - a connected subgraph
* i.e. a graph is a partition of components

<!-- ======================================================================= -->
## classification

* multigraph - `E` is a multiset
* simple graph - undirected and `E` is a set (no multiset)
* regular graph - each vertex has the same degree
* complete graph - `E` has an edge for each pair of vertices
* dense graph - #E is close to the maximum number of edges possible
* sparse graph - #E is opposite to dense
* finite graph - sets `V` and `E` are both finite in size
* network - vertices and/or edges have attributes
* planar - can draw `G` on a plane without intersecting edges
* directed acyclic graph (DAG) - finite, directed, no cycles
* polytree - a DAG whose undirected graph is a tree
* tree - connected, no cycles
* forest - a disjoint union of trees
* cyclic - has one or more cycles
* acyclic - has not even one cycle

bipartite graph

* `V` can be split into two sets (`X` and `Y`) such that
* all edges lead from `X` into `Y`, or vice versa

path/linear graph

* all vertices on one path, such that ...
* the degree of all but two vertices is 2
* i.e. one big path

cycle/circular graph

* all vertices on one path, such that ...
* the degree of all vertices is 2
* i.e. one big cycle/loop

aboresence

* there is exactly one path from the root to any other node
* a directed, rooted tree in which all edges point away from the root
* aborecence -> directed acyclic graph (DAG)

<!-- ======================================================================= -->
## graph data structure

* an abstract data type meant to implement a graph
* may represent vertices by references (i.e. external)
* may associate values with edges (e.g. reference, weight, etc)

adjacency list

* associate each vertex with the collection of its neighboring vertices
* e.g. `Hashmap<V,[V]>`

adjacency matrix

* a square matrix of size/dimensions `[#V, #V]`
* elements indicate whether two vertices are adjacent
* symmetric in case of undirected graphs
* empty diagonal if no loops

incidence matrix

* more general than an adjacency matrix (#A X #B)
* i.e. possibly two different sets of vertices
* elements indicate if (a,b) are related (i.e. incident)
