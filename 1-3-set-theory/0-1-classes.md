
<!-- ======================================================================= -->
# Classes in set theory

<!-- ======================================================================= -->
## wikipedia, classes in set theory

* a collection of sets that can be unambiguously
  defined by a property that all its members share
* proper class - a class that is not a set
* e.g. class of all ordinal numbers, class of all sets
* small class - a class that is a set
* sometimes "class" is used synonymous to "set"

<!-- ======================================================================= -->
## wikipedia, equivalence classes

* when the elements of a set S have a notion of equivalence
* e.g. objects having the same color, size, etc.
* defined by an equivalence relation
* S can be split into equivalence classes
* i.e. each subset counts as class - i.e. synonymous use
* quotient set/space - set of equivalence classes
* S/R - S modulo R - R being the equivalence relation (~)

canonical surjection, canonical projection map

* (f: X -> X/R), (f(x) = [x])
* maps each element x to its equivalence class [x]
* (s: X -> X) - "injective map" or "section"
* map x onto a "representative" of [x]
* i.e. s(x) = c, if c is the representative of [x]
* consequently, s(c) = c
* canonical representative

properties

* two equivalence classes are either equal or disjoint
* the set of all equivalence classes forms a partition

graphical representation

* an undirected graph may be associated to any symmetric relation on X
* vertices are all elements of X
* two vertices s and t are joined iff s~t

invariant, well-defined

* `(P: X -> bool)` - invariant of R, well-defined under R
* i.e. property of x has a specific value
* if (P(x) and P(y)) whenever xRy
* `(f: X -> Y)` - class invariant under R
* i.e. a mapping from one set to another
* if (f(a) == f(b)) whenever aRb
* any function can be understood to define an equivalence relation
* aka. kernel of f
