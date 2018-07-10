
<!-- ======================================================================= -->
# Logic

<!-- ======================================================================= -->
## not, or, and

```
a b | not a | a or b | a and b |
----|-------|--------|---------|-
0 0 | 1     | 0      | 0       |
0 1 | 1     | 1      | 0       |
1 0 | 0     | 1      | 0       |
1 1 | 0     | 1      | 1       |
```

* `!a := (not a)` - negation
* `(a & b) := (a and b)` - conjunction
* `(a | b) := (a or b)` - disjunction

```
a b | a not b |
----|---------|-
0 0 | 0 1 | 0 |
0 1 | 0 0 | 0 |
1 0 | 1 1 | 1 |
1 1 | 1 0 | 0 |
```

* `(a ! b), (a not b) := (a and !b)`
* in set-based speech, (a not b) is equivalent to (A \ B)

<!-- ======================================================================= -->
## xor, xnor

```
a b | a xor b | a xnor b |
----|---------|----------|-
0 0 | 0 1 | 0 | 0 1 | 1  |
0 1 | 1 1 | 1 | 0 0 | 0  |
1 0 | 1 1 | 1 | 1 1 | 0  |
1 1 | 1 0 | 0 | 1 0 | 1  |
```

xor

* `(a xor b) := (a not b) or (b not a)`
* `(a xor b) := (a or b) and !(a and b)`
* `(a ^ b), (a ex-or b) := (a xor b)`
* in set-based speech, (a xor b) is equivalent to (A\B or B\A)

xnor, xand

* `(a xnor b) := !(a xor b)`
* `(a xnor b) := (a xor !b)`
* `(a xand b) := (a xnor b)`

<!-- ======================================================================= -->
## (->, <->)

```
a b | !a !b | a -> b  | b -> a  | a <-> b | b <-> a |
----|-------|---------|---------|---------|---------|
0 0 |  1  1 | 1 0 | 1 | 1 0 | 1 | 0 0 | 1 | 0 0 | 1 |
0 1 |  1  0 | 1 1 | 1 | 0 0 | 0 | 0 1 | 0 | 1 0 | 0 |
1 0 |  0  1 | 0 0 | 0 | 1 1 | 1 | 1 0 | 0 | 0 1 | 0 |
1 1 |  0  0 | 0 1 | 1 | 0 1 | 1 | 1 1 | 1 | 1 1 | 1 |
```

clarification (->)

* `(a -> b) := (!a or b)`
* (->) - material conditional, only-if, if-then
* (if A then B) := (A -> B)
* note - `(a -> b)` is not commutative
* note - must flip the arguments and the arrow

clarification (<->)

* `(a <-> b) := (a and b) or (!a and !b)`
* (<->) - logical biconditional, if-and-only-if
* (A iff B), (A if and only if B) := (A <-> B)
* `(a <-> b)` is equivalent to `(b <-> a)` (commutative)
* `(a <-> b)` is equivalent to `(a -> b) and (b -> a)`

clarification

* signature - "(list of parameter types) -> result-type"
* (->) may be used in the specification of a function's signature

clarification

* the negation operator (!, see below) must not be used with these
  strict operators (i.e. not `<!-`, `-!>`, `<-!->`, etc)
* hint: no confusion with the lower-or-equal order operator (<=) possible

<!-- ======================================================================= -->
## notes on (->)

```
a b | !a !b | a -> b  |
----|-------|---------|
0 0 |  1  1 | 1 0 | 1 |
0 1 |  1  0 | 1 1 | 1 |
1 0 |  0  1 | 0 0 | 0 |
1 1 |  0  0 | 0 1 | 1 |
```

* `(a -> b) := (!a or b)`
* note - if A is true, then B must also be true
* note - if A is false, then B may have any value
* to poof `(a -> b)` - proof that `b` is always true if `a` is true.

```
a b | !a !b | a -> b  | !a -> b | a -> !b |
----|-------|---------|---------|---------|
0 0 |  1  1 | 1 0 | 1 | 1 0 | 0 | 0 1 | 1 |
0 1 |  1  0 | 1 1 | 1 | 1 1 | 1 | 0 0 | 1 |
1 0 |  0  1 | 0 0 | 0 | 0 0 | 1 | 1 1 | 1 |
1 1 |  0  0 | 0 1 | 1 | 0 1 | 1 | 1 0 | 0 |
```

* `!(a -> b) <-> (a and !b)`
* `(!a -> b) <-> (a or b)`
* `(a -> !b) <-> !(a and b) <-> (!a or !b)`

```
      |          | u :=    | v :=    | w :=    | x :=    | y :=    |
a b c | !a !b !c | a -> b  | b -> c  | a -> c  | v -> w  | u -> x  |
------|----------|---------|---------|---------|---------|---------|
0 0 0 |  1  1  1 | 1 0 | 1 | 1 0 | 1 | 1 0 | 1 | 0 1 | 1 | 0 1 | 1 |
0 1 0 |  1  0  1 | 1 1 | 1 | 0 0 | 0 | 1 0 | 1 | 1 1 | 1 | 0 1 | 1 |
1 0 0 |  0  1  1 | 0 0 | 0 | 1 0 | 1 | 0 0 | 0 | 0 0 | 0 | 1 0 | 1 |
1 1 0 |  0  0  1 | 0 1 | 1 | 0 0 | 0 | 0 0 | 0 | 1 0 | 1 | 0 1 | 1 |
------|----------|---------|---------|---------|---------|---------|
0 0 1 |  1  1  0 | 1 0 | 1 | 1 1 | 1 | 1 1 | 1 | 0 1 | 1 | 0 1 | 1 |
0 1 1 |  1  0  0 | 1 1 | 1 | 0 1 | 1 | 1 1 | 1 | 0 1 | 1 | 0 1 | 1 |
1 0 1 |  0  1  0 | 0 0 | 0 | 1 1 | 1 | 0 1 | 1 | 0 1 | 1 | 1 1 | 1 |
1 1 1 |  0  0  0 | 0 1 | 1 | 0 1 | 1 | 0 1 | 1 | 0 1 | 1 | 0 1 | 1 |
```

* (->) not commutative, not associative, transitive
* (`((a -> b) -> c)` != `(a -> (b -> c))`) => not associative
* `(a -> b) -> ((b -> c) -> (a -> c))`
* `(a -> b) -> (v -> w)` => `(u -> x)` => true => transitive

note

* `((a and b) -> a)` - check
* `((a and b) -> b)` - check

<!-- ======================================================================= -->
## notes on (<->)

```
a b | !a !b | a -> b  | b -> a  | a <-> b |
----|-------|---------|---------|---------|
0 0 |  1  1 | 1 0 | 1 | 1 0 | 1 | 0 0 | 1 |
0 1 |  1  0 | 1 1 | 1 | 0 0 | 0 | 0 1 | 0 |
1 0 |  0  1 | 0 0 | 0 | 1 1 | 1 | 1 0 | 0 |
1 1 |  0  0 | 0 1 | 1 | 0 1 | 1 | 1 1 | 1 |
```

* `(a <-> b) := (a and b) or (!a and !b)`
* to proof `(a <-> b)` - proof that `a` and `b` always have the same value.
* `(a <-> b)` is equivalent to `(a -> b) and (b -> a)`
* to proof `(a <-> b)` - proof that `(a -> b)` and `(b -> a)` are both true.

consequently

* if `(a <-> b)` is true, then `(a -> b)` is also always true.
* if `(a <-> b)` is true, then `(b -> a)` is also always true.

```
a b | !a !b | a <-> b | !a <-> b | a <-> !b | !a <-> !b |
----|-------|---------|----------|----------|-----------|
0 0 |  1  1 | 0 0 | 1 | 1 0 | 0  | 0 1 | 0  | 1 1 | 1   |
0 1 |  1  0 | 0 1 | 0 | 1 1 | 1  | 0 0 | 1  | 1 0 | 0   |
1 0 |  0  1 | 1 0 | 0 | 0 0 | 1  | 1 1 | 1  | 0 1 | 0   |
1 1 |  0  0 | 1 1 | 1 | 0 1 | 0  | 1 0 | 0  | 0 0 | 1   |
```

* `(a <-> b) <-> (!a <-> !b) <-> !(a xor b) <-> (a xnor b)`
* `!(a <-> b) <-> (!a <-> b) <-> (a <-> !b) <-> (a xor b)`

```
      |          | u :=    | v :=    | w :=    | x :=    | y :=    |
a b c | !a !b !c | a <-> b | b <-> c | a <-> c | v <-> w | u <-> x |
------|----------|---------|---------|---------|---------|---------|
0 0 0 |  1  1  1 | 0 0 | 1 | 0 0 | 1 | 0 0 | 1 | 1 1 | 1 | 1 1 | 1 |
0 1 0 |  1  0  1 | 0 1 | 0 | 1 0 | 0 | 0 0 | 1 | 0 1 | 0 | 0 0 | 1 |
1 0 0 |  0  1  1 | 1 0 | 0 | 0 0 | 1 | 1 0 | 0 | 1 0 | 0 | 0 0 | 1 |
1 1 0 |  0  0  1 | 1 1 | 1 | 1 0 | 0 | 1 0 | 0 | 0 0 | 1 | 1 1 | 1 |
------|----------|---------|---------|---------|---------|---------|
0 0 1 |  1  1  0 | 0 0 | 1 | 0 1 | 0 | 0 1 | 0 | 0 0 | 1 | 1 1 | 1 |
0 1 1 |  1  0  0 | 0 1 | 0 | 1 1 | 1 | 0 1 | 0 | 1 0 | 0 | 0 0 | 1 |
1 0 1 |  0  1  0 | 1 0 | 0 | 0 1 | 0 | 1 1 | 1 | 0 1 | 0 | 0 0 | 1 |
1 1 1 |  0  0  0 | 1 1 | 1 | 1 1 | 1 | 1 1 | 1 | 1 1 | 1 | 1 1 | 1 |
```

* (<->) commutative, associative, transitive (?)
* (`((a <-> b) <-> c)` == `(a <-> (b <-> c))`) => associative
* `(a <-> b) <-> ((b <-> c) <-> (a <-> c))`
* `((a <-> b) <-> (a <-> c)) <-> (b <-> c)`
* `(a <-> b) <-> (v <-> w)` => `(u <-> x)` => true => transitive (?)
* `(a <-> b <-> c)` is ambiguous and should not be used

note

* `((a <-> b) and (a <-> c)) -> (b <-> c)` - check
* `((a <-> b) and (b <-> c)) -> (a <-> c)` - check
