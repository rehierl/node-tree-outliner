
<!-- ======================================================================= -->
# Order structures - structures (1)

<!-- ======================================================================= -->
## wikipedia, preorder

* aka. preset, quasi order
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
* e.g. set (x <= y) if some path p=(x,...,y) exists
* many-one reduction, turing reduction in complexity
* and many more ...

construction

* every bin-rel can be turned into a preorder
* take the reflexive and transitive closures
* create an equivalence relation - set (a ~ b) if (a <= b) and (b <= a)
* create a partial order - via the set of equivalence classes
* from a partial order on a partition one can create a preorder

intervals

* `[a,b] := (a <= x <= b)`
* `[a,b] := { x | (a <= x) and (x <= b) }`
* i.e. an interval represents an intersection of sets

<!-- ======================================================================= -->
## wikipedia, partial order

* aka. poset, a partially ordered set
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
* in-comparable - if neither (a <= b) nor (b <= a)
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

* (<=) non-strict - aka. reflexive, weak
* (<) strict - irreflexive
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
* it needs to be clear what the underlying set and relation operation is
* locally finite - every interval is finite

<!-- ======================================================================= -->
## wikipedia, total order

* aka. loset, toset, a linear/totally ordered set
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
