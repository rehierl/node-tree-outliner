
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

<!-- ======================================================================= -->
## css-of-set()

**CLARIFICATION**
The **characteristic subset (CSS)** `css(s)` of set `s` in hierarchy
`H := (V,P)`, is a potentially empty subset of `s` such that no element
in `css(s)` is also an element of any of the descendants of `s`.

* `css(s), css(s,H) := css-of-set(s,H)`
* `css-of-set(s,H) := s - (union of all descendant sets of s)`
* signature: (P,H) -> P(V)

Note that ...

* The result of css(s) is defined for any set in H.
* Each set always has exactly one CSS.
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

* (s in LS) => (css(s) != {})
* (css(s) == {}) => (s in PS)
* (s in LS) <=> (css(s) in P)
* (s in PS) <=> (css(s) not in P)

**CLARIFICATION**
A CSS is understood to be an existing part of a hierarchy.

Even though a CSS is not necessarily an element in P (i.e. not an explicit
set in H), any CSS is understood as an existing subset and consequently as
a distinct element. That is, because a hierarchy allows to extract any CSS
within it.

**CLARIFICATION**
Any CSS is disjoint to any other CSS.

(1) For both subsets css(s) and css(t) to not be disjoint, sets s and t must
have one or more elements in common. That is, because css(s) is still a subset
of s, and css(t) is still a subset of t.

(2) In order for s and t to share one or more elements, t must be a strict
subset (i.e. descendant) of s (or vice versa). That is, because in a hierarchy,
two distinct sets are either disjoint, ex-or one set is a strict subset of the
other.

(3) If t would indeed be a descendant of s, then css(s) could (by definition)
not contain any element in t and therefore also not any element in css(t).
Consequently, no two distinct characteristic subsets can exist that have one
or more elements in common. That is, two distinct characteristic subsets are
always disjoint.

Note that ...

* css(s) and css(t) are disjoint, for any (s,t in P) and if (s != t)
* css(s) and css(t) can not have even one element in common

<!-- ======================================================================= -->
## set-of-css()

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
4: return anElementOutOf(S)
end
```

Note that ...

* The result may be undefined if `(css == {})` is true. That is,
  because H could contain more than one parent set which is
  identical to the union of its descendants (will trigger step 3).
* The result will be undefined if `(css - V)` is non-empty.
  That is, because no set `s` can then exist such that `(css(s) === css)`.
* The result may be undefined even if `(css - V)` is empty.
  (e.g. if `css` is a parent set in H).
* The result is defined and unique for any `(css in (CSS(H) - {}))`.
  That is because any CSS is disjoint to any other CSS.

Note that, because a hierarchy (like any other strict setup), does not contain
the empty set (i.e. `({} not in P)`), the empty set could be used to represent
a "does not exist" response.

**CLARIFICATION**
The result of `set-of-css()` is defined and unique,
if the following requirements are met:

* `(css in CSS(H))` is true (i.e. no input error).
* Each CSS in the hierarchy has one or more elements.

In such a case, `set-of-css()` is inverse to `css-of-set()`:

* `(set-of-css( css-of-set(s) ) == s)` is true for any `s in H`
* `(css-of-set( set-of-css(css) ) == css)` is true for any `css in CSS(H)`

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Even a single element in css(s) is sufficient to uniquely identify set s.

Because a CSS is disjoint to any other CSS, no two such subsets can exist
that have even one element in common. Consequently, any element in css(s)
is sufficient to uniquely identify the parent set s of css(s).

Note that these kind of elements are obviously not "unique" to s in a strict
sense. That is, because s may have one or more ancestor sets and because css(s)
is also a subset to all of these ancestors. However, these elements are "unique"
to s in such a way that s is the least significant set of those sets. No other
set contains these elements in that particular "unique" way.

**CLARIFICATION**
A unique point of view: The elements within a CSS are no "object properties",
they are "object identifiers". That is, any element within a CSS can be seen as
a reference to data that is unique to a set. This allows to associate a property
with a set that may hold the same value as the property of another set (e.g. a
tag name).

**CLARIFICATION**
Any non-empty CSS can be minimized to hold one element only.

A non-empty CSS does not need to have more than one element. Additional elements
do not add substantial information to a hierarchy. They merely increase the
storage requirement of a hierarchy (hint: ancestor sets). That is, instead of
having multiple distinct objects per set, each of which holds a single property,
a set may and should contain only one reference to an object that combines all
the properties of that set.

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
