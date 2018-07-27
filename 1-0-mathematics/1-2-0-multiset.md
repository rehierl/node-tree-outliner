
<!-- ======================================================================= -->
# A multiset of values (ms)

<!-- ======================================================================= -->
## core concept

* values may be grouped into multisets of values
* multisets are not paired with an order-relation
* synonymous - group, collection, etc.
* multisets are complex values

`ms1 := < v1, v2, v1 >`

* each value may appear multiple times within a multiset
* the "multiplicity" of `v1` is `2` because `v1` appears twice within `ms1`

`ms1 := < e1:v1, e2:v2, e3:v1 >`

* a multiset can be understood to hold one element/slot per value
* the number of elements in a multiset is referred to as "cardinality"
* the elements within a multiset have no order - i.e. no first/last element
* any element is allowed to hold the value of another element
* i.e. a `1:N` relationship between values and elements
* `(vi != vj) -> (ei !== ej)`, but not vice versa

`ms2 := < e1:v1, e2:v1, e3:v2 >`

* `(ms2 == ms1)` => `ms1` is considered to be equal to `ms2`
* i.e. both have the same distinct values, and the same multiplicity per value

definition

* `V := < vi | (vi holds an odd integer) >`
* instead of listing each value, multisets can be defined by
  specifying a condition that must be satisfied by each value
* alternative notations - `<:>`, `<;>`, `<,>`, etc.

<!-- ======================================================================= -->
## which characters to use?

* in general, `{` and `}` are used to group values into multisets
* this pair of characters is however misleading as they are also used for sets
* however, in contrary to multisets, simple sets hold distinct values only
* `[` and `]` could be confused with arrays
* `(` and `)` could be confused with sequences
* both of these pairs imply some element order
* `<` and `>` seem unique enough to avoid such issues
* note that vectors aren't subject of this discussion

<!-- ======================================================================= -->
## cardinality

* the cardinality of a multiset is
  the total number of its elements
* the cardinality of a multiset is the sum over
  the multiplicities of each distinct value

element, component

* elements are in general referred to as "components"
* `ms1` has 3 components, but only 2 distinct values

Note that the "cardinality" of a complex value is in general understood to
refer to the number of elements it needs to hold its values.

<!-- ======================================================================= -->
## size, length

sizeOf(ms)

* "size" will be used to refer to the number of distinct values
* i.e. "size" reflects a set-based perspective on a multiset

lengthOf(ms), cardinalityOf(ms)

* "length" will be used to refer to the number of elements
* i.e. "length" is understood to be synonymous to "cardinality"
* i.e. "length" reflects a sequence-based perspective on a mutliset
* i.e. "length" is not understood to imply any order

clarification

* `(sizeOf(ms) <= lengthOf(ms))`
* `(lengthOf(ms) == cardinalityOf(ms))`

<!-- ======================================================================= -->
## labels

`ms1 := < a:v1, b:v2, c:v1 >`

* labels are not part of a multiset, they don't allow to access a component
* labels act as a visual aid and are intended to support discussions
* i.e. it is not possible to retrieve the element/value associated with a label
* i.e. a multiset is still not a dictionary

clarification

* labels `a` to `c` allow to refer to a specific component
* labels are not limited to letters, any identifier can be used
* if numbers are used, they act as id values, not as indexes

<!-- ======================================================================= -->
## multiset-of

a homogenous multiset of values

* `V1 := < 1, 2, 3 >`
* `V2 := < 'a', 'b', 'c' >`
* a multiset may only contain values that have similar characteristics
* `isHomogenous(V)`, `isHom(V)` := true, if `V` is a homogenous multiset

a heterogenous multiset of values

* `V3 := < 1, 2.0, 0xab, 'a' >`
* `V4 := < 1, 2.0, 0xab, 'a', "abc", {5} >`
* a multiset may contain values that have distinct characteristics
* `isHeterogenous(V) := not isHom(V)`

a multiset of X

* `V := < vi | isX(vi) >`
* all values `(vi in V)` have characteristic `X`
* e.g. a multiset of numbers, characters, sets, etc.

a multiset of atomic values

* `V := < vi | isAtomic(vi) >`
* `V` contains primitive values only
* no `vi` is complex - no strings, no sets, etc.
* however, `V` is itself still a complex value
* a set of atomic values is not necessarily homogenous

<!-- ======================================================================= -->
## is-multiset

* `isMultiSet(ms)` returns `true`, if value `ms` is a multiset of values
* i.e. `true` if `ms` has the characteristics of a multiset
* `(is-multiset ms) := isMultiSet(ms)`

<!-- ======================================================================= -->
## cardinality

* `#V, #(V)` := the number of elements in multiset `V`
* `(cardinality-of V), cardinalityOf(V) := #V`

<!-- ======================================================================= -->
## is-empty

* `(is-empty V), isEmpty(V) := (#V == 0)`
* `<>` represents an empty multiset
* `(#<> == 0)` is always true
* `(V == <>) <-> (#V == 0)`

<!-- ======================================================================= -->
## (random) iteration

```
traceOf(multiset) begin
  seq = new sequence()
  for e in multiset begin
    seq.add(e.value)
  end
  return seq
end

s = < 1, 2, 2, 3 >
s1 = traceOf(s) //- e.g. [ 2, 1, 3, 2 ]
s2 = traceOf(s) //- e.g. [ 3, 2, 1, 2 ]
```

* any multiset of values allows iterate over its elements
* an iteration may visit the elements in any order
* subsequent iterations may visit the elements in different order
* i.e. `s1` is not guaranteed to be identical to `s2`
* synonymous - iterate, visit

<!-- ======================================================================= -->
## multiplicity-of

```
multiplicityOf(x,V) begin
  result = 0
  for e in V begin
    if(e.value == x) begin
      result = result + 1
    end
  end
  return result
end
```

That is, multiplicityOf() returns the number of occurrences of `x` in `V`.
The result will be `0` if `(x !in V)`.

<!-- ======================================================================= -->
## (v in V), element-of

(v in V)

* `(v in V)` := `(multiplicityOf(v,V) >= 1)`
* `(v element-of V), elementOf(v,V) := (v in V)`
* `(V contains v), (v belongs-to V) := (v in V)`

(V in W)

* any multiset is itself a value
* `(V in W)` := `(multiplicityOf(V,W) >= 1)`
* `(W contains V), (V belongs-to W), (V element-of W) := (V in W)`

<!-- ======================================================================= -->
## add, remove

add(x,V)

* `add(x,V)` := increase the multiplicity of `x` in `V` by `1`
* i.e. `V` and `add(x,V)` will only differ in multiplicity of `x`
* i.e. `multiplicityOf(x,add(x,V)) == multiplicityOf(x,V)+1`
* signature: (value,multiset) -> new-multiset

remove(x,V)

* `remove(x,V)` := decrease the multiplicity of `x` in `V` by `1`
* i.e. `V` and `remove(x,V)` will only differ in multiplicity of `x`
* `(V == remove(x,V))` will be true iff `(x !in V)`
* i.e. the multiplicity of `x` can not be reduced beyond `0`
* signature: (value,multiset) -> new-multiset

<!-- ======================================================================= -->
## one-element-of

* `oneElementOf(V)` := a random element of the given multiset

clarification

* the element returned remains to be an element of the set - i.e. not removed
* each element is returned with equal chance - i.e. `1/#V`
* i.e. subsequent calls will result in different elements being returned

Recall that elements can not be accessed directly.
That is, any access to an element will access the value it holds.

Note that this operation is most useful in combination with multisets that
have cardinality one/1. This operation allows to consistently retrieve the
single element/value it holds.
