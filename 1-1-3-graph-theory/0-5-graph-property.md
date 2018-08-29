
<!-- ======================================================================= -->
# Graph properties

* the association of nodes with sections is similar to a graph property
* the association of a node carries over to its descendants
* but, an association is initially a node property, not a graph property
* however, an association could be considered a property of a subgraph

some similarity with style sheets in CSS

* seems to be more similar to CSS properties
* unless overridden, these are inherited to all descendants

<!-- ======================================================================= -->
## wikipedia, hereditary property

* an object property inherited to all sub-objects
* used in topology, graph theory, set theory
* graph theory - a graph property that also applies to its induced subgraphs
* (/see/ "hereditary sets" /)

<!-- ======================================================================= -->
## wikipedia, graph property

* aka. graph invariant
* depends only on the abstract structure
* not on a particular representation

property vs. invariant

* a property is preserved under all isomorphisms of a graph
* i.e. a property of the graph itself, not one of presentation
* "property" is used for descriptive characterizations
* e.g. has no vertices of degree 1
* "invariant" is used for quantitative properties
* e.g. the number of vertices of degree 1

definition - graph property

* in general a class of graphs such that ...
* any two isomorphic graphs belong to the class
* i.e. they either both belong to the class, or they don't
* (f: G -> B) - indicator function
* class of graphs G, boolean indicator set B
* f(g) is true, for any graph (g in G)
* f(g1) <-> f(g2) if (g1 isomorphic-to g2)

definition - graph invariant

* aka. graph parameter
* (f: G -> X), where X is a general set of values
* i.e. a graph property if invariant and (X == Bool)
* f(g1) == f(g2) if (g1 isomorphic-to g2)

properties of properties

* many properties are well-behaved with respect to posets or preorders
* hereditary - every induced subgraph has the same property
* monotone - every subgraph has the same property
* monotone -> hereditary, but not necessarily vice versa
* minor-closed - every graph minor has the same property

**SKIPPED** - properties of invariants
