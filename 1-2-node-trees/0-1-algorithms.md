
<!-- ======================================================================= -->
# Graph theory algorithms

Algorithms related to graphs and trees.

<!-- ======================================================================= -->
## Prüfer sequence (tree)

* iteratively remove vertices from a tree until two remain
* set i: remove the leaf with the smallest label and add i to the sequence
* the sequence has length (n-2) and is unique to the tree
* i.e. prüfer-sequence <-> tree

comment

* x is "unique to a tree"
* i.e. tree -> x -> same tree

<!-- ======================================================================= -->
## Graph rewriting

* produce a new graph from an input graph

example

* represent the state of a computation/process as a graph
* further execution is understood to transform that graph
* via graph rewrite rules

comment

* "graph rewriting" a generalization of "topological sort"?
* i.e. produce a linear graph

<!-- ======================================================================= -->
## Topological sorting

* topological sort/ordering
* a linear ordering of vertices
* such that `aEb -> (a presequent-to b)`

notes

* only possible with DAGs
* any DAG has one or more topological orderings (i.e. min one)
* most used in "scheduling"
* basis for linear-time algorithms
* find the critical path of a project
* allows to find shortest paths

algorithms

* Kahn's algorithm - start with sinks
* Depth-first search

comments

* "topological sorting" a generalization of "graph traversal"?
* a descendant is subsequent to its ancestors
* related to linear extensions of partial orders

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
