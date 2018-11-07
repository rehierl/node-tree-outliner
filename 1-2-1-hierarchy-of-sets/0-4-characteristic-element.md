
<!-- ======================================================================= -->
# Characteristic element (CE)

```
|-------------|
| c1={}    c2 | - CSS(h)
|---------/|--|
         / |
|-------/--|--|
|      e1  e2 | - CE(h)
|-------------|
```

**CLARIFICATION**
Any element within a CSS will be referred to as **a characteristic element CE**.
The union of all characteristic subsets within a hierarchy will be referred to
as **the set of (all) characteristic elements CE(h)** in the corresponding
hierarchy. A similar definition is possible in regards to any (s in P):

* `CE(h) := E(CSS(h))` for any hierarchy `h`
* `CE(s) := css(s)` for any `(s in P)`
* `CE(css) := css` for any `(css in CSS(h))`

Note that, depending on the context of a statement, (s in P) and css(s) may
both be referred to as the parent set of a CE, if the CE is an element of
the corresponding CSS.

Note that, like the set of elements (V) within a hierarchy (h), CE(h) may
be a homogenous, or a heterogenous set of elements. That is, there is no
requirement of what kind of elements these sets hold.

**CLARIFICATION**
Each CE is unique to its CSS. That is, two distinct sets (s,t in P)
can not have any characteristic elements in common.

* `CSS-to-CE` is a `1:N` relationship.
* i.e. a CSS may have one or more CEs
* `(CSS(h) \ {})` is a partition of `CE(h)` into disjoint sets.

Note that the "uniqueness" of a CE is similar to the "uniqueness" of its CSS:
The parent set of a CSS is the least significant set which contains all the
characteristic elements in that CSS.

**CLARIFICATION**
The relationship of each set (s in P) with a non-empty CSS depends on its CEs.
After all, and similar to a CSS, any CE is an element of its parent set (s)
and an element of all the sets in A(s).

As a consequence, two disjoint sets (s,t in P) can not hold the same CE. That
is, because both sets would then no longer be disjoint. In addition to that,
both sets would overlap each other as they were initially disjoint. Because of
that, the (disjoint ex-or strictly related) rule could no longer apply, which
is why such CEs, if added to disjoint sets, would break the hierarchy.

<!-- ======================================================================= -->
## (CE(h) == V)

**CLARIFICATION**
Each CE is an element in V.

That is because each CE is an element of one or more sets in P.

**CLARIFICATION**
Each element in V is a CE.

(1) Any hierarchy (h) has by definition exactly one root set (r in P).
Furthermore, the root set is equal to V, which is because any other set
(s in P) is a strict subset to (r).

(2) If element (v) is an element such that it is not an element of any other
set other than the root set (r), then that element is an CE of (r). (Note that
this includes the case in which the root set is itself a leaf set).

(3) If element (v) is no such element, then it must also be an element of one
of the child sets of (r). That is because the child sets of a parent set are
disjoint to one another (i.e. due to disjoint ex-or strictly related).

(4) Child set (c in P), which holds (v in V), can now be seen as the root set
(r) of a sub-hierarchy. The iteration therefore has to recursively continue
with step-2.

**CLARIFICATION**
The overall set of CEs is equal to the hierarchy's set of elements.
That is because each element in V is a CE and each CE is an element in V.

* `(CE(h) == V)`
* `(CSS(h) \ {})` is a partition of `V` into disjoint sets.
* (recall that all characteristic subsets are disjoint)

<!-- ======================================================================= -->
## ce-of-css(), ce-of-set(), ce()

A (random) CE of a CSS can be retrieved as follows:

```
ce-of-css(css,h) begin
1: assert(#css > 0)
2: return oneElementOf(css)
end
```

Note that, provided the input CSS does indeed represent an element in CSS(h),
the result is undefined if the CSS is empty. Furthermore, if the CSS has more
than one CE, the result is a random CE of the input CSS. That is because, even
though each CE is distinct to all the other CEs in that CSS, a simple set of
elements provides no means to retrieve a particular element (i.e. a CSS has no
first/last CE, etc). And even if a simple set of values had such means, there
is no information available to tell which specific CE to return.

```
ce-of-set(s,h) begin
1: css = css-of-set(s,h)
2: ce = ce-of-css(css,h)
return ce
end
```

Note that, as before, the result is either undefined (if (css(s) == {})),
the single CE of css(s), or a random CE in css(s).

```
ce(x,h) begin
  if (x in P) then
    return ce-of-set(x,h)
  else
    return ce-of-css(x,h)
  end if
end
```

Note that any leaf set is equal to its CSS (i.e. css(l) == l) and that the CSS
of a parent set is not an element in P. Hence, if (x) is not a set in P, then
(x) must be a CSS. If, in contrary to that, (x) is a set in P, then (x) may or
may not be a CSS (i.e. leaf set vs. parent set).

<!-- ======================================================================= -->
## css-of-ce(), set-of-ce()

The CSS of a CE can be retrieved as follows:

```
css-of-ce(ce,h) begin
1: S = < css(s) | (s in P) and (ce in css(s)) >
2: assert(#S > 0)
3: assert(#S < 1)
4: return oneElementOf(S)
end
```

Note that, provided the input CE is indeed the element of a CSS, the result is
defined and unique. That is, step-2 can only trigger in case of an input error,
and step-3 only if the corresponding hierarchy is broken (as each CE is unique
to its CSS).

```
set-of-ce(ce,h) begin
1: c = css-of-ce(ce,h)
2: p = set-of-css(c,h)
3: return p
end
```

Note that, provided the input CE is indeed the element of a CSS, the result is
defined and unique. That is because the corresponding CSS will never be empty.

Note that neither `css-of-ce()` nor `set-of-ce()` allow to retrieve the empty
CSS of a parent set, or a parent set that has an empty CSS. None of those sets
can be retrieved as there is no CE that would allow to identify those sets.

<!-- ======================================================================= -->
## Iff (#CE(s) == 1)

```
|----------------|
| p1    p2    p3 | - P
|-|-----|-----|--|
  |     |     |
|-|-----|-----|--|
| c1    c2    c3 | - CSS(h)
|-|-----|-----|--|
  |     |     |
|-|-----|-----|--|
| e1    e2    e3 | - CE(h)
|----------------|
```



**CLARIFICATION**
The following is true, iff each CSS has exactly one CE:

* if (#CE(s) == 1) is true for any (s in P), then ...
* `ce-of-set()` is defined and unique for any (s in P)
* `set-of-ce()` allows to retrieve any (s in P)

**CLARIFICATION**
If each CSS has exactly one CE, then V and P have equal size.

(1) (#CSS(h) == #P) -
That is because each set (s in p) has a unique non-empty CSS.

(2) (#CE(h) == #P) -
That is because each CSS is required to have exactly one CE.

(3) (#V == #P) -
That is because (#CSS(h) == #P == #CE(h) == #V).

* `(#V == #P)` is true, iff `(#CE(s) == 1)`

**CLARIFICATION**
`ce-of-set()` is inverse to `set-of-ce()` iff `(#CE(s) == 1)`.

* `(set-of-ce( ce-of-set(s) ) == s)` is true for any `(s in P)`
* `(ce-of-set( set-of-ce(ce) ) == ce)` is true for any `(ce in CE(h))`
