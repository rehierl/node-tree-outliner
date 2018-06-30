
<!-- ======================================================================= -->
# Multi-set (ms)

* values may be grouped into multisets of values
* synonymous - group, collection, etc.

`ms1 := < v1, v2, v1 >`

* each value may appear multiple times within a multiset
* each distinct value is referred to as a distinct element
* the multiplicity of `v1` is `2` because `v1` appears twice within `ms1`
* the number of distinct elements in `ms1` is 2 - referred to as "size"
* the total number of elements in `ms1` is 3 - referred to as "length"

`ms2 := < v1, v1, v2 >`

* `(ms2 == ms1)` => `ms1` is considered to be identical to `ms2`
* same distinct elements, same multiplicity per element
* the order of elements within a multiset has no meaning
* a multiset has no inner positions or indexes
* `ms2(3)` and `ms2[3]` are both undefined - syntax errors

clarification

* `ms3 := < ms1, ms2 >`
* multisets are values

clarification

* in general, `{` and `}` are used to group the components of a multiset
* in order to distinguish a multiset from a set, `[` and `]` may be used
* `[` and `]` could be confused with arrays
* `(` and `)` could be confused with sequences
* vectors aren't subject of this discussion
* which is why `<` and `>` seem unique enough to avoid such issues

<!-- ======================================================================= -->
## cardinality

* the cardinality of `ms1` is 3
* the cardinality of a multiset is
  the total number of its elements/components
* the cardinality of a multiset is the sum of
  the multiplicity of each distinct element

length, size

* `sizeOf(ms) <= lengthOf(ms)`
* "size" could be used to refer to the number of distinct elements
* "size" implies a set-based view on a multiset
* "length" could be used to refer to the total number of elements
* "length" implies a sequence-based view on a mutliset

element, component

* "component" could be used as counterpart to "distinct element"
* `ms1` has 3 components, but only 2 (distinct) elements

<!-- ======================================================================= -->
## labels

`ms1 := < a:v1, b:v2, c:v1 >`

* labels are not part of a multiset, they don't allow to access a component
* labels act as a visual aid and are intended to support discussions
* a multiset is still not a dictionary

clarification

* labels `a` to `c` allow to refer to a specific component
* labels are not limited to letters, any identifier can be used
* if numbers are used, they act as id values, not as indexes
