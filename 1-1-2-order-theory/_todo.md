
<!-- ======================================================================= -->
# TODO - order theory

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
