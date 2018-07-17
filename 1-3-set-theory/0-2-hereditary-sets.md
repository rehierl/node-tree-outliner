
<!-- ======================================================================= -->
# Hereditary sets

* aka. pure sets, nested sets
* a set whose elements are all hereditary sets
* all elements are themselves sets
* all elements of the elements are sets
* i.e. never any non-set element

<!-- ======================================================================= -->
## wikipedia, hereditarily finite set (HF)

* a HF set is a set whose elements all are HF sets
* i.e. never any non-set element

recursive definition of well-founded HF sets:

* the empty set `{}` is a HF set
* assume that `a1,...,an` are HF sets
* `{ a1,...,an }` is a HF set

remarks

* V0={}, V1=P(V0), V2=P(V1), ...
* Vom - the set of all well-founded HF sets - union of V0 to VInf
* the HF sets represent a subclass of the "von neumann universe"

ackermann's bijection

* from the natural numbers to HF sets
* aka. bit predicate, ackermann coding

rado/random graph

* vertices are HF sets
* edges - iff one HF set is contained within the other

hereditarily countable sets

* a set that is 

<!-- ======================================================================= -->
## wikipedia, von neumann universe V

* aka. von-neumann-hierarchy-of-sets
* the class of hereditary well-founded sets
* formalized by the Zermelo-Fraenkel set theory (ZFC)

rank of a well-founded set

* smallest ordinal number greater than the ranks of all members
* rank of the empty set is 0
* cumulative hierarchy Va - all sets divided/grouped based on their rank
* Va - all sets having rank less than a
* sets Va - called stages or ranks

(canceled, too abstract)
