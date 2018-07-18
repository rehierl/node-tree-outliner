
<!-- ======================================================================= -->
# Order structures - structures

comparability graph

* an undirected graph
* connected vertices are comparable
* aka. containment graphs

interval graph

* a family of real intervals
* vertices represent intervals
* edges indicate that two intervals intersect

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
