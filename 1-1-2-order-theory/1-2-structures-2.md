
<!-- ======================================================================= -->
# Order structures - structures (2)

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

**SKIPPED** - canceled at some point

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
## wikipedia, antichain

* comparable - if (a <= b) or (b <= a)
* incomparable - if neither (a <= b) nor (b <= a)
* chain - a subset of a poset such that each pair is comparable
* antichain - a subset of a poset such that no pair is comparable
* maximal antichain - not a strict subset of any other antichain
* maximum antichain - cardinality is greater-or-equal to any other antichain
* i.e. "any other antichain" with regards to one poset
* width of a poset - cardinality of a maximum antichain
* i.e. width is max k, if partition a poset into k chains

**SKIPPED** - sperner families
**SKIPPED** - join/meet operations

<!-- ======================================================================= -->
## wikipedia, filter

* a special subset of a poset
* e.g. a powerset ordered by inclusion
* filters appear in order theory, lattice theory, topology
* a filter is dual to an "ideal"
* similar to a "net" in topology

definition

* filter F is a non-empty subset of poset (P,<=)
* for (x in F) and (x <= y) => (y in F)
* i.e. upper set, aka. upward closed
* for (x,y in F) a (z in F) exists such that (z <= x) and (z <= y)
* i.e. F is downward directed - aka. a filter base

<!-- ======================================================================= -->
## wikipedia, ideal

* a special subset of a poset
* historically derived from ideals in ring theory
* originally defined for lattices

definition

* ideal I is a non-empty subset of poset (P,<=)
* for (x in I) and (y <= x) => (y in I)
* i.e. I is a lower set, aka. downward closed
* for (x,y in I) a (z in I) exists such that (x <= z) and (y <= z)
* i.e. I is a (upward) directed set

remarks

* proper/strict ideal if not equal to P

<!-- ======================================================================= -->
## wikipedia, directed set

* aka. directed preorder, filtered set
* a set X with a preorder such that X is an upward directed set
* equivalent - a set X such that every subset has an upper bound

upward directed set

* every pair of elements (a,b in X) has an upper bound
* i.e. (c in X) exists such that (a <= c) and (b <= c)

downward directed set

* every pair of elements (a,b in X) has a lower bound
* i.e. (c in X) exists such that (c <= a) and (c <= b)

remarks

* a generalization of totally ordered sets
* totally ordered sets are directed
* posets are not necessarily directed - incomparable elements
* lattices are upward and downward directed
* in topology, directed sets define nets/sequences

<!-- ======================================================================= -->
## wikipedia, lattice order

* a poset in which every two elements have a unique supremum and infimum
* join-semilattice - each pair has a least upper bound
* meet-semilattice - each pair has a greatest lower bound
* lattice - if join- and meet-semilattice

**SKIPPED** - canceled after the definition

<!-- ======================================================================= -->
## wikipedia, semiorder

* two items are incomparable if their numerical scores are too close
* i.e. with regards to a given margin of error

definition

* poset (X,<), (x ~ y) are incomparable if neither (x < y) nor (y < x)
* axiom 1 - must be asymmetric
* axiom 2 - if (x < y), (y ~ z) and (z < w), then (x < w)
* i.e. no transitive incomparability due to the increased "distance"
* axiom 3 - if (x < y), (y < z) and (y ~ w), then (x ~ w), (z ~ w) not both

remarks

* (x ~ x) - due to (a1)
* (<) is transitive - i.e. if (y = z) and due to (a2)
* originally introduced to model human preferences (psychology)

**SKIPPED** - canceled after the definition
