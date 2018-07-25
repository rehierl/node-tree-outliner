
<!-- ======================================================================= -->
# Remarks

<!-- ======================================================================= -->
## computer science vs. mathematics

* `a = v`, `b = v`, `x = (a === b)`
* variables `a` and `b` are both set to hold the abstract value `v`
* variable `x` holds the result of comparing `a` and `b` for identity

In principle, every abstract bit of information (aka. value, entity) is stored
at some specific location (aka. address). In general, the combination of a
value and its globally unique address will be referred to as an object.

Computer science can therefore in principle not support indistinguishable
entities. That is because two objects, set to represent the exact same abstract
entity, can always be distinguished from one another by their address. Hence,
and in computer science, `x` will always evaluate to `false`. In contrary to
that, mathematics has in general no concept of storage location. Because of
that, and in mathematics, `x` will always evaluate to `true`.

<!-- ======================================================================= -->
## sets of values

```
1: a = [v1], b = [v2]
2: c = {a, b}
3: b[1] = v1
4: d = (c == {[v1], [v1]})
```

From a technical perspective, the value of a storage location can be changed at
any point. Care must therefore be taken to not end up with a result that is in
conflict with abstract mathematical concepts. That is, after modifying sequence
`b`, the set of objects `c` no longer represents an abstract set of values; it
instead represents a multiset of values. Hence, computer science can only
simulate the abstract mathematical concept of sets of values.

Note that the implementation of a set of values is in fact closer to a set of
objects than a set of abstract values.

<!-- ======================================================================= -->
## ordered vs. unordered complex values

In general, no information can be written down without specifying some sort
of order. That is, because written information is based upon a sequence of
characters. Likewise, no computer-internal representation of a complex value
is completely without order; i.e. there always is a first/last bit of
information. Because of that, unordered complex values may appear to a
programmer as being "artificial" and ordered complex values as the more
"natural" concept.

However, from an abstract point of view, ordered complex values are the
artificial ones because further information is required that defines the
corresponding order.

One must therefore not confuse the order of sequentialized/stored information,
which can not be avoided, with the order of the members of some abstract
complex value. True unordered abstract values can therefore only be simulated.
