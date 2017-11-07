
# Values and Variables

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
* any set of values is itself a value -
  e.g. `V3 := { V1, V2 }`, `V4 := { V3 }`, `v1 := V3`

### iteration

```
for v in V begin
  //- do something
end
```

* any set of values allows to visit each of its values
* however, any iteration may visit the values in any order!
* synonymous - iterate, visit

### size of V

```
sizeOf(set) begin
  size = 0
  for v in set begin
    size = size + 1
  end if
  return size
end
```

* `#V, #(V) := sizeOf(V)`
* the size of a set is the number of values it contains
* signature - (set) -> number `n in [0,*]`

### V contains v

```
contains(set, value) begin
  for v in set begin
    if(v == value) return true
  end
  return false
end
```

* `(V contains v) := (contains(V, v) == true)`
* set `V` contains `v`, if `v` is an element of `V`
* signature - (set, value) -> boolean

V does not contain v

* `(V !contains v), (V not contains v) := (contains(V,v) == false)`
* set `V` does not contain `v`, if `v` is not an element of `V`

### v in V, v belongs to V

* `(v in V) := (V contains v)`
* `v` belongs to `V`, if `v` is an element of `V`
* `(v !in V), (v not in V) := (V !contains v)`
* `v` does not belong to `V`, if `v` is not an element of `V`
* synonymous - in, belongs to, element of
* i.e. `(v element-of V), (v belongs-to V) := (v in V)`
* signature - (value, set) -> boolean

clarification

* different sets of values may contain the same value
* `v1 in V1` and `v1 in V2` may be true at the same time
* however, `v2 !in V2` may also be true
* `(v in V) <=> (V contains v)`

### V subset-of W

```
subsetOf(set1, set2) begin
  for v in set1 begin
    if(v !in set2) return false
  end
  return true
end
```

* `(V subset-of W) := (subsetOf(V,W) == true)`
* set `V` is a subset of set `W`, if `v in W` for any `v in V`
* signature - (set,set) -> boolean

clarification

* `(V subset-of W) <!> (W subset-of V)`

### V is equal to W

* `(V == W) := (subsetOf(V,W) and subsetOf(W,V))`
* any value `v in V` also belongs to `W`, and
  any value `w in W` also belongs to `V`
* `(V equal-to W) := (V == W)`
* signature - (set,set) -> boolean
* `V` and `W` are equal, if `(V == W)`
* `V` and `W` have same size and values

V is unequal to W

* `(V != W) := not (V == W)`
* `V` and `W` are different in size and/or values

clarification

* `(V == W) <=> (W == V)`, and `(V != W) <=> (W != V)`
* `(V == W) => (#V == #W)`, but `(#V == #W) !> (V == W)`

### V in W, W contains V

```
contains(set1, set2) begin
  for v in set1 begin
    if(v == set2) return true
  end
  return false
end
```

* any set is itself a value
* `(W in V), (V contains W) := (contains(V,W) == true)`
* set `V` contains set `W` as an element, if `W` is an element of `V`
* set `V` is a set of set values

clarification

* `subset-of <!> element-of`
