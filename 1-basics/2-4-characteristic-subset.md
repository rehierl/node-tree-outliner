
<!-- ======================================================================= -->
## Characteristic subset (CSS)

```
|-A-------|   |-B-----------|
| 1 |-A-| |   | |-A-| |-B-| |
|   | 2 | |   | | 1 | | 2 | |
|   |---| |   | |---| |---| |
|---------|   |-------------|
```

* CSS(/A)={1}, CSS(/A/A)={2}
* CSS(/B)={}, CSS(/B/A)={1}, CSS(/B/B)={2}

**CLARIFICATION**
The **characteristic subset** CSS of set `s`, with regards to
hierarchy `H := (V,P)`, is defined as follows:

* `css(s), css(s,H) := css-of-set(s,H)`
* `css-of-set(s,H) := s - (union of all descendant sets of s)`
* signature: (P,H) -> P(V)

Note that ...

* Each set has exactly one CSS.
* The result of `css(s)` is defined for any set `s in P`.
* The CSS of a set is an element of the powerset `P(V)`.
* The CSS of a set is not necessarily an element of `P`.

The characteristic subset `css(s)` of set `s` in hierarchy `H`, is a
potentially empty subset of `s` such that none of the elements in `css(s)`
is also an element of any of the descendants of `s`.

Note that the CSS of a set is empty, if the corresponding set is the union
of its descendant sets (e.g. CSS(/B)). That is, a (simple) hierarchy does
not guarantee that all the characteristic subsets of its sets are non-empty.

Note that set `s` and all of its ancestors contain all the elements in `css(s)`.
Otherwise, hierarchy `H` would be in conflict with the `subset-of` operator
and could therefore not be a hierarchy. Because of that, `s` is the least
significant set that contains all the elements in `css(s)`. That is, set `s`
is the parent set of `css(s)`.

Note that the characteristic subset could also be defined for strict setups.
The advantage of a hierarchy over a strict setup is however, that a hierarchy
is never empty: A hierarchy always has one root set.

**CLARIFICATION**
The set of all characteristic subsets in H is defined as follows:

* `CSS(H) := { css(s) | (s in P) where (H := (V,P)) }`

**CLARIFICATION**
The parent set of a CSS can be identified as follows:

1. Determine all sets in H to which the CSS is a subset.
2. Return the least significant set of these sets.

Note that this operation will be referred to as the `set-of-css()` operation:

* `set-of-css(css,H)` := "the parent set of css in H"
* signature: (P(V),H) -> P

Note that the result of this operation is undefined, if (1) the supplied CSS is
empty, or (2) if there is no set `s in H` such that `(css(s) == css)` is true.

Note that the set of a CSS can not be determined, if the supplied CSS is empty.
That is, because an empty set is a subset to any set. Consequently, a set which
has an empty CSS can not be identified via its empty CSS.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
equiv? If (css(s) in P), then s is a leaf set.
equiv? If (css(s) not in P), then s is a parent set.

Note that (css(s) in P(V)) and (P subset-of P(V)) are both true by definition.
The question is, could the definition of `css-of-set(s)` be clarified such that
the image/range (i.e. target set) of that operation is reduced (e.g. P instead
of P(V))?

(1) The CSS of leaf set `l` is identical to `l` (i.e. (css(l) == l)). In that
particular case, css(l) is an element of P. Put differently, (CSS(H) & P) is
guaranteed to be non-empty for any hierarchy.

Note that a leaf set is never empty because H is by definition not allowed to
be empty. Furthermore, the CSS of a leaf set is non-empty because there is no
descendant set which could remove even a single element from the leaf set.
Finally, any hierarchy always has one or more leaf sets.

(2) The empty CSS of a parent set is not an element in P. That is, because H
can by definition not contain the empty set. Consequently, CSS(H) may contain
one or more sets that are not in P. Put differently, (CSS(H) - P) is not
necessarily empty.

Note that only a parent set can have an empty CSS.
(If the parent set is the union of its descendant sets).

(3) The non-empty CSS of a parent set is not an element in P.

By definition, the non-empty CSS of parent set s can not contain any element
which is also an element of a descendant set of s. However, and because all
elements in css(s) are also elements of s, any element in css(s) is also an
element of any ancestor of s. That is because s, as a set within a hierarchy,
is still a strict subset to its ancestors.

And because s, as a parent set, has one or more non-empty child sets, css(s)
is guaranteed to have fewer elements than s itself.

Consequently, and in order for (css(s) in P) to be true,


css(s) would have to
be a child/descendant of s. That however is not possible, because css(s) would
then be empty.

Also recall that two sets within a hierarchy are either disjoint, ex-or one
set is a strict subset of the other. Because of that, 

<!-- ======================================================================= -->

* `(P - CSS(H))` - if true, then not every set in P is a CSS

**CLARIFICATION**
The non-empty CSS of a set is unique to that set.
No other set within a hierarchy has the exact same non-empty CSS.

That is, because each element within a non-empty CSS is also an element of the
CSS's parent set, and, because of that, also an element of the ancestors of that
set.

Note that, in order to identify every set within a hierarchy,
the CSS of each set must have one or more elements (i.e. non-empty).

<!-- ======================================================================= -->
## Relationship between the elements in V and P

(warning - not sure, if the following is error-free
or even if it covers all possible cases)

Note that this section is with regards to the requirements
which a given set of sets P thrusts upon the set of elements V.

```
|-A-------|   |-B-----------|   |-C---------------------|
| 1 |-A-| |   | |-A-| |-B-| |   | |-A-| |-B-----------| |
|   | 2 | |   | | 1 | | 2 | |   | | 1 | | |-C-| |-D-| | |
|   |---| |   | |---| |---| |   | |---| | | 2 | | 3 | | |
|---------|   |-------------|   |       | |---| |---| | |
                                |       |-------------| |
                                |-----------------------|
```

(if each set is only allowed to hold a single element)

A hierarchy is minimal, if none of the elements in V can be removed without
changing the structure of the hierarchy and/or without violating any of the
hierarchy's requirements (e.g. no empty set, one root set).

(1) V must have one (unique) element per leaf set `l in L`

* `L := { l | (l in P) and (l is a leaf set) }`
* because H is not allowed to contain empty sets
* each leaf set `l` must have a unique element in V
* because it would otherwise not be possible
  to distinguish the leaf sets from one another
* `(#L <= #V)` must be true

(2) V must have one (unique?) element per parent `p in P1`

* `P1 := { p | (p in P) and (p is a parent) and (p has one child only) }`
* because it would otherwise not be possible to distinguish
  such a parent `p` from parent `q in P1` if `(p != q)`
* `(#L + #P1 <= #V)` must be true

<!-- ======================================================================= -->

In order for `set-of-css()` to be inverse to `css-of-set()` (and vice versa),
each set within a hierarchy `H := (V,P)` must have a non-empty CSS.

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
