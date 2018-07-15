
<!-- ======================================================================= -->
# A multiset of values (ms)

* values may be grouped into multisets of values
* synonymous - group, collection, etc.
* multisets are complex values

`ms1 := < v1, v2, v1 >`

* each value may appear multiple times within a multiset
* the **multiplicity of** `v1` is `2` because `v1` appears twice within `ms1`
* the number of distinct values in a multiset is its **size**

`ms1 := < e1:v1, e2:v2, e3:v1 >`

* a multiset can be understood to hold one element/slot per value
* the number of elements in a multiset is its **cardinality/length**
* the elements within a multiset have no order - no first/last element/value
* any element may hold the value of another element
* i.e. a `1:N` relationship between values and elements
* `(vi != vj) -> (ei !== ej)`

`ms2 := < e1:v1, e2:v1, e3:v2 >`

* `(ms2 == ms1)` => `ms1` is considered to be identical to `ms2`
* same distinct values, same multiplicity per value

clarification

* `ms3 := < ms1, ms2 >`
* multisets are themselves values

clarification

* in general, `{` and `}` are used to group the values in a multiset
* this pair might be misleading - simple sets hold distinct values only
* `[` and `]` could be confused with arrays
* `(` and `)` could be confused with sequences
* both of these pairs imply some order of elements
* `<` and `>` seem unique enough to avoid such issues
* that is because vectors aren't subject of this discussion

<!-- ======================================================================= -->
## cardinality

* the cardinality of a multiset is
  the number of its elements/components
* the cardinality of a multiset is the sum of
  the multiplicity of each distinct value
* the cardinality of `ms1` is 3

length, size

* `sizeOf(ms) <= lengthOf(ms)`
* "size" could be used to refer to the number of distinct elements
* "size" implies a set-based view on a multiset
* "length" could be used to refer to the overall number of elements
* "length" implies a sequence-based view on a mutliset

element, component

* elements is in general referred to as a "components"
* `ms1` has 3 components, but only 2 distinct values

<!-- ======================================================================= -->
## labels

`ms1 := < a:v1, b:v2, c:v1 >`

* labels are not part of a multiset, they don't allow to access a component
* labels act as a visual aid and are intended to support discussions

clarification

* a multiset is still not a dictionary
* i.e. it is not possible to retrieve the element/value associated with a label

clarification

* labels `a` to `c` allow to refer to a specific component
* labels are not limited to letters, any identifier can be used
* if numbers are used, they act as id values, not as indexes
