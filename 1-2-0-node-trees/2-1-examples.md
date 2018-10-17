
<!-- ======================================================================= -->
# Examples of tree operations

Some examples to illustrate operations on trees.

<!-- ======================================================================= -->
## implementation-specific remarks

An implementation could use null references to represent an empty graph/tree.

In contrary to that, and even though a tree represents a tree of trees (i.e.
`T[c]` for `(r root-of T)` and `(r parent-of c)`), a single tree can, from a
strict perspective, not represent a forest of trees. One would have to misuse
the tree's root (e.g. a root-id of `-1`) in order to indicate that a returned
tree is intended to represent a forest. However, that approach is error prone
as it requires implementations to always distinguish between the two cases
(i.e. is the result a tree or a forest?). Because of that, the focus is on
returning either an empty graph, or a single tree.

Note that, due to the above, the below examples consider a forest to represent
an undefined result (i.e. an error).

<!-- ======================================================================= -->
## union, examples

```
tree S        tree T        tree U
========      ========      =========
1 -|-> 2      2 -|-> 5      1 -|-> 2 -|-> 5
   |-> 3         |-> 6                |-> 6
                               |-> 3
```

* `U == (S + T) == unionOf(S,T)`

Note that, given the above trees, `(T + S)` could be considered to be undefined.
That is because the root of `S` (i.e. `1`) is not a node in `T`. Hence, and from
an implementation's perspective, the union operation is **not commutative**.

* `(S + T) <=!=> (T + S)`

Note that one could be tempted to first determine whose root is a node in the
other tree and then swap the trees accordingly.

```
tree S      tree T      tree U
======      ======      ======
1           1 -> 2      1 -> 2
```

In that case, `(S + T)` and `(T + S)` both result in `U`. The subtle difference
however is in the oder of operations: If `S` is understood to represent existing
content, then the addition of edge `(1,2)` by `(S + T)` could trigger an event
related to the addition of new content. In contrary to that, such an event must
not be triggered if `T` represents the existing content and if `(T + S)` needs
to be executed. That is, the union operation should not be treated as being
commutative even if `(S + T)` and `(T + S)` would yield the same tree.

```
tree S      tree T          tree U
========    ===========     =============
1 -|-> 2    1 -> 2 -> 4     1 -|-> 2 -> 4
   |-> 3                       |-> 3
```

Because `(S + T) == U == (T + U)`, the root of the 2nd tree does not
necessarily have to be a leaf in the 1st tree.

```
tree S     tree T      tree U      tree X       tree Y
======     ======      ======      ========     ========
1          1 -> 2      1 -> 3      1 -|-> 2     1 -|-> 3
                                      |-> 3        |-> 2
```

Given the above trees where `X := (S + T + U)` and `Y := (S + U + T)`, the
union operation can not be treated as being commutative, if the child order
of parent nodes is relevant. That is because both results are not equal
(i.e. `(X != Y)`)), if the child order is based upon the order of operations.

```
tree S       tree T     tree U      tree X
========     ======     ======      =============
1 -|-> 2     2 -> 4     3 -> 5      1 -|-> 2 -> 4
   |-> 3                               |-> 3 -> 5
```

Note that `X == (S + T + U) == (S + U + T)`. Because of that, the sequence
that defines the resulting tree is **not necessarily unique** to that tree.
Put differently, a tree may be the result of several distinct sequences.

```
tree T     tree U      forest Y
======     ======      ========
2 -> 4     3 -> 5      (2 -> 4), (3 -> 5)
```

Note that `Y == (T + U)` is a forest and therefore, from a strict perspective,
undefined. Consequently, `Z == (S + (T + U))` must also be understood represent
an undefined result.

The union operation is therefore **not associative** (i.e. due to `(X != Z)`).
Because of that, it is in general not possible to evaluate subexpressions
in parallel as subexpressions could turn out to be undefined. Consequently,
sequences of three or more trees must be evaluated from left-to-right.

* `(S + T + U) == ((S + T) + U) <=!=> (S + (T + U))`

Note that the order of operations in a complete left-to-right sequence has
in general a top-down, and then first-to-last order.

<!-- ======================================================================= -->
## difference, examples

```
tree S            tree T      (S \ T)    (T \ S)
===========       ======      =======    ========
1 -> 2 -> 3       2 -> 3      1          Ø
```

As mentioned before, this operation is by definition **not commutative**.

```
tree S            tree T     tree U    tree X    tree Y
===========       ======     ======    ======    ========
1 -|-> 2 -> 3     3          2         1 -> 4    1 -|-> 2
   |-> 4                                            |-> 4
```

From these examples, where `X := ((S \ T) \ U)` and `Y := (S \ (T \ U))` it
can be state that the difference operation is **not associative**. That is
because both expressions result in distinct trees. (Note that from a strict
perspective, `Y` could be considered to be undefined because the root of
`U` is not a node in `T`).

```
tree S          tree T     tree U
===========     ======     ======
1 -> 2 -> 3     2 -> 3     1
```

Here, `T` is a proper induced subtree of `S` (i.e. `(T == S[2])`).
Because of that, the result `U` is a single tree.

```
tree S       tree T     forest U
========     ======     ========
1 -|-> 2     1          2, 3
   |-> 3
```

Here, the root of `T` is equal to the root of `S` and that its only
leaf (i.e. node `1`) is no leaf in `S`. Hence, the result is a forest.

Note the special case that the result could still be a single tree,
if node `1` had only a single child in `S`.

```
tree S          tree T     forest U
===========     ======     ========
1 -> 2 -> 3     2          1, 3
```

Here, the root of `T` is neither equal to the root of `S`, nor is `T`
an induced subtree of `S`. The result is therefore a forest of trees.

Note that the above mentioned special case therefore also requires
that both root nodes must be equal (i.e. `(s == t)`).
