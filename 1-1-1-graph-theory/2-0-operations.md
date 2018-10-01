
<!-- ======================================================================= -->
# Operations on graphs

* (/see/ "operations" in "relations" /)
* (/see/ "relationships between sets" /)
* the general focus is (still) on directed (simple) graphs

<!-- ======================================================================= -->
## unary operations

Unary operations take a single input graph `H`
in order to produce a single result:

* a single graph `H := (V,F)` is used ...
* to create a new graph `operator(H) => (V,E) := G`
* i.e. `(operator: Graph -> Graph)`

<!-- ======================================================================= -->
## binary operations

Binary operations take two input graphs `S` and `X`
in order to produce a single result:

* two graphs `S := (T,U)` and `X := (Y,Z)` are used ...
* to create a new graph `(S operator X) := operator(S,X) => (V,E) := G`
* i.e. `(operator: (Graph,Graph) -> Graph)`

Note that the intention behind the binary operations described here is the
description of the relationship between a graph and its subgraphs. The
definitions therefore create new graphs by executing set-based operations
(e.g. union of sets) on the corresponding sets of vertices and/or on the
corresponding sets of edges. That is, the definitions build upon existing
vertices and/or edges rather than the creation of (entirely) new entities
via (e.g.) the Cartesian product (e.g. tensor/strong product).

Note that the binary operations in general require the input graphs to be of
the same sort. That is, the graphs involved are (implicitly) expected to have
similar, if not identical semantics.
