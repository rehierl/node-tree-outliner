
<!-- ======================================================================= -->
# implementation specific aspects

When creating the tree for an input hierarchy of sets,
the following statements may help ...

**CLARIFICATION**
The root set (r) in a (strict) hierarchy is the largest set in (P) and equal to
(V). Furthermore, no other set in (P) can have the same amount of elements as
(r). That is because every other set in (P) must be a strict subset to (r).

* `(r == V)` is true if `(r root-of h)`
* `(#d < #r)` is true for any `(d descendant-of r)`

Note that, due to (r == V), an implementation does not need to maintain (V)
as an explicit set of elements. That is because it would otherwise have to
maintain two instances of the same set (i.e. an unnecessarily increased waste
of memory). An implementation would want to implement (V) as a reference to (r).

**CLARIFICATION**
In a strict hierarchy, (#r == #P) is true.
That is because (r == V) and (#V == #P) are both true.

Since this must also apply to every sub-hierarchy, searching the descendants
of a given set (s in P) may be restricted to (#s) sets that all have fewer
elements than (s). Consequently, one would want to process the overall set
of sets ordered according to the number of elements in each set.

**CLARIFICATION**
In a strict hierarchy, all one-element sets in (P) are leaf sets. That is
because such a set can not have any descendant set as those descendant sets
would also need to have an characteristic element.

**CLARIFICATION**
In a strict hierarchy, the number of elements of a parent set (p in P) may
differ from the number of elements in one of its child sets (c in P) by more
than one. That is because, in a large hierarchy, the root may still have a
leaf as child.

* `(#p == #c+1)` may be true if `(p parent-of c)`
* (but does not have to be true!)

Note that, if it is true, then (c) is the only child of (p).

**CLARIFICATION**
One or more descendant sets of (r) in a (strict) hierarchy may have the same
amount of elements. That is, not all sets in a hierarchy need to have distinct
amounts of elements.

* `(#d1 == #d2)` may be true iff `(d1,d2 descendant-of r)`

**CLARIFICATION**
In a strict hierarchy, all equal-sized sets in (P) are disjoint.

This is obviously true for all leaf sets. However, and since strictly related
sets have distinct sizes, even equal-sized parent sets are disjoint. Because
of that, and in a class of equal-sized sets, at most one set can be an ancestor
to a descendant set.

<!-- ======================================================================= -->

**TODO** - begin with a leaf and work your way up to the root
