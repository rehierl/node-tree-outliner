
<!-- ======================================================================= -->
# Graph theory algorithms

* algorithms related to graphs and trees

<!-- ======================================================================= -->
## wikipedia, induced subgraph

* formed from a subset of vertices and all the corresponding edges
* i.e. the edges connect vertices within the subset
* i.e. no edge leads into or out of the subset

<!-- ======================================================================= -->
## wikipedia, topological sorting

* topological sort, or topological ordering of a DAG
* a linear ordering of vertices such that `aPb -> (a presequent-to b)`
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
