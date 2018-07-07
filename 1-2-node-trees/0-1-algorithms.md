
<!-- ======================================================================= -->
# Graph theory algorithms

Algorithms related to graphs and trees.

<!-- ======================================================================= -->
## Hamilton path

* aka. a traceable path
* a path in an undirected/directed graph that visits each vertex
* assumed to visit each vertex only once

hamiltonian-connected graph

* for every pair of vertices,
* there is a hamilton path between both

comment

* presumably uses only the edges in the given graph
* i.e. does not add new ones, which would make no sense anyways

<!-- ======================================================================= -->
## Prüfer sequence (tree)

* iteratively remove vertices from a tree until two vertices remain
* set i: remove the leaf with the smallest label and add i to the sequence
* the resulting sequence has length (n-2) and is unique to the tree
* i.e. prüfer-sequence <-> tree

comment

* x is "unique to a tree"
* i.e. tree -> x -> same tree
* the prüfer sequence of a tree can be used to re-create that tree

<!-- ======================================================================= -->
## Graph rewriting

* produce a new graph from an input graph

example

* represent the state of a computation/process as a graph
* as a result of graph rewrite rules
* further execution is understood to transform that graph

<!-- ======================================================================= -->
## Topological sort

* topological sort/ordering
* a linear ordering of vertices
* such that `aEb -> (a presequent-to b)`

notes

* only possible with DAGs
* any DAG has one or more topological orderings (i.e. min one)
* most used in "scheduling"
* basis for linear-time algorithms
* used to find the critical path of a project
* used to find shortest paths

algorithms

* Kahn's algorithm - start with sinks
* Depth-first search

comments

* seems related to linear extensions of partial orders

comments

* a "topological sort" could be understood to be rewriting a graph
* i.e. produce a "linear graph"

comments

* a graph traversal can be understood to visit the vertices
* according to some pre-executed topological sort

<!-- ======================================================================= -->
## Graph traversal/search

* visit/check/update each vertex
* classified by the order in which each vertex is visited
* graph traversal is a generalization of tree traversal

depth-first search (DFS)

* a tree-based algorithm
* begin with a root and visit child vertices before sibling vertices
* depth before breadth

breadth-first search (BFS)

* a tree-based search
* begin with a root and visit the siblings before any child
* breadth before depth

notes

* in a general graph, vertices may be visited more than once
* visit as infrequently as possible
* serialize/deserialize is more efficient with BFS as it allows
  to re-construct the graph more efficiently
