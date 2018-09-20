
<!-- ======================================================================= -->
# Unary operations on graphs

* a single graph `H := (V,F)` is used ...
* to create a new graph `operator(H) := G := (V,E)`
* i.e. `(operator: S -> G)`

<!-- ======================================================================= -->
## wikipedia, complement graph

* the complement graph H := (V,F) is inverse to graph G := (V,E)
* iff (x adjacent-to y in G) -> not (x adjacent-to y in H)
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
## wikipedia, edge contraction

* merging two adjacent vertices into one and adjusting the edges

definition

* occurs relative to a particular edge `e`
* `e` is removed and its incident vertices `u` and `v`
  are merged into a new vertex `w`
* edges then need to be modified
* `(uEx -> wEx)`, `(xEu -> xEw)`
* `(vEy -> wEy)`, `(yEv -> yEw)`
* note - fewer/merged edges are possible if `E` is a set
* note - will in general produce a multiset
* note - may or may not be allowed to produce loops

more formal

* remove edge `uEv` and/or `vEu`
* replace `u` by `w` in any edge `uEx` and `xEu`
* likewise, replace `v` by `w`

vertex identification

* aka. vertex contraction
* `u` and `v` may or may not be (strictly) connected
* i.e. more general than edge contraction

path contraction

* contract a path into a single edge
* edges connected to intermediary vertices may be removed
  or connected to the end vertices

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
