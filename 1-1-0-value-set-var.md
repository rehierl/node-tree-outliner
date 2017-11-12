
# Values and Elements

<!-- ======================================================================= -->
## Value v

* a value `v` (or a constant `c`) represents a specific value
* `v` can not be changed to represent a different specific value

number identifiers

* `v2, v:2` := some value `v` identified by value `2`
* multiple values can be distinguished by number identifiers
* `v1` and `v2` always represent different specific values

letter identifiers

* `vi, v:i` := some value `v` identified by `i in [1,N]`
* number ids may be generalized into letter ids
* `vi` represents one of the available values
* e.g. `(vi = v2)` for `i = 2`

clarification

* `vi` is constant, `vi` can not be changed, `vi` is immutable
* `vi` is not a variable, `vi` is not a reference of sorts
* it is an error to attempt to assign any value to `vi` - e.g. `vi = 2`

clarification

* `(v3 == v3)` and `(vi == vi)` are always true
* `(vi == vj)` is true if `(i == j)` and false if `(i != j)`
* different identifiers always refer to different specific values

<!-- ======================================================================= -->
## Set of values V

* different values may be grouped into a set of values -
  e.g. `V := {v1, v2}`
* the values of a set have no order -
  i.e. a set of values has no 1st, no last and no n-th value
* values may be grouped into different sets of values -
  e.g. `V := {v1, v2}`, `W := {v1, v3, v4}`
* sets of values may be identified by a number id -
  e.g. `V1 := V`, `V2 := W`
* similar to values, number ids may be generalized into letter ids -
  e.g. `Vi := V2` for `i = 2`

clarification

* adding or removing a value to or from a set results in a different set
* sets are constant/immutable, sets can not be changed, sets are not variable
* any set of values is itself a value - e.g. `V3 := { V1, V2 }`, `v1 := V3`

### is set

* `(is-set s), isSet(s)` is true, if `s` is a set of values
* i.e. `s` has the characterisitics of a set
* signature - (anything) -> boolean

### set of X

* in general, a set only contains values that have similar characteristics -
  e.g. `V5 := { 1, 2, 3 }`, `V6 := { 'a', 'b', 'c' }`
* however, a set may also consist of arbitrary selected values -
  e.g. `V7 := { 1, 2.0, 0xab, 'a', "abc", {5} }`
* a set-of-values - any `vi in V` is a primitive value - no string, no set
* a set-of-sets - any `si in S` is itself a set - this does not state what
  kind of set `si` is - `S` may contain sets that have any characteristics

### iteration

```
for v in V begin
  //- do something
end
```

* any set of values allows to visit each of its values
* however, any iteration may visit the values in any order!
* synonymous - iterate, visit

### size of V, cardinality

* `sizeOf(V)` returns the number of elements in `V`
* `#V, #(V), (size-of V), (cardinality-of V) := sizeOf(V)`
* signature - (set) -> number `n in [0,*]`

### n size of V

* `(n size-of V) := (n == sizeOf(V))`
* `(n cardinality-of V) := (n size-of V)`
* signature - (number,set) -> boolean

### is empty V

* `(is-empty V), isEmpty(V) := (#V == 0)`
* `{}` represents an empty set, i.e. `(#({}) == 0)`
* `isEmpty({})` is always true

### V contains v

* `contains(V,v)` is true, if `v` is an element of `V`
* `(V contains v) := (contains(V, v) == true)`
* set `V` contains `v`, if `v` is an element of `V`
* signature - (set, value) -> boolean

### (v in V), (v belongs to V)

* `(v in V) := (V contains v)`
* `(v element-of V), (v belongs-to V) := (v in V)`
* signature - (value, set) -> boolean

clarification

* different sets of values may contain the same value
* `v1 in V1` and `v1 in V2` may be true at the same time
* however, `v2 !in V2` may also be true -
  i.e. the indexes are independent from each other
* `(v in V) <=> (V contains v)`

### V is equal to W

* `(V == W) := (v in W, for any v in V) and (w in V, for any w in W)`
* `(V equal-to W) := (V == W)`
* signature - (set,set) -> boolean

(V == W)

* any value `v in V` also belongs to `W`, and
  any value `w in W` also belongs to `V`
* `V` and `W` are said to be equal
* `V` and `W` have same size and values

(V != W)

* both are different in size and/or values

clarification

* `(V == W) <=> (W == V)`, and `(V != W) <=> (W != V)`
* `(V == W) => (#V == #W)`, but `(#V == #W) !> (V == W)`

### V subset-of W

* `(V subset-of W) := (v in W for any v in V)`
* `subsetOf(V,W) := (V subset-of W)`
* set `V` is a subset of set `W`, if `v in W` for any `v in V`
* signature - (set,set) -> boolean

clarification

* `subset-of` is analogous to `<=`
* `(V subset-of W) => (#V <= #W)`
* `(V == W) := (subsetOf(V,W) and subsetOf(W,V))`
* `(V subset-of W) <!> (W subset-of V)`

### V strict-subset-of W

* `(V strict-subset-of W) := (V subset-of W), but (V != W)`
* a `w in W` exists such that `w !in V`
* signature - (set,set) -> boolean

clarification

* `strict-subset-of` is analogous to `<`
* `(V strict-subset-of W) => (#V < #W)`

### V contains W

* any set is itself a value
* `(W in V)` is true, if set `W` is an element of set `V`
* `(V contains W), contains(V,W) := (W in V)`
* `(W element-of V), elementOf(W,V) := (W in V)`
* signature - (set,set) -> boolean

clarification

* `subset-of <!> element-of`

<!-- ======================================================================= -->
## Union

* in this context, the addition of values if of no interest
* this allows to use the (+) operator as the union operator for sets

### (V + W)

* `(V + W) := { x, (x in V) or (x in W) }`
* `(V union W) := (V + W)`

clarification

* `((U + V) + W) <=> (U + (V + W))`

### (V + w)

* `(V + w) := (V + {w})`
* `(V union w) := (V + w)`

### (v + W)

* `(v + W) := ({v} + W)`
* `(v union W) := (v + W)`

### (v + w)

* `(v + w), ({v} + {w}) := {v, w}`
* `(v union w) := (v + w)`

clarification

* `((u + v) + w) <=> (u + (v + w))`

<!-- ======================================================================= -->
## Variables, Elements

* a variable `var` (aka. element `e`) represents some value `v`
* in contrary to values, the value of a variable may change over time

### value of e

* `e.value := v`, if value `v` was assigned to `e`
* `(value-of e), valueOf(e) := e.value`
* signature - (element) -> value

### v value of e

* `(e == v), (v value-of e) := (valueOf(e) == v)`
* `(ei == ej)`, if `(valueOf(ei) == valueOf(ej))`
* signature - (value,element) -> boolean

clarification

* `(ei == ei)` is always true
* different elements may represent the same value
* `(ei !== ej) !> (ei != ej)`, e.g. `(e1 == v) and (e2 == v)`
* different elements may represent different values
* two elements aren't necessarily identical, if they hold the same value
* `(ei == ej) !> (ei === ej)`, e.g. `(i != j)`
* an element can not represent different values at the same time
* `(ei != ej) => (ei !== ej)`, i.e. `(i != j)`, but not `<=`
* `(ei === ej) => (ei == ej)`, i.e. `(i == j)`

clarification

* an element can not store different values at the same time
* different elements are needed to store different values
* different elements may still represent the same value

### domain of, type of

* `e.domain := V`, if `e` may represent any value `v in V`
* `dom(e), domainOf(e), (domain-of e) := e.domain`
* `typeOf(e), (type-of e) := e.domain`
* the value `v` an element `e` may represent is limited to a set of values `V`
* signature - (element) -> set

clarification

* `domainOf(v) := { v }`
* a value can not represent any other value
* the domain of a value is essentially the value itself

### V domain of e

* `(V domain-of e), (V type-of e) := (e.domain == V)`
* `V` is said to be the domain or type of element `e`
* signature - (set,element) -> boolean
