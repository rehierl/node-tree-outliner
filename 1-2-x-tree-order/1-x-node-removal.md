
<!-- ======================================================================= -->
# The removal of nodes from a tree

* aka. vertex removal
* (/see/ "operations" in "relations" /)
* (/see/ "operations" in "graph theory" /)
* (/see/ "edge contraction" in "graph theory" /)

<!-- ======================================================================= -->
## relevant, relation-based operations

* reflexive closure - `RC(G) := G + { (v,v) | (v in V) }`
* reflexive reduction - `RR(G) := G \ { (v,v) | (v in V) }`
* transitive closure - `TC*(G) := G + { uEv | uEx and xEu for some x }`
* i.e. iteratively add edges until `TC(n+1) == TC(n)`
* transitive reduction - `TR(G) := G \ { uEv | uPv }`
* i.e. remove those edges for which there is a corresponding path
* i.e. `(TR(G) subgraph-of G)` and `(G subgraph-of TC*(G))`
* cover relation - `CR(G) := TR(RR(G))`

Note that the cover relation is minimal insofar as it has least amount of edges
such that the corresponding complete partial order relation can be recreated.

**TODO**

* restriction - restrict G to a vertex-subset
* anything to do with "induced subgraph/tree"?

<!-- ======================================================================= -->
## general context

a graph is understood as the cover relation of an order relation
i.e. the reflexive, transitive closure of a graph is equal to the order relation

a tree is a partial order - the removal of a node in a tree must be consistent
with the removal of the corresponding element in the tree's partial order -

the removal of a node from a tree must yield the same result as removing the
node from tree's reflexive transitive closure (including all incident edges)

* the removal of a tree's root will result in a forest of trees
* will add the child nodes of the removed node to the node's parent
* i.e. replace the node (in its parent) with the node's child nodes

<!-- ======================================================================= -->

Note that the merger of two vertices into one vertex, could be termed a "vertex
contraction". This operation is however not in the focus of this section. That
is, this section is about the removal of a single vertex and the removal and/or
the adjustment of incident edges.
