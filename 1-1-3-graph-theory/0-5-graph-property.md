
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

<!-- ======================================================================= -->
## wikipedia, glossary of terms

graph property

* true for some graphs, but not for others
* depends only on the graph structure
* not incidental/invariant - e.g. no labels
* may be described as classes of graphs
* e.g. the set of subgraphs of a section (???)

maximal subgraph

* a subgraph of `G` that has property `p` such that ...
* none of its super-graphs in `G` have `p`
* i.e. a maximal element of the subgraphs in `G` with `p`
* e.g. maximal clique, (belongs-to section)
* maximum -> maximal, but not vice versa

maximum subgraph

* the largest subgraph among all subgraphs with property `p`
* (don't yet see the difference to maximal ...)

minimal subgraph

* no proper subgraph has the same property
* i.e. a minimal element of the subgraphs with `p`

monotone property

* a property that is closed under subgraphs
* if G has a hereditary property, then so must every subgraph
* hereditary - closed under induced subgraphs
* minor-closed - closed under minors

<!-- ======================================================================= -->
## wikipedia, hereditary property

* an object property inherited to all sub-objects
* used in topology, graph theory, set theory
* graph theory - a graph property that also applies to its induced subgraphs
* (/see/ "hereditary sets" /)

<!-- ======================================================================= -->
## wikipedia, graph minor

* an undirected graph H of another graph G
* H is formed from G by deleting edges/vertices and/or edge contraction

definition

* undirected H of undirected G - if an isomorphic graph I exists ...
* that can be derived from G by contracting edges, deleting edges/vertices

**SKIPPED** - parts non-relevant to the discussion
