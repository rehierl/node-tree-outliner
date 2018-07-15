
<!-- ======================================================================= -->
# Values v

( The intention behind introducing "values" and their "representatives" is to
avoid thinking in terms of concrete values like numbers, characters, etc. )

`v := 2`

* a value `v` (or a constant `c`) represents some specific abstract value
* no representative `v` can be changed to represent a different value
* e.g. the literal `'2'` represents the abstract number value `2`
* i.e. a `1:1` relationship between a value and its representative

primitive values

* a primitive value is understood to be "atomic"
* i.e. a self-enclosed unit

number identifiers

* `v2, v:2` := some value `v` identified by number `2`
* multiple values can be distinguished by number identifiers
* `v1` and `v2` always represent different specific values
* `v1` and `v2` never hold the same abstract value

letter identifiers

* `vi, v:i` := some value `v` identified by `i in [1,N]`
* number ids may be generalized into letter identifiers
* `vi` represents one of the available values
* e.g. `(vi == v2)` for `i = 2`

clarification

* `vi` is constant, `vi` can not be changed, `vi` is immutable
* `vi` is not a variable, `vi` does not represent a reference of sorts
* it is an error to attempt to assign any value to `vi` - e.g. `vi = 2`

clarification

* `(v3 == v3)` and `(vi == vi)` are always true
* `(vi == vj)` is true if `(i == j)` and false if `(i != j)`
* different identifiers always refer to different specific values
