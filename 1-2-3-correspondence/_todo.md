
<!-- ======================================================================= -->
# TODO - correspondence / category theory

* set of rooted paths
* each rooted path is itself a hierarchy of rooted paths
* associate a parent = associated all descendants?

<!-- ======================================================================= -->
## initial draft

Since a (directed) unordered tree corresponds with a hierarchy of sets (HoS)
and with a hierarchy of trees (HoT), the question is whether a HoS also
corresponds with a HoT?

```
       Tree T
        / \
       /   \
HoS(T) ----- HoT(T)
```

Both hierarchies correspond with each other!

* Any HoT can be transformed into a HoS (straight forward)
* Any HoS can be transformed into a HoT (more complex)

If `T` represents a directed tree, then ...

* `T == Tree(HoS(T)) == Tree(HoT(T))`
* `T == Tree(HoS(HoT(T))) == Tree(HoT(HoS(T)))`

Hint to category theory:

* If a proof exists for a HoT, then that proof also applies to the tree.
* The same applies if that proof is based upon a tree or upon a HoS.
