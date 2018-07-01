
<!-- ======================================================================= -->
# Values v

* a value `v` (or a constant `c`) represents a specific abstract value
* such values need to be seen to be atomic - i.e. self-enclosed units
* `v` can not be changed to represent a different value
* i.e. a `1:1` relationship between a value and its representative
* e.g. the digit literal `2` represents the number `2`

number identifiers

* `v2, v:2` := some value `v` identified by value `2`
* multiple values can be distinguished by number identifiers
* `v1` and `v2` always represent different specific values

letter identifiers

* `vi, v:i` := some value `v` identified by `i in [1,N]`
* number ids may be generalized into letter ids
* `vi` represents one of the available values
* e.g. `(vi == v2)` for `i = 2`

clarification

* `vi` is constant, `vi` can not be changed, `vi` is immutable
* `vi` is not a variable, `vi` does not represent some reference
* it is an error to attempt to assign any value to `vi` - e.g. `vi = 2`

clarification

* `(v3 == v3)` and `(vi == vi)` are always true
* `(vi == vj)` is true if `(i == j)` and false if `(i != j)`
* different identifiers always refer to different specific values
