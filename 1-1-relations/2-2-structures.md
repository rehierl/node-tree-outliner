
<!-- ======================================================================= -->
# Order structures - structures

<!-- ======================================================================= -->
## wikipedia, weak ordering

* formalization of ranking of a set
* may contain ties - i.e. may have equal items
* a generalization of totally ordered sets
* e.g. ranking of a set

axiomatized as - strict weak ordering (SWO,<)

* the incomparability relation is an equivalence relation
* i.e. if neither (a < b) nor (b < a), then (a = b)
* however, (a = b) counts as incomparable under (<)

axiomatized as - total preorder

* SWOs are closely related to total preorders or (non-strict) weak orders
* a "total preorder" or "weak order" is a preorder that is total

axiomatized as - ordered partitions

* partition + total order => an ordered partition / a list of sets

remarks

* SWOs generalize semiorders, but don't assume transitivity of incomparability
* strict total order - a trichotomous SWO

**TODO** - canceled at some point

<!-- ======================================================================= -->
## wikipedia, well order

* aka. well-ordering, well-order relation
* a total order in which each non-empty subset has a least element
* i.e. a well-order has itself a least element
* least element - smaller than every other element
* in general, each element has a unique successor (i.e. a next element)
* i.e. the least element of all elements greater than
* every subset that has an upper bound has a least upper bound
* i.e. the least element of all upper bounds
* strict well ordering <=> well-founded strict total order
* well-founded - every non-empty subset has a minimal element
* well-ordering principle - the natural numbers are well ordered under (<)

ordinal numbers

* the position of each element is given by an ordinal number
* i.e. assign an ordinal number one-by-one to each element
* order type - in this context the association with ordinal numbers
* zero-based or one-based counting

examples

* natural numbers
* integers - not well-ordered as there is no least negative
* reals - similar to integers

<!-- ======================================================================= -->
## wikipedia, preorder

* aka. quasi order
* must be - reflexive, transitive
* note - a preorder may have more characteristics
* partial order - an antisymmetric preorder
* equivalence relation - a symmetric preorder
* "pre-order" - almost a (partial) order, but not quite
* note - the (<=) operator/symbol does not always apply
* preordered set, proset - a set equipped with a preorder

directed graphs

* preorder => a graph such that edges correspond with the order relation
* preorder => a directed graph (with possibly disconnected components)
* partial order => a DAG - loops, but no cycles
* most directed graphs are neither reflexive, nor transitive
* graphs may however have cycles

examples

* reachability relationship in a directed graph
* i.e. (x <= y) if some path p=(x,...,y) exists
* many-one reduction, turing reduction in complexity
* and many more ...

construction

* every bin-rel can be turned into a preorder
* take the reflexive and transitive closures
* create an equivalence relation - (a ~ b) if (a <= b) and (b <= a)
* create a partial order - via the set of equivalence classes
* from a partial order on a partition one can create a preorder

intervals

* `[a,b]` => (a <= x <= b) - i.e. an intersection of sets

<!-- ======================================================================= -->
## wikipedia, equivalence relation (ER,~)

* there is no "equivalence order" because
* there is no direction (i.e. "before" or "after")
* i.e. there is consequently no "order"
* all elements are either equal or unequal
* i.e. disjoint equivalence classes of equal elements

remarks

* must be - reflexive, transitive, symmetric
* i.e. a symmetric preorder
* e.g. "is-equal-to" is the canonical example
* any ER represents a partition of the underlying set

construction

* (~) is an equiv. relation on set X
* P(x) is a property of elements of X
* P(x) is well-defined, if whenever (x ~ y) => P(x) is true if P(y) is true

### wikipedia, setoid

* aka. e-set, bishop set, extensional set
* a setoid is a set euipped with an ER
* used in proof theory, type theory

### wikipedia, partition of a set

* aka. a family of sets
* group the elements of set X into a set of non-empty disjoint subsets P
* equivalence relation <= defines => partition
* subsets in P - blocks, parts, cells
* rank of P - (#X - #P) - (#elements >= #blocks)
* e.g. "equal to", "similar to"

### wikipedia, partial equivalence relation (PER)

* aka. restricted equivalence relation
* must be - symmetric, transitive
* "partial" here - "almost, but not quite"

<!-- ======================================================================= -->
## wikipedia, partial order

* poset - a partially ordered set
* formalizes the intuitive concept of ordering
* i.e. a set joined with a binary relation on that set
* the relation indicates which element precedes another
* partially - not all elements need to be comparable
* i.e. pairs may exist that are in-comparable
* e.g. subset with regards to disjoint sets
* visualized by hasse-diagrams

partial order - e.g. (subset-of)

* must be - reflexive, transitive, anti-symmetric
* i.e. an anti-symmetric pre-order
* comparable - if (a <= b) or (b <= a)
* in-comparable - if not comparable
* antichain - a subset in which all elements are in-comparable
* covered - no 3rd element fits in between two elements

examples

* powerset ordered by inclusion
* natural numbers ordered by divisibility - i.e. (a|b)
* vertices in a directed acyclic graph (DAG) ordered by reachability

extrema

* least/greatest elements
* minimal/maximal elements
* upper/lower bounds

**TODO** - cartesian product of posets
**TODO** - sums of posets

strict/non-strict partial orders

* non-strict - aka. reflexive, weak
* strict - irreflexive
* note - pairs may still be incomparable
* the non-strict order is the reflexive closure of the strict order
* strict partial orders correspond more closely with DAGs
* i.e. every strict partial order is a DAG

**TODO** - inverse and order dual
**TODO** - mappings between posets
**TODO** - number of posets

linear extension

* an extension of a poset that is linear/total
* every partial order can be extended to a total order
* topological sorting - find an extension for a DAG

**TODO** - category theory
**TODO** - posets in topological spaces

interval

* `[a,b]` => set of elements satisfying (a <= x <= b)
* `(a,b)` => elements satisfying (a < x < b)
* locally finite - every interval is finite

<!-- ======================================================================= -->
## wikipedia, antichain

* comparable - if (a <= b) or (b <= a)
* incomparable - if neither (a <= b) nor (b <= a)
* chain - a subset of a poset such that each pair is comparable
* antichain - a subset of a poset such that
  no two distinct elements are comparable
* maximal antichain - not a strict subset of any other antichain
* maximum antichain - cardinality is greater-or-equal to any other antichain
* i.e. "any other antichain" with regards to one poset
* width of a poset - cardinality of a maximum antichain
* i.e. width is max k, if partition a poset into k chains

**TODO** - sperner families
**TODO** - join/meet operations

<!-- ======================================================================= -->
## wikipedia, total order

* aka. totally/linearly/simply ordered set, chain
* aka. total/linear/simple order, (non-strict) ordering
* linear extension - transform a partial order into a total order

total order - e.g. (<=)

* must be - reflexive, transitive, anti-symmetric, connex
* i.e. a total partial order
* i.e. the set can be "linearized"

strict total order - e.g. (<)

* must be - transitive, trichotomous, strict weak order
* i.e. total, but not reflexive

remarks

* chain - either synonymous or with regards to some subset
* height of a poset - size/length of largest chain

examples

* e.g. any set of cardinal/ordinal numbers

**TODO** - continue with "further concepts"
