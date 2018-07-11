
<!-- ======================================================================= -->
# Characteristic element (CE)


**TODO**

* relationship between #CE and #V
* is any (v in V) a CE?
* ce(), ce-of-set(), set-of-ce()

<!-- ======================================================================= -->
## ce(), set-of-ce()

**CLARIFICATION**
Any single CE is sufficient to uniquely identify the corresponding parent set
`(s in P)`.

Because a CSS is disjoint to any other CSS, no two such subsets can exist that
have one or more elements in common. Consequently, any element in css(s) is
sufficient to uniquely identify its parent set.

Note that a CE is obviously not "unique" to (s) in a strict sense. That is,
because #A(s) may be non-empty and because css(s) is also a subset to all of
these ancestors. However, these elements are "unique" to (s) in such a way
that (s) is the least significant set of those sets. No other set contains
a given CE in that particular "unique" way.

**CLARIFICATION**
A unique point of view: The elements within a CSS are no "object properties",
they are "object identifiers". That is, any CE can be seen as a reference to
data that is unique to a set. This allows to associate a property with a set
that may hold the same value as the property of another set (e.g. a tag name).

**CLARIFICATION**
Any non-empty CSS can be minimized to hold one CE only.

A non-empty CSS does not need to have more than one CE. Additional CEs do not
add substantial information to a hierarchy. They merely increase the storage
requirement of a hierarchy (hint: ancestor sets). That is, instead of having
multiple distinct CEs per set, each of which holds a single property, a set
may and should contain only one reference to an object that combines all the
properties of that set.

<!-- ======================================================================= -->
## TODO

* a tree of references
* what does a CSS allow to do?
* characteristic element
* allow to verify that a hierarchy of sets corresponds with a node tree
* not every s in P is a CSS of some other set in P
* `(P - CSS(H))` - if non-empty, then not every set in P is a CSS

Because of that requirement, each set must have one or more elements, which
none of its descendant sets is allowed to have. Consequently, such a
hierarchy must have at least as many elements in V as it has sets in P
(i.e. `(#P <= #V)`).

The CSS of a set can obviously be considered to represent data which is "unique"
to that set. That is, because there is always exactly one least significant set
which holds all the elements in that CSS. As such, the non-empty CSS of a set
can be understood to further characterize the corresponding set.

Note however, that the elements within the CSS of a set has an effect on the
relationship a set has with all the other sets in a hierarchy. After all, the
elements of a CSS are also elements of its ancestor sets (including the CSS's
parent set). That is, the elements within a CSS are not independent of the
relationships within a hierarchy (and vice versa).

* Recall that a root set `r in P` is the union of all of its descendant sets:
  i.e. `(#r == #V)`.

<!-- ======================================================================= -->
## TODO - strict Hierarchy/Forest of sets

**CLARIFICATION**
A setup is said to be **a strict hierarchy (of sets)**,
if the following requirements are met:

0. `H := (V,P)`
1. The setup is a (simple) hierarchy.
2. `(#css(s) == 1)` for each set `s in P`

Note that ...

* strict hierarchy => simple hierarchy
* The characteristic subset of each set `css(s)`
  consists of a single element in `V`.
* Each set `s in P` can be identified by a single element in `V`.

**CLARIFICATION**
A setup is said to be **a strict forest (of hierarchies)**
or "a forest of strict hierarchies", if the following requirements are met:

0. `F := (V,P)`
1. The setup is a simple forest.
2. Each hierarchy in `F` is strict.

Note that

* strict forest => simple forest
* All hierarchies within a forest are disjoint.
* Each set `s in P` can be identified by a single value `v in V`.
