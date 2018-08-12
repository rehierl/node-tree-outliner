
<!-- ======================================================================= -->
# (Set-like) Operations on groups

Note that the following definitions correspond with those defined for simple
sets of values. That is, the following definitions can be understood to be
generalization of the set-based operations and the set-based operations as
specializations.

The cardinality/multiplicity of a value, that is not an element of a group,
is zero/0. Because of that, set-like operations can be defined based on the
addition/subtraction of multiplicities.

* `#(x,V) = 0` if `(x !in V)`

extended set-builder-like notation

* `V := < x*n | (x in Integer) and (n = [0,2]) >`
* `x*n` - increase the multiplicity of element `x` by `(n in [0,*])`
* `x*0` - the "current run" has no effect on `#(x,V)`

<!-- ======================================================================= -->
## union (+, or, union)

* `(A union B) := < x*n | (n = #(x,A) + #(x,B)) >`
* `(A or B), (A + B) := (A union B)`

likewise

* `(A + b) := (A + < b >)`
* `(a + B) := (< a > + B)`
* `(a + b), (< a > + < b >) := < a, b >`

clarification

* `((A + B) + C) <-> (A + (B + C))`
* `((a + b) + c) <-> (a + (b + c))`

example

* `A := < 1, 2, 2 > and B := < 1, 2 >`
* `(A union B) = < 1, 1, 2, 2, 2 >`

<!-- ======================================================================= -->
## intersection (&, and, isect)

* `(A isect B) := < x*n | (n = min(#(x,A), #(x,B))) >`
* i.e. the minimum of the multiplicities in both groups
* `(A & B), (A and B) := (A isect B)`

example

* `A := < 1, 2, 2 > and B := < 1, 2 >`
* `(A and B) = < 1, 2 >`

<!-- ======================================================================= -->
## difference (\, sub, diff)

* `(A diff B) := < x*n | (n = max(0, (#(x,A) - #(x,B)) ) >`
* i.e. reduce the multiplicity in A by the multiplicity in B
* `(A \ B), (A sub B) := (A diff B)`

example

* `A := < 1, 2, 2 >` and `B := < 1, 2 >`
* `(A sub B) = < 2 >`

<!-- ======================================================================= -->
## symmetric difference (^, xor, ex-or)

* `(A ex-or B) := (A \ B) union (B \ A)`
* `(A ^ B), (A xor B) := (A ex-or B)`

clarification

* `(A xor B) := (A \ B) or (B \ A)`
* `(A xor B) := (A or B) \ (A & B)`

example

* `A := < 1, 2, 2 > and B := < 1, 2, 3 >`
* `(A xor B) = (< 2 > union < 3 >) = < 2, 3 >`

<!-- ======================================================================= -->
## complement (*)

Similar to simple sets, a universal group U could be defined, which would have
to contain any element with infinite multiplicity. Because of that, an absolute
complement can not be defined as the multiplicities within the resulting group
would be infinite (?). Because of that A* := (U \ A) would be equal to U,
regardless of what the contents of group A are.

However, a "relative complement" (i.e. U' \ A) may still be defined with regards
to some known finite and restricted universal group U'.
