
<!-- ======================================================================= -->
# Multiset ms

* values may be grouped into multisets of values
* aka. group, collection, etc.

clarification

* by default, `{` and `}` are used to group the components of a multiset
* in order to distinguish a multiset from a set, `[` and `]` may be used
* `[` and `]` however have the disadvantage that a multiset could be
  confused with a set or a sequence/array
* if `(` and `)` are used, then multisets could be confused with sequences
* vectors aren't subject of this discussion, which is why `<` and `>` seem
  unique enough to avoid any confusion

`ms1 := <v1,v2,v1>`

* each value may appear once or several times within a multiset
* each distinct value is referred to as a distinct element
* the multiplicity of `v1` is `2` because `v1` appears twice within `ms1`
* the number of distinct elements in `ms1` is 2
* the total number of elements in `ms1` is 3

`ms2 := <v1,v1,v2>`

* `(ms2 = ms1)` => `ms1` is considered to be identical to `ms2`
* the order of elements within a multiset has no meaning
* `ms2(3)` and `ms2[3]` are both undefined
* a multiset has no inner positions or indexes

cardinality

* the cardinality of `ms1` is 3
* the cardinality of a multiset is
  the total number of its elements
* the cardinality of a multiset is the sum of
  the multiplcities of its distinct elements

clarification

* `sizeOf(ms) <= lengthOf(ms)`
* "size" could be used to refer to the number of distinct elements
* "size" implies a set-based view on a multiset
* "length" could be used to refer to the total number of elements
* "length" implies a sequence-based view on a mutliset

clarification

* "component" could be used as counterpart to "distinct element"
* `ms1` has 3 components, but 2 (distinct) elements

labels, a visual aid

* `ms1 := < a:v1, b:v2, c:v1 >`
* labels `a` to `c` allow to refer to a specific component
* labels are not limited to letters
* anything that allows to identify a component can be used
* if numbers are used, they act as id values, not indexes
* labels are not part of a multiset, they can not be used to access a component
* a multiset is still not a dictionary
