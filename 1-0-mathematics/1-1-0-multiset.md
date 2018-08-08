
<!-- ======================================================================= -->
# A multiset of values (ms)

```
multisets
-------------
order:  none

slots:  c1 c2
        | /
values: v1
```

<!-- ======================================================================= -->
## core concept

* values may be grouped into multisets of values
* multisets are not paired with an order-relation
* i.e. there is no order on the underlying set of components
* synonymous - group, collection, etc.
* multisets are complex values

`ms1 := < c1:v1, c2:v2, c3:v1 >` or short `< v1, v2, v1 >`

* a multiset holds one component per value
* the number of components in a multiset is referred to as its "cardinality"
* the components within a multiset have no order - i.e. no first/last component
* a component is allowed to hold the value of another component
* i.e. different components may hold identical values
* i.e. a `1:N` relationship between values and components
* the "multiplicity" of `v1` is `2` because `v1` appears twice within `ms1`
* `(vi != vj) -> (ci !== cj)`, but not vice versa

`ms2 := < e1:v1, e2:v1, e3:v2 >` or short `< v1, v1, v2 >`

* `(ms2 == ms1)` => `ms1` is considered to be equal to `ms2`
* i.e. both have the same distinct values, and the same multiplicity per value

definition

* `V := < vi | (vi holds an odd integer) >`
* instead of listing each value, multisets may be defined by
  specifying a condition that must be satisfied by each value
* alternative notations - `<:>`, `<;>`, `<,>`, etc.
* i.e. a set-builder-like notation

<!-- ======================================================================= -->
## which characters to use?

* in general, `{` and `}` are used to group values into multisets
* this pair of characters is however misleading as they are also used for sets
* however, in contrary to multisets, simple sets hold distinct values only
* `(` and `)` could be confused with sequences
* `[` and `]` could be confused with arrays/sequences
* both of these pairs imply some order of components
* `<` and `>` seem unique enough to avoid such issues
* note - vectors aren't subject of this discussion

<!-- ======================================================================= -->
## cardinality

* the cardinality of a multiset is equal to
  the sum over the multiplicities of its distinct values
* `ms1` has cardinality 3, but only 2 distinct elements

<!-- ======================================================================= -->
## size, length

sizeOf(ms)

* "size" will be used to refer to the number of distinct values
* i.e. "size" reflects a set-based perspective on a multiset

lengthOf(ms), cardinalityOf(ms)

* "length" will be used to refer to the number of components
* i.e. "length" is understood to be synonymous to "cardinality"
* i.e. "length" reflects a sequence-based perspective of a mutliset
* i.e. "length" is not understood to imply any order

clarification

* `(sizeOf(ms) <= lengthOf(ms))`
* `(lengthOf(ms) == cardinalityOf(ms))`

<!-- ======================================================================= -->
## labels

`ms1 := < a:v1, b:v2, c:v1 >`

* labels are not part of a multiset, they don't allow to access a component
* labels act as a visual aid and are intended to support discussions
* i.e. it is not possible to retrieve the component associated with a label
* i.e. a multiset is no dictionary

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
  for c in multiset begin
    seq.add(c.value)
  end
  return seq
end

s = < 1, 2, 2, 3 >
s1 = traceOf(s) //- e.g. [ 2, 1, 3, 2 ]
s2 = traceOf(s) //- e.g. [ 3, 2, 1, 2 ]
```

* any multiset of values allows to randomly iterate over its components
* an iteration may visit the components in any order
* subsequent iterations may visit the components in different order
* i.e. `s1` is not guaranteed to be identical to `s2`
* synonymous - iterate, visit

<!-- ======================================================================= -->
## multiplicity-of

```
multiplicityOf(x,V) begin
  result = 0
  for c in V begin
    if(c.value == x) begin
      result = result + 1
    end
  end
  return result
end
```

* multiplicityOf() returns the number of occurrences of `x` in `V`
* the result is `0` if no component holds `x` as its value

<!-- ======================================================================= -->
## (v in V), element-of

(v in V)

* `(v in V) := (multiplicityOf(v,V) >= 1)`
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
* i.e. subsequent calls may result in different elements being returned

Note that this operation is useful in combination with multisets that have
cardinality one/1. This operation allows to consistently retrieve the single
element/value it holds.
