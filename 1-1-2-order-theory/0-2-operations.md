
<!-- ======================================================================= -->
# Order structures - operations

<!-- ======================================================================= -->
## wikipedia, order type

* two ordered sets have the same "order type" if they are "order isomorphic"
* i.e. an order-preserving bijective order-isomorphic mapping exists
* e.g. (n -> 2*n) on the set of integers

<!-- ======================================================================= -->
## wikipedia, order isomorphism

order isomorphism

* a monotone function
* an isomorphism for posets

ordinal number

* ordinal number - generalization of "natural number"
* any finite set can be put in order by counting its elements
* i.e. label its elements with distinct natural numbers
* ordinal numbers are used to describe the order type of well ordered sets

order type

* order isomorphic - ordered sets X and Y have the same order type
* requires a bijection (1:1, e.g. `n -> 2*n`)
* must be order-preserving
* every well-ordered set is order-equivalent to exactly one ordinal number

remarks

* given posets (P,<=) and (Q,<=) and (f: P -> Q)
* (f) is an isomorphism, if: (x <= y) <-> (f(x) <= f(y))
* i.e. order-preserving and order-reflecting
* (f) may also be referred to as an order-isomorphism
* if an (f) exists, P and Q are referred to as being order-isomorphic
* P and Q have identical hasse diagrams

<!-- ======================================================================= -->
## wikipedia, order embedding

* a monotone function
* used to include one poset into another
* a notion that is strictly weaker than order isomorphism
* may be understood in terms of category theory

formal

* two posets (S,<=) and (T,<=)
* (f: S -> T) is an order embedding if
* (f) is order-preserving and order-reflecting
* (x <= y) <-> (f(x) <= f(y)) for all (x,y in S)

remarks

* (f) must be injective
* S can be embedded into T, if an order-embedding exists
* an order-isomorphism is a surjective order-embedding
* an order-embedding restricts to an isomorphism between S and f(S)

perspectives

* a poset is a reflexive, transitive DAG
* an order-embedding is a graph-isomorphism to an induced subgraph
* a poset is a (small,skeletal) category
* an order-embedding is an isomorphism to a full subcategory

<!-- ======================================================================= -->
## wikipedia, series-parallel partial order

* (/see/ "series-parallel graph" /)
* a poset formed by composition from smaller series-parallel posets
* characterized as N-free finite posets
* include weak orders, reachability in directed trees
* the comparability graphs of series-parallel posets are cographs

series composition (SC) - P;Q, P*Q, P<Q

* given two posets P and Q
* the disjoint union of the elements in P and Q
* if (x,y in P/Q), ordered according to P ex-or Q
* i.e. both either in P ex-or both in Q
* if (x in P) and (y in Q), then ...
* both have an additional order (<=) in the composition
* SC is associative, but not commutative

parallel composition (PC) - P||Q, P+Q

* given two posets P and Q
* the disjoint union of elements in P and Q
* if (x,y in P/Q), ordered according to P ex-or Q
* if (x in P) and (y in Q), then incomparable
* PC is associative and commutative

ties with graph theory

* any poset may be represented by a directed acyclic graph
* note - there is usually more than one way to do so
* vertex-sp (vsp) graph - the graph of a sp poset
* minimal vsp graphs - the transitive reduction (i.e. cover relation)

remarks

* class of sp-posets formed by composition from one-element posets
* weak order - a sp-poset such that all PCs are executed first

**SKIPPED** some aspects

<!-- ======================================================================= -->
## wikipedia, product order

* short - prod-order
* given two ordered sets A and B
* induce a partial ordering on the Cartesian product (A × B)
* (a1,b1) and (a2,b2) in (A × B)
* (a1,b1) <= (a2,b2) iff (a1 <= a2) and (b1 <= b2)

remarks

* aka. coordinate-wise order, component-wise order
* the product order of two totally ordered sets is not total
* e.g. (0,1) and (1,0) are incomparable
* in general, the prod-order is a sub-relation of the lexi-order

<!-- ======================================================================= -->
## wikipedia, linear extension

* short - lin-ext
* the linear extension of a poset is a total order
* the lexi-order of a totally ordered set is a lin-ext of its prod-order

definition

* given o1 and o2 on set X
* o2 is a lin-ext of o1, if
* 1) o2 is a total order
* 2) if (x o1 y), then (x o2 y) for all (x,y in X)

remarks

* o2 is said to extend o1
* a lin-ext is a order-preserving bijection from a poset to a chain

principle

* known as the order-extension principle
* proven by the use of the "axiom of choice"
* the principle is itself taken as an axiom
* a partial order in which every pair is incomparable can be extended
* i.e. every poset can be linearly ordered
* known as the ordering principle
