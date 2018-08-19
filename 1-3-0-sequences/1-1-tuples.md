
<!-- ======================================================================= -->
# Tuples, Sequences

<!-- ======================================================================= -->
## wikipedia, tuples

* a finite ordered list of elements
* n-tuple - a list of `n` elements, where `(n in [0,*])`
* 0-tuple - null-tuple, an empty list - i.e. `()`
* 1-tuple - singleton - i.e. `(a)`
* 2-tuple - ordered pair - i.e. `(a,b)`
* 3-tuple - triple, triplet - i.e. `(a,b,c)`
* used as an abstraction of sequences

definition

* `(a1,...,an) = (b1,...,bn)` iff `(ai=bi)` for any `(i in [1,n])`
* both tuples must have the same length - i.e. `n`
* `(ai = aj)` may be true for some `(i,j in [1,n])`
* `(a,b) != (b,a)` if `(a != b)` - i.e. ordered
* tuples always have finite length

tuples as functions

* domain X is the implicit set of element indexes
* codomain Y is the tuple's set of elements/values
* i.e. `(f: [1,*] -> Y)` - i.e. `t := (f(1),...,f(n))`

tuples as nested ordered pairs

* 0-tuple - `()` or `Ø`
* n-tuple - `t := (a1,...,((an-1),(an,{}))...)`
* n-tuple - `t := (...((Ø,a1),a2),...,an)`

tuples as nested sets

* Kuratowski's definition
* `(x -> y) := {{x},{x,y}}`
* 0-tuple - `()` => `Ø`
* 1-tuple - `(a)` => `(Ø -> a)` => `{{Ø},{Ø,a}}`
* 2-tuple - `(a,b)` => `{ (a), {(a),b} }`
* 2-tuple - `(a,b)` => `{ {{Ø},{Ø,a}}, { {{Ø},{Ø,a}}, b } }`
* 3-tuple - `(a,b,c)` => `{ (a,b), {(a,b),c} }`
* note - a linear subset-of relationship

implementations

* directly as (ordered) product types
* i.e. accessed by indexes
* alternatively as (unordered) record types
* i.e. accessed by labels

<!-- ======================================================================= -->
## wikipedia, unordered pair

* a (multi-)set of the form {a,b}
* i.e. no particular relation between (a) and (b)
* aka. 2-set, binary set, etc.
* aka. an unordered n-tuple
* i.e. {a1,a2,...,an}
* i.e. {a,b} == {b,a}

remarks

* unordered tuples - aka. multisets

<!-- ======================================================================= -->
## wikipedia, ordered pair

* a pair of objects in which the order of an object is significant
* i.e. has first and second/last element/component/coordinate
* `(a1,b1) = (a2,b2)` iff `(a1=a2)` and `(b1=b2)`
* (a,b) in (A × B) - Cartesian product
* several formal definitions possible
* e.g. Kuratowski's definition

<!-- ======================================================================= -->
## wikipedia, product type

* in programming languages and type theory
* a product of types is a compounded type in a structure
* multiple types -> compound/combined/complex/tuple type
* A × B × ... -> (A,B,...)
* i.e. retains the fixed order
* instances - (a,b,...)
* e.g. a vector in a vector space

<!-- ======================================================================= -->
## wikipedia, record type

* aka. record, structure, compound
* a collection of fields fixed in number and sequence
* fields "addressed" via labels - i.e. "unordered"
* a record type describes such compound values

<!-- ======================================================================= -->
## wikipedia, sequences

* aka. strings, words, lists, streams
* an enumerated collection of objects
* a sequence of members/elements/terms
* may appear multiple times at different positions - aka. repetitions
* length - the number of elements
* finite/infinite sequences - with regards to their length
* the empty sequence () may be excluded

formally defined as a function

* (f: Naturals -> Elements)
* domain - the index set holds rank/index values
* conventional aspect whether 0- or 1-based indexes are used

notation

* complete listing - e.g. (1,2,3)
* first few elements - e.g. (2,3,5,7,11,...)
* a formula to compute the n-th element - e.g. (2*n)
* sequence of sequences - ( ( ( a(m,n) )_n )_m)
* recursion - e.g. (an = a(n-1) + a(n-2))

properties

* (f: Integers -> Elements)
* domain - an interval of integers
* allows for bi-infinite sequences
* codomain - usually fixed by context
* f(1) -> 1st element, f(2) -> 2nd element, ...
* sequences and limits studied in topological spaces
* sequences generalized as nets
* net: a function from a directed set to a topological space

finite, infinite

* length of a sequence: the number of terms
* n-tuple: a finite sequence of length n
* infinite sequence: in general finite on one side, infinite on the other
* i.e. has a first but no final element
* aka. one-sided infinite sequence
* bi-infinite: neither a first, nor a final element
* aka. two-way infinite

increasing, decreasing

* monotonically increasing - each term is greater or equal to the one before it
* i.e. (an <= an+1) for all (n in Nat)
* (strictly) monotonically increasing (<=,<)
* (strictly) monotonically decreasing (>=,>)
* monotone sequence - either increasing or decreasing
* non-increasing - neither <= nor < - similarly non-decreasing
* may be more clear than (strictly) decreasing/increasing

bounded

* upper bound, bounded from above - (an <= m)
* lower bound, bounded from below - (an >= m)

**SKIPPED** - limits and convergence
**SKIPPED** - series - sum over all terms
**SKIPPED** - uses of sequences

<!-- ======================================================================= -->
## wikipedia, subsequences

* a sequence that can be derived from an initial sequence
* derived by the deletion/removal of elements - i.e. same order
* e.g. (t subsequence-of s), if t=[b,d] and s=[a,b,c,d,e]
* subsequence-of is a pre-order
* in contrary to that, substring-of does not support removal within an infix
* common subsequence - e.g. u=[b] is a common subsequence of s and t
* used in bio-informatics - e.g. compare/analyze/store protein sequences

<!-- ======================================================================= -->
## wikipedia, indexed family

* a collection/family of objects
* each object is associated with an index

definition

* (x: I -> X), index set I, element/indexed set X
* (xi) - a family of elements in X indexed by I
* x() - in general only surjective, not necessarily injective
* i.e. (xi = xj) is allowed for some (i != j)
* X := { xi | (i in I) } - the set/family of all objects
* note - (#X <= #I) - i.e. not necessarily (==)

functions, sets, families

* any function f with domain I induces a family (f(i))
* a family of objects is in general a collection - i.e. not a set
* a set iff f() is injective

subfamily

* (Bi) for (i in J) is a subfamily of (Ai) for (i in I)
* iff (J subset-of I) and (Bi = Ai) for all (i in J)
* note - B is not required to be 0/1-based

remarks

* a N×M matrix is indexed by tuples in (N × M)
* a net is a family indexed by a directed set
* diagrams - an analogous concept in category theory
