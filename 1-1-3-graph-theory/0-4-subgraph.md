
<!-- ======================================================================= -->
# Subgraph

* targeted at defining subtrees

<!-- ======================================================================= -->
## wikipedia, glossary of terms

* assumed graphs: `G := (V,E)`, `S := (T,U)`, `X := (Y,Z)`
* i.e. vertex sets `V,T,Y` and edge sets `E,U,Z`

subgraph

* a graph `S` formed from another graph `G`
* such that `(T subset-of V)` and `(U subset-of E)`
* `T` must include all endpoints of the edge subset `U`
* `S` may, or may not be connected
* other than that, no further restriction

disjoint

* edge-disjoint - have no edge in common
* vertex-disjoint - have no vertex in common

induced subgraph

* aka. full subgraph
* a subgraph `S` such that `(T subset-of V)`
* and all edges in `E` whose endpoints are in `T`
* i.e. a subset of vertices and all edges between them
* i.e. the subset of edges is not arbitrarily selected

spanning subgraph

* a subgraph `S` such that `(T == V)` and `(U subset-of E)`
* i.e. all vertices, but only a subset of edges
* i.e. a special case of an induced subgraph

intersection

* the largest common subgraph of `G` and `S`
* formed by all vertices and edges that belong to both
* i.e. the intersection graph

regular subgraph

<!-- ======================================================================= -->
## wikipedia, induced subgraph

* formed from a subset of vertices and all the corresponding edges
* i.e. the edges connect vertices within the subset
* i.e. no edge leads into or out of the subset

<!-- ======================================================================= -->
## wikipedia, intersection graph

* undirected edges - two sets intersect each other
* i.e. the intersection of connected sets is non-empty
* i.e. sets may overlap each other

classes of intersection graphs

* interval graphs
* and many more ...
