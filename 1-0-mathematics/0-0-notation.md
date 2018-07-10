
<!-- ======================================================================= -->
# Notation

The main intention behind the following content is to provide an
overview of the notational style used throughout this repository.

<!-- ======================================================================= -->
## (=>, <=>, non-standard)

* (=>) and (<=>) are used to express "linguistic" or "logical" statements
* to express whether one object can be "transformed" into the other
* these "operators" need to be understood in a far less strict sense

implication (=>)

* (=>) is in general similar to (->)
* "a" can be transformed into "b"
* "b" can be derived from "a"
* "b" is a consequence of "a"
* "b" is a result of "a"
* "b" is subsequent to "a"
* one can transition from "a" to "b"

not a result of (=!>)

* used to point out that (->) is not true in general
* "a" can not be transformed into "b"
* "b" can not be derived from "a"
* "a" does not necessarily imply that "b" is also true

equivalence (<=>)

* (<=>) is in general similar to (<->)
* "a" and "b" can be transformed into each other
* one can transition back and forth

not "equivalent" (<=!=>)

* used to point out that (<->) is not true in general
* "a" and "b" can not be transformed into each other
* "a" can not be derived from "b", and "b" not from "a"
* "a" and "b" are not necessarily equivalent

<!-- ======================================================================= -->
## definition (:=)

* `a := b` means that `a` is defined to be equal to `b`
* synonymous - equal, same value, same meaning, same characteristics, identical
* i.e. `a` is said to be by definition equal to `b`

Note that, for clarification purposes, `a` may be redefined to be equal to `b`.
However, `a` can not be redefined to be un-equal to its initial definition.

multi-definition

* `a := b := c` (in short `a, b := c`)
  means that `b` is by definition equal to `c`
  and `a` is by definition equal to `b`
* consequently, `a` is by definition equal to `c`
* multiple definitions in one row are transitive -
  i.e. `(a := b := c)` => `((a := b) and (b := c))` => `(a := c)`
* `(a,b := c)` <=> `(b,a := c)`

definition (:=, if)

* `a := b`, (`if` -or- `for`) `<condition>`
* `a` is defined to be equal to `b` if, and only if, certain conditions hold
* `a` is undefined, if the specified condition does not hold
* e.g. `a := i`, if `i in [1,N]`

<!-- ======================================================================= -->
## assignment (=)

* `a = b` means that the value of `b` is assigned to `a`
* `a` may be re-assigned to a different value (e.g. `a = c`)

<!-- ======================================================================= -->
## equal by value (=, ==)

* whenever sensible, (==) should be used rather than (=)
* `(a == b), (a equal-to b)` := true if `a` and `b` hold the same value
* `true` if both values are equal, `false` otherwise
* `(a == b)` is in general `true`, if such an expression
  is subsequent to one of the following two expressions: `a = b` or `a := b`
* `(a == b) <-> (b == a)`

clarification (==, if)

* `(a == b)`, (`if` -or- `for`) `<condition>`
* this pattern is used to clarify that `(a == b)` is true,
  if the specified condition is true
* e.g. `(a == 2)`, if `a` evaluates to `2`

<!-- ======================================================================= -->
## unequal by value (!=)

* `(a != b), (a unequal-to b) := not (a == b)`
* true if `a` and `b` do not hold the same value
* `(a != b) <-> (b != a)`

clarification (!=, if)

* `(a != b)`, (`if` -or- `for`) `<condition>`
* this pattern is used to clarify that `(a != b)` is true,
  if the specified condition is true
* e.g. `(a != 0)`, if `a` evaluates to anything but `0`

<!-- ======================================================================= -->
## addressOf()

* `addressOf(a)` := a number value that is globally unique
  to the entity that is referenced by reference `a`
* if `(addressOf(a) == addressOf(b))` is true,
  then, apart from having different labels,
  `a` can not be distinguished from `b`
* this pattern is used in combination with distinct entities

<!-- ======================================================================= -->
## equal by reference (===)

* `(a === b), (a identical-to b) := (addressOf(a) == addressOf(b))`
* `true` if `a` is identical to `b`, `false` otherwise
* `(a === b)` is true if and only if `a` can not be distinguished from `b`

clarification

* (===) will be used to stress that no distinction is possible
* it must not be possible to tell the operands apart

clarification

* `(a === b) <-> (b === a)`
* `(a !== b) <-> (b !== a)`

clarification

* `(a === b) -> (a == b)`
* but not necessarily vice versa

<!-- ======================================================================= -->
## unequal by reference (!==)

* `(a !== b) := not (a === b)`
* `true` if `a` is not identical to `b`, `false` otherwise

clarification

* `(a != b) -> (a !== b)`
* but not necessarily vice versa

<!-- ======================================================================= -->
## (n in N), (n !in N)

* `n in N` is true, if `n` is an element of `N`
* `(n !in N), (n not in N) := not (n in N)`

clarification

* the `in` operator merely tests that `n` is an element of `N`
* the `in` operator can not determine if `N` contains `n` multiple times
* `N` appears as if it contains each value no more than once

<!-- ======================================================================= -->
## informal definitions

* `-Inf, -Infinity` := negative infinity
* `+Inf, +Infinity` := positive infinity

synonyms, groups

* frequently, names or identifiers are grouped together using (/)
* "name1/name2" may be used to express that ...
* 1) "name1" and "name2" are understood to be synonymous
* 2) the context in which such a pattern is used applies to all names

labels/indexes

* `l:a`:= entity `a` can be referred to by using the specified label `l`
* `a:i, ai` := some value `a` that corresponds with index/identifier `i`

number intervals/ranges

* `[a,*] := [a,+Inf)`, likewise `[*,b] := (-Inf,b]`
* `i in [a,*]` := value `i` may have any value from `a` to `+Infinity`

regular expression like patterns

* `<e>{a,b}` := expression `<e>` repeated `a` to `b` times, for `[a,b] in [0,*]`
* `<e>{a,*}` := `<e>` may appear `[a,+Inf)` times
* `<e>{0,1}, <e>{?}` := `<e>` may appear once, or not at all
* `<e>{0,*}, <e>{*}` := `<e>` may appear `i` times, for `i in [0,+Inf]`
* `<e>{1,*}, <e>{+}` := `<e>` may appear `i` times, for `i in [1,+Inf]`
* `<e>{a,a}, <e>{a}` := `<e>` must appear exactly `a` times
* `<e>{1}, <e>{1,1}` := `<e>`
