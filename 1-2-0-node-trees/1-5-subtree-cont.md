
<!-- ======================================================================= -->
## Subtrees (of trees)

<!-- ======================================================================= -->
## remarks

* CG := the class of generic subtrees
* CIN := the class of subtrees that are induced by a set of nodes
* CIE := the class of subtrees that are induced by a set of edges
* CIR := the class of subtrees that are induced by the subtree's root

Note that any generic subtree of a tree can be expressed as an induced subtree,
if the subtree is induced by the appropriate subset nodes or edges. However,
since not every descendant of the root has to be included in a generic subtree,
not every generic subtree can be expressed as a subtree that is induced by its
root. That is, this class of induced subtrees has in general fewer elements
than the class of generic subtrees.

* CI := (CIN + CIE + CIR)
* (CIN == CIE)
* (CIR subset-of CIN)
* (CI == CIN)
* (CG == CI)

Note that CIR is equal to CIN only if the super-tree has one node only.
In every other case, CIR will be a proper subset of CIN.

<!-- ======================================================================= -->
## remarks

() Note that an induced proper subtree `S := G[T] := (T,U)` (i.e. `(#T < #N)`)
can not have the same set of edges as tree `G := (N,E)` (i.e. `(#U < #E)`)
since the number of edges in `S`, is then also smaller than the number of
edges in `G`. That is because any edge incident to a remove node must be
implicitly removed.

* `(S == G[T]) -> (#U < #E)`, if `(#T < #N)`
* `(S == G[T]) -> (#U == #E)`, if `(#T == #N)`
* i.e. `(G[T] proper-subtree-of G) -> (#T < #N) and (#U < #E)`

Because of that ...

* `(#T < #N) <-> (#U < #E)`, if `(S == G[T])`
* `(T == N) <-> (U == E)`, if `(S == G[T])`
* `(G[N] == G)` is true

() Note that any subtree which is induced by its root, is a subtree that is
induced by the outer set of its root (i.e. `(G[r] := G[OS(r)])`). Because of
that, the above also applies to subtrees of the form `G[r]`.

* `(#T < #N) <-> (#U < #E)`, if `(S == G[r])`
* `(T == N) <-> (U == E)`, if `(S == G[r])`
* `(G[r] == G) <-> (r == RN(G))`

() Note that an induced proper subtree `S := G[U] := (T,U)` (i.e. `(#U < #E)`)
can not have the same set of nodes as `G` (i.e. `(T == N)`). That is because,
except for the root, every node in a tree has one parent only. Conversely,
if the entire set of edges of a tree is used to induce a subtree, then that
subtree will be equal to the super-tree since it has no disconnected nodes.

* `(S == G[U]) -> (#T < #N)`, if `(#U < #E)`
* `(S == G[U]) -> (#T == #N)`, if `(#U == #E)`
* i.e. `(G[U] proper-subtree-of G) -> (#T < #N) and (#U < #E)`

Because of that ...

* `(#T < #N) <-> (#U < #E)`, if `(S == G[U])`
* `(T == N) <-> (U == E)`, if `(S == G[U])`
* `(G[E] == G)` is true

() Note that any subtree of a tree can be expressed as an induced subtree,
induced by its set of nodes or edges. Because of that, any proper subtree
of a tree has a proper subset of nodes and a proper subset of edges.

* `(#T < #N) <-> (#U < #E)` => `(T == N) <-> (U == E)`
* i.e. `((#T < #N) and (#U < #E))` ex-or `((T == N) and (U == E))`
* `(S proper-subtree-of G) -> (#T < #N) and (#U < #E)`, if `isTree(G)`

<!-- ======================================================================= -->
## remarks

The following is a formal approach which confirms the above:

Note that the number of nodes in a tree is coupled with the number of its
edges (i.e. `(#E == #N-1)`, i.e. `(#E < #N)`).

```
   remove X nodes         remove Y edges
   ==================     ==================
1. (#E == #N-1)           (#N == #E+1)
2. (#T == #N-X)           (#U == #E-Y)
3. (#E == (#T+X)-1)       (#N == (#U+Y)+1
4. (#U == #T-1)           (#T == #U+1)
5. (#E == (#U+1)+X-1)     (#N == (#T-1)+Y+1)
6. (#E == #U+X)           (#N == #T+Y)
7. (#U == #E-X)           (#T == #N-Y)
```

Consequently, if a node is removed from a tree, then the resulting subtree
is guaranteed to also have fewer edges. Likewise, if an edge is removed from
a tree, then the resulting subtree is also guaranteed to have fewer nodes.

In addition to that, the number of elements removed from the set of a tree
will result in the removal of the same amount of elements from the other set.
Put differently, a subtree can only have the same set of edges, if and only
if its set of nodes is equal to the set of nodes of its super-tree.

* `(#T == #N-X) -> (#U == #E-X)`
* `(#U == #E-Y) -> (#T == #N-Y)`
* `(#T == #N-X) <-> (#U == #E-X)`, for `(X > 0)`

Because of that ...

* `(#T < #N) <-> (#U < #E)` => `(T == N) <-> (U == E)`
* `(S == G)` ex-or `((#T < #N) and (#U < #E))`
* `(S proper-subtree-of G) -> (#T < #N) and (#U < #E)`, if `isTree(G)`
