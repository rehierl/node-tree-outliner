
<!-- ======================================================================= -->
# Notation

<!-- ======================================================================= -->
## assignment (=)

* `a = b` means that the value of `b` is assigned to `a`
* `a` may be re-assigned to a different value (e.g. `a = c`)

<!-- ======================================================================= -->
## definition (:=)

* `a := b` means that `a` is defined to be equal to `b`
* synonymous - equal, same value, same meaning, same characteristics
* for clarification purposes, `a` can be redefined to be equal to `b` -
  however, `a` cannot be redefined to be un-equal to its initial definition

multi-definition

* `a := b := c` (in short `a, b := c`)
  means that `b` is defined to be equal to `c`
  and `a` is defined to be equal to `b`
* as a result, `a` is also defined to be equal to `c`
* multiple definitions in one row are transitive -
  i.e. `(a := b := c) => (a := b and b := c) => (a := c)`
* `(a,b := c) <=> (b,a := c)`

definition (:=,if)

* `a := b`, (`if` -or- `for`) `<expression>{+}`
* `a` is defined to be equal to `b` if, and only if, certain conditions hold
* `a` is undefined, if one of the specified conditions does not hold
* e.g. `a := i`, if `i in [1,N]`

<!-- ======================================================================= -->
## fundamental definitions

* `-Inf, -Infinity` := negative infinity
* `+Inf, +Infinity` := positive infinity
* `a:i, ai` := some value `a` that corresponds with identifier `i`

number intervals

* `[a,*] := [a,+Inf)`, likewise `[*,b] := (-Inf,b]`
* `i in [a,*]` := value `i` may have any value from `a` to `Infinity`

regular expression like patterns

* `<e>{a,b}` := expression `<e>` repeated `a` to `b` times, for `[a,b] in [0,*]`
* `<e>{a,*}` := `<e>` may appear `[a,+Inf)` times
* `<e>{0,1}, <e>{?}` := `<e>` may appear once, or not at all
* `<e>{0,*}, <e>{*}` := `<e>` may appear `i` times, for `i in [0,+Inf]`
* `<e>{1,*}, <e>{+}` := `<e>` may appear `i` times, for `i in [1,+Inf]`
* `<e>{a,a}, <e>{a}` := `<e>` must appear exactly `a` times
* `<e>{1}, <e>{1,1} := <e>`

<!-- ======================================================================= -->
## equal by value (==)

* `(a == b), (a equal-to b)` := the values of `a` and `b` are tested for equality
* `true` if both values are equal, `false` otherwise
* signature - (anything, anything) -> boolean
* `(a == b)` is in general true, if `(a == b)` follows `a = b` or `a := b`
* e.g. `true` if `b = 3`, but `false` if `b := +Inf`
* `(a == b) <=> (b == a)`

clarification (==,if)

* `(a == b)`, (`if` -or- `for`) `<expression>{+}`
* this pattern is used to clarify that `(a == b)` is true,
  if the specified conditions are all true
* e.g. `(a == 2)`, if `a` evaluates to `2`

<!-- ======================================================================= -->
## unequal by value (!=)

* `(a != b), (a unequal-to b) := not (a == b)`
* references `a` and `b` are tested for in-equality by value
* `(a != b) <=> (b != a)`

clarification (!=,if)

* `(a != b)`, (`if` -or- `for`) `<expression>{+}`
* this pattern is used to clarify that `(a != b)` is true,
  if the specified conditions are all true
* e.g. `(a != 0)`, if `a in [1,+Inf]`

<!-- ======================================================================= -->
## equal by reference (===)

* `a === b, (a === b), (a identical-to b) := (addressOf(a) == addressOf(b))`
* the references of `a` and `b` are tested for equality
* `true` if `a` is identical to `b`, `false` otherwise
* `(a === b) <=> (b === a)`
* `(a !== b) <=> (b !== a)`

clarification

* equal by value => not necessarily also equal by reference

<!-- ======================================================================= -->
## unequal by reference (!==)

* `a !== b, (a !== b) := not (a === b)`
* `true` if `a` is not identical to `b`, `false` otherwise

clarification

* unequal by value => also unequal by reference

<!-- ======================================================================= -->
## (n in N), (n !in N)

* `n in N` is true, if `n` is an element of `N`
* `(n !in N), (n not in N) := not (n in N)`

clarification

* in general, a boolean operator may be prefixed with the negation operator
  to express an inverted statement
* e.g. `(V contains v)` => `(V !contains v)`

<!-- ======================================================================= -->
## equivalent - TODO

* `a <=> b`
* if `a` is true, then `b` is also true
* if `a` is not true, then `b` is also not true
* does not always mean, that both are strictly equivalent
* also used to clarify, that `a` and `b` have the same meaning
* `!<=>, <!> := not(<=>)`
* clarify that `a` and `b` do not have the same meaning

implication

* `a => b`
* if `a` is true, then `b` is also true
* if `a` is not true, then `b` may still be true
* also clarify, that `b` is derived from `a`
* `!=>, !> := not(=>)`
* clarify that `a` does not imply `b`

reversed implication

* `(a <= b) <=> (b => a)`
* `!<=, <! := not(<=)`