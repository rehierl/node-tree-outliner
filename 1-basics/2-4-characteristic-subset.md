
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
The **characteristic subset** `css(s)` of set `s` in hierarchy `H := (V,P)`,
is a potentially empty subset of `s` such that no element in `css(s)` is also
an element of any of the descendants of `s`.

* `css(s), css(s,H) := css-of-set(s,H)`
* `css-of-set(s,H) := s - (union of all descendant sets of s)`
* signature: (P,H) -> P(V)

Note that ...

* Each set always has exactly one CSS.
* The result of css(s) is defined for any set in H.
* css(s) is an element of powerset P(V).
* (css(l) == l) is true for any leaf set.

Note that, because `s` is a strict subset to any of its ancestors, any
element in `css(s)` is an element of `s` and an element of any ancestor of `s`.
Consequently, `s` is the least significant set in `H` which contains all the
elements in `css(s)`. That is, set `s` acts as the parent set of `css(s)`.

Note that the CSS of a set is empty, if the corresponding set is the union
of its descendant sets (e.g. CSS(/B)). That is, a (simple) hierarchy does
not guarantee that all the sets in `P` have non-empty characteristic subsets.
Furthermore, not every CSS is necessarily an element in `P`.

Note that the characteristic subset could also be defined for strict setups.
The advantage of a hierarchy over a strict setup is however, that a hierarchy
always has a root set (i.e. a hierarchy is never empty).

**CLARIFICATION**
The set of all characteristic subsets `CSS(H)` is defined as follows:

* `CSS(H) := { css(s,H) | for any (s in P) and (H := (V,P)) }`

Note that CSS(H) is never empty.
That is because any hierarchy always has a root set.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
In general, css(s) is an element in P(V).
That is, css(s) is not necessarily an element in P.

The question is, whether or not the image/range of the `css-of-set(s)`
operation can be reduced from P(V) to P? That is, would it be possible to
change the signature from "(P,H) -> P(V)" to "(P,H) -> P"? For that to be
possible, any CSS of a set would itself always have to be an element in P.

(1) The CSS of leaf set l is identical to l (i.e. (css(l) == l)).
That is, (CSS(H) & P) is guaranteed to be non-empty for any hierarchy.

Note that a leaf set is never empty because H is by definition not allowed to
be empty, or even to contain the empty set. Furthermore, the CSS of a leaf set
is not empty because there is no descendant set which could result in the
removal of even a single element. That is, css(l) can not have fewer elements
than leaf set l. Finally, any hierarchy always has one or more leaf sets.

(2) The empty CSS of a parent set is not an element in P.
That is, (CSS(H) - P) is not necessarily empty.

Note that the CSS of a parent set will be empty,
if the parent set is identical to the union of its descendant sets.

Note that H can by definition not contain the empty set.
Consequently, CSS(H) may contain one or more elements that are not in P.

(3) The non-empty CSS of a parent set is not an element in P.
That is, (CSS(H) - P) is not necessarily empty.

By definition, the non-empty CSS of parent set s can not contain any element
which is also an element of a descendant of s. However, and because all elements
in css(s) are also elements of s, any element in css(s) is also an element of
any ancestor of s. That is because s, as a set within a hierarchy, is still a
strict subset to its ancestors.

And because s, as a parent set in a hierarchy, has one or more child sets,
css(s) is guaranteed to have fewer elements than s itself. Consequently, and
in order for (css(s) in P) to be true, css(s) would also have to exist as a
separate descendant set of s. That however is not possible because css(s) would
then have to be empty. Obviously, css(s) can not be empty and non-empty at the
same time, which is why (css(s) in P) is false in this particular case.

(Summary) Set (CSS(H) & P) is guaranteed to be non-empty for any hierarchy, and
set (CSS(H) - P) is guaranteed to be non-empty if (#PS > 0). Consequently, the
signature of `css-of-set()` can not be restricted to P.

Note that ...

* (s in LS) <=> (css(s) in P)
* (s in PS) <=> (css(s) not in P)

**CLARIFICATION**
Any CSS is disjoint to any other CSS.

(0) For this statement to not be true, it would have to be possible that two
distinct characteristic subsets could exist (within the same hierarchy), which
have one or more elements in common. That is, both subsets could not be empty.

(1) For both subsets css(s) and css(t) to not be disjoint, sets s and t would
have to share one or more common elements. That is, because css(s) is still a
subset of s, and css(t) is still a subset of t.

(2) And because two distinct sets within a hierarchy are either disjoint, ex-or
one set is a strict subset of the other, set t is assumed to be a descendant of
set s.

(3) However, if t would indeed be a descendant of s, then css(s) could not
contain any element in t and therefore also not any element in css(t).
Consequently, no two distinct characteristic subsets can exist that have
one or more elements in common.

Note that ...

* css(s) and css(t) are disjoint, for any (s,t in P) and if (s != t)
* css(s) and css(t) can not have even one element in common

**CLARIFICATION**
Any element in css(s) allows to identify its parent set s.

Because all characteristic subsets are disjoint, no two such subsets can exist
that have even one or more elements in common. Because of that, any element in
css(s) is sufficient to identify parent set s.

Note that, in order to identify every set within a hierarchy, the CSS of each
set must have one or more elements (i.e. non-empty).

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The parent set of a CSS can be identified as follows:

* `set-of-css(css,H)` := "the parent set of css in P"
* signature: (P(V),H) -> P

An implementation of this operation could be:

```
set-of-css(css,H) begin
1: S = < s | (s in H) and (css(s) === css) >
2: assert(#S > 0)
3: assert(#S < 1)
4: return oneElementOf(S)
end
```

Note that ...

* The result may be undefined because if `(css == {})` is true,
  then H could contain more than one parent set that is identical
  to the union of its descendants (step 3 could trigger).
* The result will be undefined, if `(css - V)` is non-empty.
  That is, because no set `s` can exist such that `(css(s) === css)`.
  As such, `css` would represent an input error.
* The result may be undefined if `(css - V)` is empty.
  That is, because `(css not in CSS(H))` will be true
  if `(css(s) strict-subset-of css)` and `(css subset-of s)`.
* The result is unique for any `(css in (CSS(H) - {}))`.
  That is because any CSS is disjoint to any other CSS.

Note that, because a hierarchy (like any other strict setup), does not contain
the empty set (i.e. `({} not in P)`), the empty set could be used to represent
a "does not exist" reply.

<!-- ======================================================================= -->

* what does a CSS allow to do?
* characteristic element

**CLARIFICATION**

* not every s in P is a CSS of some other set in P
* `(P - CSS(H))` - if non-empty, then not every set in P is a CSS

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
