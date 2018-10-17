
<!-- ======================================================================= -->
# Examples of tree operations

Some examples to illustrate operations on trees.

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
commutative even if `(S + T)` and `(T + S)` could result in the same tree.

```
tree S     tree T      tree U      tree X       tree Y
======     ======      ======      ========     ========
1          1 -> 2      1 -> 3      1 -|-> 2     1 -|-> 3
                                      |-> 3        |-> 2
```

Given the above trees, `X` is the result of `(S + T + U)` whereas `Y` is the
result of `(S + U + T)`. That is, if the child order of nodes is relevant, then
the union operation can not be treated as being commutative. That is because
both results can not be treated as being equal (i.e. `(X != Y)`)), if the child
order of each parent is based upon the order of operations.

```
tree S       tree T     tree U      tree V
========     ======     ======      ========
1 -|-> 2     2 -> 4     3 -> 5      1 -|-> 2 -> 4
   |-> 3                               |-> 3 -> 5
```

Note that `V == (S + T + U) == (S + U + T)`.

Even though any tree can be defined as a series of union operations, the
sequence used to define a tree is not necessarily unique to that tree.

Note that `(T + U)` is undefined as trees `T` and `U` are disjoint. The union
operation is therefore **not associative**. Hence, it is in general not possible
to evaluate subexpressions in parallel as subexpressions could turn out to be
undefined.

Note that the order of operations in a complete left-to-right sequence is in
general oriented top-down, and then first-to-last.

* `(S + T + U) == ((S + T) + U) <=!=> (S + (T + U))`

```
tree S      tree T          tree U
========    ===========     =============
1 -|-> 2    1 -> 2 -> 4     1 -|-> 2 -> 4
   |-> 3                       |-> 3
```

Because `(S + T) == U == (T + U)`, the root of the 2nd tree does not
necessarily have to be a leaf in the 1st tree.

<!-- ======================================================================= -->
## difference, examples

```
tree S            tree T      (S \ T)    (T \ S)
===========       ======      =======    ========
1 -> 2 -> 3       2 -> 3      1          Ø
```

As mentioned before, this operation is **not commutative**.
