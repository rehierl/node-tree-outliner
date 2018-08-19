
<!-- ======================================================================= -->
# Sequences

* see "mathematics" for the core concept of sequences
* see "formal languages" for string-related aspects
* see "topology" for "every sequence is a net"

<!-- ======================================================================= -->
## Which term is appropriate?

* term "sequence" will be used in the course of this discussion
* in the course of this discussion, an "ordered sequence of nodes"

tuples

* `t := [1, 'a'] := (1,a)`
* an ordered list of "anything"
* in general of finite length

sequences

* `s := [1, 2, ...] := (1,2, ...)`
* an enumerated collection of "anything" of any length
* in general a rule exists such that subsequent elements
  in a sequence can be calculated from presequent ones
* e.g. `an := a(n-2) + a(n-1)` (Fibonacci)

strings

* `s := "abac..." := ['a', 'b', 'a', 'c', ...]`
* traditionally a sequence of characters
* elements are selected from an alphabet
* in computing generalized into a sequence of binary data
* depending on the context, a mutable/immutable sequence

vectors

* `v := [1.0, 2.0, 3.0] := < 1, 2, 3 >`
* in general an element of the real coordinate space (R^n)
