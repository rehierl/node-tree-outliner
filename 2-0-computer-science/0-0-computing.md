
<!-- ======================================================================= -->
# General aspects in computing

<!-- ======================================================================= -->
## tree structures - binary tree

* each node has no more than two child nodes (left and right)
* store data in a particular order
* that order is maintained when changing the tree

<!-- ======================================================================= -->
## tree structures - threaded binary tree

* a binary tree variant
* holds additional pointers to speed up traversals
* the pointers reference the next/previous node in the search
* essentially allows a "list"-based traversal

<!-- ======================================================================= -->
## wikipedia, disjoint-set

* aka. merge-find set, union-find/disjoint-set data structure
* tracks a set of disjoint sets (partition)
* each tree represents a set
* the element of the root is the set's representative member
* does not take into account that each subtree is itself a set
* process - create 1-element trees and join them one by one
* union - attach the root of a tree to the root of another tree
* used to keep track of connected components within a graph

<!-- ======================================================================= -->
## wikipedia, partition refinement

* a technique to represent the partition of a set
* allows to refine the partition by splitting sets into smaller ones

structure

* start with a single set S of all elements
* reach the next set X and split Si in two sets (Si & X) and (Si \ X)
* needs (1) a list of sets, (2) elements per set, (3) a set of elements

e.g. used in Coffman-Graham algorithm for parallel scheduling

* construct a lex-ordered topological sort of a DAG in linear time
* the elements of the disjoint sets are vertices
* sets X are sets of neighbors of vertices

<!-- ======================================================================= -->
## wikipedia, nested set model

* see also - sequences / nested intervals
* a model/technique used to represent nested sets in relational databases
* nested sets - aka. hereditarily finite set, trees, hierarchies
* due to difficulties to express operations on hierarchies
* hierarchies may be expressed as graph databases

technique

* number the nodes according to a tree traversal
* visit each node twice - two numbers per node
* test hierarchy membership by comparing these numbers
* updating is expensive - requires renumbering
* avoid renumbering by using rational numbers - complicated

dynamic endless database tree hierarchy

* used in combination with elements that have very few attributes
* good for queries, not so good for updates
* needs additional tagging for multi-parent support
* implemented as nested intervals
