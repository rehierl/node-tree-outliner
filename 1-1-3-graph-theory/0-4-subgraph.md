
<!-- ======================================================================= -->
# Subgraph

* targeted at the definition of subtrees

<!-- ======================================================================= -->
## wikipedia, glossary of terms

* assumed graphs: `G := (V,E)`, `S := (T,U)`, `X := (Y,Z)`
* i.e. vertex sets `V,T,Y` and edge sets `E,U,Z`

connected graph

* each pair of vertices forms a path
* strong connectivity - in directed graphs
* i.e. a path in both directions exists

connected component

* a maximal connected subgraph

disjoint graphs

* edge-disjoint - have no edge in common
* vertex-disjoint - have no vertex in common

induced subgraph

* aka. full subgraph
* a subgraph `S` such that `(T subset-of V)`
* and all edges in `E` whose endpoints are in `T`
* i.e. a subset of vertices and all edges between them
* i.e. the subset of edges is not arbitrary
* e.g. induced paths, induced cycles

intersection

* the largest common subgraph of `G` and `S`
* formed by all vertices and edges that belong to both
* i.e. the intersection graph

proper subgraph

* removes at least one vertex or edge
* i.e. not isomorphic to G (if finite)
* i.e. the graphs are distinct

spanning subgraph

* a subgraph `S` such that `(T == V)` and `(U subset-of E)`
* i.e. all vertices, but not necessarily all edges between them
* i.e. not a special case of an induced subgraph

subgraph

* a graph `S` formed from another graph `G`
* such that `(T subset-of V)` and `(U subset-of E)`
* `T` must include all endpoints of the edge subset `U`
* `S` is not necessarily connected
* other than that, no further restriction
* subforest - a subgraph of a forest

subtree

* a connected subgraph of a tree
* also - particular subgraphs for rooted trees
* e.g. all vertices and edges reachable from some initial vertex

supergraph

* formed by adding vertices, edges or both
* subgraph <=> supergraph

<!-- ======================================================================= -->
## wikipedia, induced subgraph

* formed from a subset of vertices and all the corresponding edges
* that is, there is no general rule as how the vertex-subset is formed
* in contrary to that, the edge-subset is formed based on the vertex-subset
* i.e. the edges connect vertices within the vertex subset
* i.e. no edge leads into, or out of the vertex-subset
* e.g. induced paths - i.e. subgraphs that are paths
* notational - `G[V']`

<!-- ======================================================================= -->
## wikipedia, intersection graph

* represents the pattern of intersections of a family of sets
* i.e. (un)directed edges - two sets intersect each other
* i.e. the intersection of connected sets is non-empty
* i.e. sets may overlap each other
* classes of graphs defined by the types of sets
* e.g. interval graphs

definition

* create one vertex per set
* connect vertices, if the sets intersect

all graphs are intersection graphs

* any undirected graph represents as an intersection graph
* for each vertex `v` create a set of vertices `Sv`
* that holds all vertices reachable beginning with `v`

**SKIPPED** - many example classes of intersection graphs

<!-- ======================================================================= -->
## wikipedia, clique

* a subset of vertices of an undirected graph such that ...
* every two distinct vertices are adjacent
* i.e. induced subgraphs that are complete
* one of the base concepts of graph theory

classification

* 1-vertex cliques - the vertices
* 2-vertex cliques - the edges
* 3-vertex cliques - triangles
* finding cliques of size N is NP-complete

definitions

* maximal clique - can not add another adjacent vertex
* maximum clique - there is no clique with mor vertices
* clique num of G - size of maximum clique
* intersection num of G - the smallest number of cliques that cover E
* clique cover num of G - the smallest number of cliques that cover V

opposite/antonymous

* every clique corresponds to an independent set in the complement of G
* independent set I - the set of non-adjacent vertices
* i.e. no pair of vertices in I is connected via an edge in G

**SKIPPED** - mathematical results
**SKIPPED** - applications

<!-- ======================================================================= -->
## wikipedia, intersection number

* the smallest number of elements in a representation of a graph
* as an intersection graph of finite sets
* i.e. the smallest number of cliques needed to cover E

**SKIPPED** - all of the main content
