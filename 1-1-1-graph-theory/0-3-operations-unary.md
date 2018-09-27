
<!-- ======================================================================= -->
# Unary operations on graphs

The following operations take a single input graph `H`
in order to produce a result:

* a single graph `H := (V,F)` is used ...
* to create a new graph `operator(H) := G := (V,E)`
* i.e. `(operator: S -> G)`

<!-- ======================================================================= -->
## wikipeida, transpose graph

* (/see/ "transpose" in "relations" /)
* aka, converse, transpose, reverse
* if (x,y) in G, then (y,x) in the converse graph
* "converse" - from the converse of a logical statement
* i.e. (Q -> P) is the converse of (P -> Q)
* "transpose" - from transposing the adjacency matrix
* notational - G', G^T, etc.

remarks

* little difference in maths, but relevant in computer science
* with regards to incoming/outgoing edges

<!-- ======================================================================= -->
## wikipedia, complement graph

* (/see/ "complement" in "relations" /)
* the complement graph H := (V,F) is inverse to graph G := (V,E)
* i.e. (x adjacent-to y in G) -> not (x adjacent-to y in H)
* i.e. start with a complete graph K(G) and remove all edges in E
* i.e. the same set of vertices, but disjoint sets of edges

definition

* H := (V,K\E), where K is the set of all 2-element subsets of V
* similar with directed graphs - i.e. K is the set of all 2-element pairs

applications/examples

* graph-theoretic concepts are related via complement graphs
* e.g. the complement of an edge-less graph is complete
* e.g. induced subgraph in H is a complement to its counterpart in G

remarks

* self-complementary graph - isomorphic to its own complement
* several classes of graphs are self-complementary

<!-- ======================================================================= -->
## wikipedia, topological sorting

* topological sort, or topological ordering of a DAG
* a linear ordering of vertices such that: aPb -> (a presequent-to b)
* the graph must not have any cycles - i.e. must be acyclic
* any DAG has one or more topological orderings (i.e. >=1)

notes

* used in (instruction) scheduling
* basis for linear-time algorithms
* used to find the critical path of a project
* used to find shortest paths

algorithms

* Kahn's algorithm
* Depth-first search

comments

* a traversal can be understood to visit the vertices
* according to some pre-calculated topological ordering

relation to partial orders

* closely related to linear extensions of partial orders
* i.e. produce a total order for a partial order
* create a partial order from a DAG
* (1) the order's objects are the vertices
* (2) define (x <= y) if (y) can be reached from (x)
* create a DAG from a partial order
* (1) the DAG's vertices are the objects of the order
* (2) define edge (x,y) if (x <= y)
* (3) use transitive reduction

comments

* a "topological sort" could be understood to be rewriting a graph
* i.e. produce a "linear graph/path"

<!-- ======================================================================= -->
## wikipedia, edge contraction (EC)

* merging two adjacent vertices into one and adjusting the edges

definition

* occurs relative to an initial edge `e := (u,v)`
* `e` is removed and its incident vertices are merged
* i.e. the vertices `u` and `v` are merged into a new vertex `w`
* after the vertex merger, incident edges need to be adjusted
* `(uEx -> wEx)`, `(xEu -> xEw)`, `(vEy -> wEy)`, `(yEv -> yEw)`
* i.e. even less edges are possible if `E` is a set
* i.e. edge contraction may in general produce a multiset/graph
* i.e. may or may not be allowed to produce loops

more formal

* remove edge `uEv` and/or `vEu`
* replace `u` by `w` in any edge `uEx` and `xEu`
* likewise, replace `v` by `w`

vertex identification/contraction - i.e. **VC**

* `u` and `v` may or may not be adjacent
* i.e. VC is more general than EC
* i.e. EC is a special case of VC
* edges between `u` and `v` become loops
* i.e. loops may or may not be allowed

vertex cleaving/splitting

* split one vertex into two vertices
* i.e. reverse to vertex contraction

path contraction

* contract a path into a single edge
* edges connected to intermediary vertices may be removed
* or connected to the path's end vertices

(unclear - path contraction)

* what exactly happens to inner vertices?
* note - the path is merged into an edge, not a single vertex
* note - edges incident to an inner vertex may end up ...
* being incident to one endpoint or the other

twisting

* given two disjoint graphs G1 and G2, and some other graph G
* (u1,v1 in V1), (u2,v2 in V2) and (u,v in V)
* identify (u1,u2 as u in G) and (v1,v2 as v in G)
* a twisting G* of G with respect to {u,v}
* identifies u1 with v2, and v1 with u2
* (completely unclear meaning)

application

* used in proof by induction
* e.g. proof that a property holds for a smaller graph,
  and then that the property holds for a larger graph
* e.g. merge essentially equal vertices

<!-- ======================================================================= -->
## wikipedia, planarity testing

* test whether a graph is planar
* i.e. can be drawn on a plane without crossing edges
* O(n) - i.e. linear complexity

<!-- ======================================================================= -->
## wikipedia, hamilton path

* aka. a traceable path
* a path in a graph that visits each vertex
* assumed to visit each vertex only once

hamiltonian-connected graph

* for every pair of vertices,
* there is a hamilton path between both

comment

* presumably uses only the edges in the given graph
* i.e. does not add new ones, which would make no sense anyways

<!-- ======================================================================= -->
## wikipedia, prüfer sequence (tree)

* iteratively remove vertices from a tree until two vertices remain
* set i: remove the leaf with the smallest label and add i to the sequence
* the resulting sequence has length (n-2) and is unique to the tree
* i.e. prüfer-sequence <-> tree

comment

* x is "unique to a tree"
* i.e. tree -> x -> same tree
* the prüfer sequence of a tree can be used to re-create that tree

<!-- ======================================================================= -->
## wikipedia, graph rewriting

* produce a new graph from an input graph

example

* represent the state of a computation/process as a graph
* further execution is understood to transform that graph
* as the result of graph rewrite rules
