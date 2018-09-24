
<!-- ======================================================================= -->
# Binary operations on graphs

* two graphs `S := (T,U)` and `X := (Y,Z)` are used ...
* to create a new graph `(S operator X) := operator(S,X) := (V,E) := G`
* i.e. `(operator: (S,X) -> G)`

<!-- ======================================================================= -->
## wikipedia, cographs (join)

* mentioned the join operation on graphs
* create the disjoint union of G and H
* and connect every pair of vertices in (V(G) × V(H))

<!-- ======================================================================= -->
## wikipedia, disjoint union (+)

* aka. graph sum (+)
* used to combine graphs to form a larger graph
* analogous to the disjoint union of sets

remarks

* the result is necessarily disconnected
* classes of graphs may be represented as disjoint unions
* e.g. clusters of graphs are unions of complete graphs
* e.g. every graph is a disjoint union of its components
* e.g. forests (of trees)

unclear ?!?

* either make the vertex sets disjoint before the union, ...
* or expect the graphs to be disjoint from the start
* i.e. a union of disjoint graphs?

<!-- ======================================================================= -->
## wikipedia, cartesian product (¤)

* `G := (S ¤ X) := (V,E)` where `V := (T × Y) := V(S) × V(X)`
* i.e. the cartesian product of both vertex sets
* where `(((x,y),(a,b)) in E)`, if `(x == y)` then `yXb`,
* or if `(y == b)` then `xSa`

In words: The product graph has an edge for each edge in one of the input
graphs. That is, any edge in the product graph represents exactly one edge
(ex-or) in one of the input graphs. Put differently, the edges in the input
graphs appear "interleaved" in the product graph.

remarks

* associative - (A ¤ B) ¤ C == A ¤ (B ¤ C)
* commutative - as an operation on isomorphism classes of graphs
* (A ¤ B) and (B ¤ A)  are naturally isomorphic
* a cartesian product graph can be factorized
* e.g. `(K2 ¤ G)` is a ladder graph, if `G` is a path graph

<!-- ======================================================================= -->
## wikipedia, tensor product (×)

* `G := (S × X) := (V,E)` where `V := (T × Y) := V(S) × V(X)`
* i.e. the cartesian product of both vertex sets
* where `(((x,y),(a,b)) in E)`, if `xSa` and `yXb`

In words: The product graph has an edge, if both input graphs have an edge
that connects the corresponding vertices. That is, any edge in the product
graph represents an edge (and) in both input graphs.

remarks

* aka. direct/categorical/cardinal/relational product
* aka. Kronecker/weak-direct product, conjunction
* e.g. `(G × K2)` is a bipartite graph
* where K2 is the single-edge complete graph

<!-- ======================================================================= -->
## wikipedia, strong product (*)

* `G := (S * X) := (V,E)` where `V := (T × Y) := V(S) × V(X)`
* i.e. the cartesian product of both vertex sets
* where `(((x,y),(a,b)) in E)`, if `(x == y)` then `yXb`,
* or if `(y == b)` then `xSa`, or (`xSa` and `yXb`)

In words: The product graph has an edge, if an input graph (or both) connects
the corresponding vertices. That is, any edge in the product graph represents
one or more edges (and/or) in the input graphs.

remarks

* aka. normal/and product
* i.e. `(S ¤ X)` is a subgraph to `(S * X)`
* i.e. the union of `(S ¤ X)` and `(S × X)`

<!-- ======================================================================= -->
## wikipedia, lexicographic product

* `G := (S lex X) := (V,E)` where `V := (T × Y) := V(S) × V(X)`
* i.e. the cartesian product of both vertex sets
* where `(((x,y),(a,b)) in E)`, if `xSa` ex-or (`(x == a)` and `yXb`)

remarks

* `E` is the lexicographic order, if `U` and `Z` are order relations
* in general non-commutative

<!-- ======================================================================= -->
## wikipedia, series-parallel graphs

* (/see/ "series-parallel partial order" /)

two-terminal graph (TTG)

* the distinguished terminals are called source and sink
* M(x,y) - the vertex that results from merging x and y
* i.e. m := M(x,y) => vEm where vEx or vEy, and mEv where xEv or yEv
* i.e. including the removal of x, y and the corresponding edges

PC(X,Y)

* parallel composition - created from the disjoint union of X and Y
* i.e. SRC(PC) = M(SRC(X),SRC(Y)), likewise SNK(PC) = M(SNK(X),SNK(Y))
* i.e. PC(X,Y) - merged source and sink terminals

SC(X,Y)

* series composition - created from the disjoint union of X and Y
* i.e. SRC(SC) = SRC(X), M(SNK(X),SRC(Y)), SNK(SC) = SNK(Y)
* i.e. SC(X,Y) - merge the sink of X with the source of Y

two-terminal series-parallel graph (TTSPG)

* formed by a series of PC or SC compositions
* starting with the single-edge complete graph K2

DEF1 - series-parallel (SP) graphs

* a TTSPG with a source and a sink
* likewise sp-digraphs - oriented from source to sink

DEF2 - alternatively

* a sp-graph can be turned into a K2 by a series of the following operations
* (1) replacing parallel edges, (2) replacing edges incident to the same vertex

remarks

* SPGs can be recognized in linear time
* used to model electric circuits
* used in complexity theory

generalization

* generalized SP-graphs (GSP)
* includes SP and outerplanar graphs
* adds the deletion operation to DEF2 - dangling vertices may be removed
