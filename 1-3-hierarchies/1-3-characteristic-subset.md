
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
The **characteristic subset (CSS)** of set `s` in hierarchy `H := (V,P)`,
is a potentially empty subset of `s` such that no element in CSS is also
an element of any descendant of `s`.

* `css(s), css(s,h) := css-of-set(s,h)`
* `css-of-set(s,h) := s - D(s,h)`
* signature: (P,H) -> P(V)

Note that ...

* `css(s)` is defined for any set in `P`.
* For any set `(s in P)`, `css(s)` returns one result only.
* `(css(l) == l)` is true for any leaf set `(l in LS)`.
* `(css(s) in P(V))` for any `(s in P)`.
* `A(s) := { a | (a ancestor-of s) }`.
* `D(s) := { d | (d descendant-of s) }`.
* `V, E(h) := { e | (e in s) and (s in P) }`.

Note that the characteristic subset could also be defined based upon strict
setups. However, a hierarchy is guaranteed to be non-empty.

Note that, because `s` is a strict subset to any of its ancestors, any element
in `css(s)` is an element of `s` and any element in `A(s)`. Consequently, `s`
is the least significant set in `P` which contains all the elements in `css(s)`.
Because of that, set `s` will be referred to as **the parent set of** `css(s)`.

Note that the CSS of a set is empty, if the corresponding set is the union
of its descendant sets (e.g. CSS(/C)). That is, a hierarchy does not guarantee
that all the sets `(s in P)` have a non-empty CSS (i.e. `(css(s) == {})` is
possible).

**CLARIFICATION**
Any CSS is understood to exist as a distinct (implicit) entity.

Even though a CSS is not necessarily an element in P (i.e. not an explicit
entity), any CSS is understood to exist within the corresponding hierarchy.
That is, because the CSS of any set in P can be determined at any time.

<!-- ======================================================================= -->
## CSS(), CE()

**CLARIFICATION**
The **set of all characteristic subsets (CSS)** is defined as follows:

* `CSS(h) := { css(s,h) | for any (s in P) and (h in H) }`

Note that `CSS(h)` is never empty, which is because no hierarchy is empty.

**CLARIFICATION**
The union of all characteristic subsets within a given hierarchy is said to
be **the set of characteristic elements (CE) of** the corresponding hierarchy.
Similar definitions are possible with regards to any CSS and any (s in P):

* `CE(h) := E(CSS(h))` for any hierarchy `h`
* `CE(s) := E({ css(s) })` for any `(s in P)`
* `CE(css) := css` for any `(css in CSS(h))`

Note that any element within a CSS is said to be **a characteristic element**.

<!-- ======================================================================= -->
## derived statements

In general, `css(s)` is an element in `P(V)`.
That is, `css(s)` is not necessarily an element in `P`.

The question is, whether or not the codomain of `css-of-set()` could
be reduced from P(V) to P? That is, would it be allowed to change the
signature from `(P,H) -> P(V)` to `(P,H) -> P`?

**(1)** (css(l) == l) for (l in LS).
That is, (CSS(h) & P) is guaranteed to be non-empty for any hierarchy.

Note that a leaf set (l) is never empty because a hierarchy is by definition
not allowed to contain the empty set. Furthermore, the CSS of a leaf set is
not empty because there is no descendant set which could result in the removal
of even one element. That is, css(l) can not have fewer elements than the 
corresponding leaf set. Consequently, (css(l) == l) is true.

Note that, any hierarchy always has at least one leaf set.

**(2)** (css(p) !in P), if (css(p) == {}).
That is, (CSS(h) - P) is not necessarily empty.

Note that the CSS of a parent set (p) will be empty,
if the parent set is identical to the union of its descendant sets.

Note that a hierarchy (h) can by definition not contain the empty set. That is,
because a hierarchy is still a setup of sets. Consequently, CSS(h) may contain
an element (i.e. the empty set {}), which is not in P.

**(3)** (css(p) !in P), if (css(p) != {}).
That is, (CSS(h) - P) is not necessarily empty.

By definition, the non-empty CSS of parent set (p in PS) can not contain any
element which is also an element in any set of D(p). However, all elements in
css(p) are also elements in any set of A(p). That is because any set (s in P)
is still a strict subset to all of its ancestors.

And because (p in PS) has one or more child sets, which is guaranteed in that
particular case, css(p) is guaranteed to have fewer elements than (p) itself.
Consequently, and in order for (css(p) in P) to be true, css(p) would have to
be a set in D(p). That however is not possible because css(p) would then have
to be empty. Obviously, css(p) can not be empty and non-empty at the same time,
which is why (css(p) in P) can not be true.

**CLARIFICATION**
The codomain of `css-of-set()` can not be changed (from `P(V)` to `P`)
because `(CSS(h) - P)` is guaranteed to be non-empty if `(#PS > 0)`.

Note that ...

* `(s in LS) -> (css(s) != {})`
* `(css(s) == {}) -> (s in PS)`
* `(l in LS) <-> (css(l) in P)`
* `(p in PS) <-> (css(p) not-in P)`

Note that css(p) may be empty (i.e. {}) for more than one (p in PS).

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Any CSS is disjoint to any other CSS.

(1) For css(s) and css(t) to not be disjoint, (s & t) would have to be
non-empty for two distinct sets (s,t in P). That is, because css(s) is
still a subset of (s), and css(t) is still a subset of (t).

(2) In order for (s & t) to be non-empty, both sets would have to be
strictly related. That is, because two distinct sets in a hierarchy are
either disjoint ex-or strictly related.

(3) If (t) would be a descendant of (s), then css(s) could by definition
not contain any element in (t) and therefore also not any element in css(t).
Consequently, two distinct characteristic subsets can not have even one
element in common.

* `(css(s) disjoint-to css(t))`, if `(s != t)`
* `CSS(h)` is a set of disjoint sets.

**CLARIFICATION**
Two distinct sets in P may still have the same CSS - i.e. N:1.
Which is, because css(p) may be empty for more than one (p in PS).

* `P-to-CSS` is a `N:1` relationship.
* `(s != t) and (css(s) == css(t)) -> (css(s) == {}) or (css(t) == {})`
* `(css(s) != css(t)) -> (s != t)`
* `(#CSS(h) <= #P)`

**CLARIFICATION**
Any non-empty CSS is unique to its parent set - i.e. 1:1.
No other set in P has the exact same non-empty CSS.

* `(s != t) <-> (css(s) != css(t))`, if `(css(s) != {})`

**CLARIFICATION**
Any characteristic element (CE) is unique to its characteristic subset (CSS).
Any CE is an element to exactly one CSS - i.e. 1:N.

* `CSS-to-CE` is a `1:N` relationship.
* `(CSS(h) - {})` is a partition of `CE(h)` into disjoint sets.

<!-- ======================================================================= -->
## set-of-css()

**CLARIFICATION**
The parent set of a CSS can be identified as follows:

* `set-of-css(css,H)` := "the parent set of css in P"
* signature: (P(V),H) -> P

An implementation of this operation could be:

```
set-of-css(css,h) begin
1: S = < s | (s in P) and (css(s) == css) >
2: assert(#S > 0)
3: assert(#S < 1)
4: return oneElementIn(S)
end
```

**CLARIFICATION**
The possible outcomes of `set-of-css()` are:

(1) If the input css is empty.

(1.1) The result is undefined if no (p in PS) exists
such that (css(p) == {}) - i.e. triggers step 2.

(1.2) The result is unclear if more than one (p in PS) exists
such that (css(p) == {}) - i.e. triggers step 3.

(1.3) The result is (p), if exactly one (p in PS) exists
such that (css(p) == {}).

(2) If the input css is non-empty.

(2.1) The result is undefined if (css - V) is non-empty.
That is, because (css !in CSS(h) - i.e. triggers step 2.

(2.2) The result is undefined if (css !in CSS(h))
- e.g. if (css in PS) - i.e. triggers step 2.

(2.3) The result is a unique (s in P).
That is, because css is then guaranteed to be in CSS(h).

Note that each hierarchy always has at least one non-empty CSS.
That is, because each hierarchy always has at least one leaf set.

Note that there is only one case possible (i.e. case 1.2) such that no unique
result can be returned, even though the input (css in CSS(h)) is valid (i.e.
no input error). In contrary to that, the result in case 2.3 is guaranteed to
be unique because any CSS is disjoint to any other CSS.

Note that, because a hierarchy (like any other strict setup), does not contain
the empty set (i.e. ({} not-in P)), the empty set could be used to represent a
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

* `(set-of-css( css-of-set(s) ) == s)` is true for any `s in P`
* `(css-of-set( set-of-css(css) ) == css)` is true for any `css in CSS(h)`

<!-- ======================================================================= -->
## derived statements

