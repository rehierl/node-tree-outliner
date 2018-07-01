
<!-- ======================================================================= -->
# TODOs

* definition - consecutive
* similar to - consecutive numbering

clarification

* `dom(ei) := Vi` - any element in a sequence has its own domain
* different elements may belong to the same, or to different domains
* e.g. `V2 := V1` is allowed, as is `(e2 == e1)`

subsequences

* range vs. sub-range
* string vs. sub-string

(ordered) sets

* unique/distinct elements in sequences
* ordered according to the elements of a set

<!-- ======================================================================= -->

```
a b | !a !b | a and b | !(a and b) | !a or !b |
----|-------|---------|------------|----------|-
0 0 |  1  1 | 0       | 0 | 1      | 1 1 | 1  |
0 1 |  1  0 | 0       | 0 | 1      | 1 0 | 1  |
1 0 |  0  1 | 0       | 0 | 1      | 0 1 | 1  |
1 1 |  0  0 | 1       | 1 | 0      | 0 0 | 0  |
```

* `!(a and b) <-> (!a or !b)`

<!-- ======================================================================= -->
notes on (->)

* `(a or b) <-> (!a -> b)`
* `(!a or !b) <-> (a -> !b)`
* `(a and !b) <-> !(a -> b)`

<!-- ======================================================================= -->
notes on (<->)

```
a b | !a !b | !a <-> b |
----|-------|----------|-
0 0 |  1  1 | 1 0 | 0  |
0 1 |  1  0 | 1 1 | 1  |
1 0 |  0  1 | 0 0 | 1  |
1 1 |  0  0 | 0 1 | 0  |
```

* `(!a <-> b) <-> (a xor b)`
* `!(a xor b) <-> (a <-> b)`
