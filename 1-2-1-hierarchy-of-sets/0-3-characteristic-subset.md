
<!-- ======================================================================= -->
## Characteristic subset (CSS)

```
|-A-------|   |-C-----------|
| 1 |-B-| |   | |-D-| |-E-| |
|   | 2 | |   | | 1 | | 2 | |
|   |---| |   | |---| |---| |
|---------|   |-------------|
```

* CSS(/A)={1}, CSS(/A/B)={2}
* CSS(/C)={}, CSS(/C/D)={1}, CSS(/C/E)={2}

<!-- ======================================================================= -->
## css(), css-of-set()

**CLARIFICATION**
The **characteristic subset** (CSS) of set `s` in hierarchy `H := (V,P)`,
is a potentially empty subset of `s` such that no element in it is also
an element of any descendant set of `s`.

* `css(s), css(s,h) := css-of-set(s,h)`
* `css-of-set(s,h) := s \ E(D(s,h))`
* signature: (P,H) -> P(V)

Note that ...

* css(s) is defined for any set (s in P)
* `A(s) := { a | (a in P) and (a ancestor-of s) }`
* `D(s) := { d | (d in P) and (d descendant-of s) }`
* `V, E(h) := { e | (e in s) and (s in P) }`

Note that, because `(s in P)` is a strict subset to any of its ancestors,
`css(s)` is a subset of `s` and a strict subset to any set in `A(s)`.
Consequently, `s` is the least significant set to which `css(s)` is a subset.
Because of that, set `s` will be referred to as the parent set of `css(s)`.

**CLARIFICATION**
The **set of all characteristic subsets** is defined as follows:

* `CSS(h) := { css(s,h) | for any (s in P) and (h in H) }`
* `css-of-set(s,h) in CSS(h)`

Note that `CSS(h)` is never empty.
That is because a hierarchy is by definition always non-empty.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The CSS of a leaf set `(l in LS)` is equal to `l`.

That is because a leaf set has no descendant set which could result in the
removal of an element. That is, `css(l)` can not have fewer elements than
its parent set `l`. Likewise, as no leaf set can be empty, the CSS of a
leaf set is never empty.

* `(l in LS) -> (css(l) == l)`
* `(l in LS) -> (css(l) in P)`
* `(l in LS) -> (css(l) != {})`

**CLARIFICATION**
The CSS of a parent set `(p in PS)` may be empty (e.g. CSS(/C)).

That is because, if a parent set (p in PS) is equal to the union of its
descendant sets, then all the elements in (p) are also elements in its
descendant sets. In that particular case, css(p) is empty.

* `(css(p) == {})` if `(p in PS)` and `(p == E(D(p))`
* `(css(p) == {}) -> (p in PS)`

**CLARIFICATION**
The CSS of a parent set `(p in PS)` is never an element in `P`.

That is obviously true, if css(p) is empty. However, it is also true if css(p)
is non-empty. That is because (p), as a parent set, has one or more non-empty
child sets, which is why the non-empty CSS is guaranteed to have fewer elements
than (p). Hence, and in order for (css(p) in P) to be true, css(p) would have
to be a descendant set of (p). (Recall that in a hierarchy, coupled sets are
strictly related to each other). However, css(p) can by definition not be a
descendant set of (p) as css(p) would then be empty. Consequently, css(p) can
not be an element in P if (p in PS).

* `(p in PS) -> (css(p) not-in P)`

Note that the codomain of `css-of-set()` can not be changed from `P(V)` to `P`
because `(CSS(h) \ P)` is guaranteed to be non-empty if `(#PS > 0)`.

**CLARIFICATION**
Note that ...

* `(l in LS) <-> (css(l) in P)`
* `(p in PS) <-> (css(p) not-in P)`
* css(p) may be empty for more than one (p in PS)
* (s in P) is the CSS of (t in P) iff (s == t) and (t in LS)
* i.e. (s in P) can not be the CSS of (t in P) if (t != s)

**CLARIFICATION**
A characteristic subset is understood to exist as an implicit set.

Even though a CSS is not necessarily an element in P (i.e. not necessarily an
explicit element), a CSS is understood to implicitly exist within the hierarchy.
That is because the CSS of a set is defined for any set in P.

<!-- ======================================================================= -->
## disjoint, unique

```
|----------------|
| p1    p2    p3 | - P
|--\----/-----|--|
    \  /      |
|----\/-------|--|
| c1=c2={}    c3 | - CSS(h)
|----------------|
```

**CLARIFICATION**
Two distinct sets in P may in general have the same CSS.
That is because css(p) may be empty for more than one (p in PS).

* `P-to-CSS` is in general a `N:1` relationship
* i.e. `(#CSS(h) <= #P)`

**CLARIFICATION**
Any element in a CSS is unique to its CSS.
Put differently, distinct characteristic subsets are disjoint.

(1) For two distinct sets (s,t in P) to have coupled characteristic subsets,
(s & t) would have to be non-empty. That is because css(s) is still a subset
of (s) and css(t) is still a subset of (t).

(2) In order for (s & t) to be non-empty, sets (s) and (t) would have to be
strictly related. That is because two distinct sets in a hierarchy are either
disjoint ex-or strictly related.

(3) If (t in P) is the descendant of (s in P), then css(s) can by definition
not have any element in (t) and therefore also not any element in css(t).
That however is in conflict with (1), which is why two distinct sets in P
can not have identical or even coupled non-empty characteristic subsets.

* `(css(s) disjoint-to css(t))`, if `(css(s) != css(t))`
* CSS(h) is a union of disjoint sets.

**CLARIFICATION**
Two distinct sets in P can not have the same non-empty CSS.
Put differently, each non-empty CSS is unique to its parent set.

For two distinct sets (s,t in P) to have the same non-empty CSS, both CSS
would need to have elements in common. (Recall that two non-empty sets are
equal if all the elements in both sets are common to both). That however
is not possible since any element in a CSS is unique to its CSS.

* if `(css(s) != {})` is true for any set `(s in P)`, then ...
* `(s != t) <-> (css(s) != css(t))`
* `P-to-CSS` is a `1:1` relationship
* `(#CSS(h) == #P)`

**CLARIFICATION**
A CSS is obviously not "unique" to its parent set (s in P) in a strict sense.
That is because (s) may have one or more ancestor sets and because css(s) is
also a strict subset to all of these sets. However, a CSS is "unique" to (s)
in such a way that (s) is the least significant set of these sets. No other
set "contains" a given CSS in that particular "unique" way.

<!-- ======================================================================= -->
## set-of-css()

**CLARIFICATION**
The parent set in P of a CSS in CSS(h) can be identified as follows:

* `set-of-css(css,H)` := "the parent set of css in P"
* signature: (P(V),H) -> P

An implementation of this operation could be:

```
set-of-css(css,h) begin
1: S = < s | (s in P) and (css(s) == css) >
2: assert(#S > 0)
3: assert(#S < 1)
4: return oneElementOf(S)
end
```

**CLARIFICATION**
The possible outcomes of that implementation are:

(0) The result is undefined, if no (s in P) exists
such that (css(s) == css) - i.e. trigger step-2.

(1) If the input css is empty, then ...

(1.1) The result is unclear if more than one (p in PS) exists
such that (css(p) == {}) - i.e. trigger step-3.

(1.2) The result is (p), if exactly one (p in PS) exists
such that (css(p) == {}).

(2) If the input css is non-empty, then ...

(2.1) The result is a unique (s in P).
That is because css is (due to case 0) guaranteed to be in CSS(h).

Note that each hierarchy always has at least one non-empty CSS.
That is because each hierarchy always has at least one leaf set.

Note that there is also only one case possible (i.e. case-1.1) such that no
unique result can be returned, even though the input (css in CSS(h)) is valid
(i.e. no input error). In contrary to that, the result in case-2.1 is unique
because no two sets can have the exact same non-empty CSS.

Note that, because a hierarchy, like any other strict setup, does not contain
the empty set (i.e. {} not-in P), the empty set could be used to represent a
"does not exist" error response.

**CLARIFICATION**
The result of `set-of-css(css)` is defined and unique,
if the following requirements are met:

* `(css in CSS(h))` is true (i.e. no input error)
* `( #{ p | (css(p) == {}) for any (p in PS) } <= 1)`
* i.e. no more than one parent set has an empty CSS

**CLARIFICATION**
If the above requirements are met,
then `set-of-css()` is inverse to `css-of-set()`.

* `(set-of-css( css-of-set(s) ) == s)` is true for any (s in P)
* `(css-of-set( set-of-css(css) ) == css)` is true for any (css in CSS(h))
