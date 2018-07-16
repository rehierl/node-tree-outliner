
<!-- ======================================================================= -->
# Set theory

( See "mathematics" for the core concept of sets )

<!-- ======================================================================= -->
## wikipedia, set theory

* a branch of mathematical logic
* a binary relation between objects and a sets
* xRs - holds if x is an element of s
* subset relation - aka. set inclusion

pure/hereditary sets

* a set whose elements are all hereditary sets
* all elements are themselves sets, as are all elements of the elements
* i.e. never any non-set elements?

urelement

* aka. atoms, individuals, etc.
* an element of a set that is itself not a set
* non-empty sets contain members, urelements do not
* urelements cannot have members - proper classes cannot be members

quine atoms

* instead of considering urelements to be a special type of object
* consider them to be a particular type of set
* quine atoms - sets that only contain themselves - i.e. (x = {x})

applications

* many mathematical concepts can be defined using set theoretic concepts
* e.g. graphs - defined as sets satisfying axiomatic properties
* e.g. properties of natural numbers can be derived within set theory
* hence - axiomatic vs. naive set theory

objections to set theory as foundation of mathematics

* issue - introduces non-computable objects
* e.g. infinite sets

<!-- ======================================================================= -->
## wikipedia, finite set

* finitely many elements
* cardinality is a natural number
* n-set - a set with `n` elements
* k-subset - a subset of a set with `k` elements - `(k <= n)`
* no bijection between a finite set and a strict subset

<!-- ======================================================================= -->
## wikipedia, family of sets

* family of sets - a collection of any sets
* family of subsets of S - a collection of subsets of a given set S
* depending on the context, subsets are not required to be disjoint
* (F subset-of P(S)) - for any family without repeated members
* e.g. the power set is a family of subsets

<!-- ======================================================================= -->
## wikipedia, disjoint sets

* disjoint - no elements in common - i.e. empty intersection
* pairwise/mutually disjoint - all distinct sets in a family are disjoint

"disjoint union" is in general ambiguous

* may mean a family of sets in which all sets are pairwise disjoint
* may mean a modified union operation (discriminated union)

disjoint/discriminated union

* replace each element with a tuple: (element,source-index)
* this makes all elements essentially unique
* i.e. no longer non-disjoint sets
* the union of these then pairwise disjoint sets
* is referred to as a "disjoint union"

<!-- ======================================================================= -->
## wikipedia, partition of a set

* group all elements in X into a set of non-empty subsets P,
  such that every element is an element of exactly one subset
* setoid - a set equipped with an equivalence relation
* the sets in P are said to cover X
* rank of P - `(#X - #P)`, if X is finite
* a partition is a family of pairwise disjoint sets
* equivalence relation <=> partition of the set
* bell number Bn - number of partitions of an n-element set

refinement of partitions

* partition v of X is a refinement of partition w of X
* if every element of v is a subset of an element in w
* v is finer than w, w coarser than v, v is further fragmented than w
* (v <= w) - a finer-than relation on the set of partitions of X

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

(cancelled)
