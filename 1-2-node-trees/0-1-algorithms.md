
<!-- ======================================================================= -->
# Graph theory algorithms

General algorithms related to graphs and trees.

<!-- ======================================================================= -->
## Prüfer sequence (tree)

* iteratively remove vertices from a tree until two remain
* set i: remove the leaf with the smallest label and add i to the sequence
* the sequence has length (n-2) and is unique to the tree
* i.e. prüfer-sequence <-> tree

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

* a descendant is subsequent to its ancestors
* related to linear extensions of partial orders

<!-- ======================================================================= -->
## Graph rewriting

* produce a new graph from an input graph

example

* represent the state of a computation/process as a graph
* further execution is understood to transform that graph
* via graph rewrite rules

comment

* so a "topological sort" is an edge case?
