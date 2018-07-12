
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
Any element within a CSS is referred to as **a characteristic element (CE)**.
The union of all characteristic subsets within a given hierarchy is said to
be the set of characteristic elements of the corresponding hierarchy. A similar
definition is possible with regards to any (s in P):

* `CE(h) := E(CSS(h))` for any hierarchy `h`
* `CE(s) := css(s)` for any `(s in P)`
* `CE(css) := css` for any `(css in CSS(h))`
* `(CE(x) subset-of V)`

Note that, depending on the context of a statement, (s in P) and css(s) may
both be referred to as **the parent set of** the CE, if the CE is an element
of the corresponding CSS.

Note that, like the set of elements (V) within a hierarchy, CE(h) may be a
homogenous, or a heterogenous set of elements. That is, there is no requirement
of what kind of elements these sets hold.

**CLARIFICATION**
Any characteristic element (CE) is unique to its characteristic subset (CSS)
and therefore also unique to the parent set of its CSS. That is, because any
CSS is disjoint to any other CSS.

* `CSS-to-CE` is a `1:N` relationship.
* `(CSS(h)-{})` is a partition of `CE(h)` into disjoint sets.

Note that the "uniqueness" of a CE is similar to the "uniqueness" of its CSS:
The parent set of a CSS is the least significant set which contains all the
characteristic elements in that CSS.

<!-- ======================================================================= -->
## (CE(h) == V)

**CLARIFICATION**
Any CE, as an element of one or more (s in P), is an element in V.

Because of that, the relationship of each set (s in P) that has one or more CEs,
also depends on all the CEs it holds. After all, and similar to a CSS, any CE is
an element of its parent set (s) and an element of all the sets in A(s).

As a consequence, two disjoint sets (s,t in P) can not hold the same CE. That
is, because both sets would then no longer be disjoint. In addition to that,
both sets would overlap each other as they were initially disjoint. Because of
that, the (disjoint ex-or strictly related) rule could no longer apply, which
is why such CEs, if added to disjoint sets, would break the hierarchy.

**CLARIFICATION**
Any element (v in V) is a characteristic element (ce in CE(h)).

(1) Any hierarchy has exactly one root set (r in P). In addition to that,
the root set holds all the elements in V. That is, because any other set
(s in P) is a strict subset of (r). After all, it would not be the only
root set, if the hierarchy had even one set disjoint to it.

(2) If an element (v in V) is an element such that it does not belong to
any other set (s in P) other than the root set (r), then that element (v)
is a CE of (r). This obviously includes the case in which the root set is
itself a leaf set (i.e. has no child set).

(3) If element (v) is no such element, then it can only belong to one child
set of (r). That is, because the child sets of a set are disjoint to one
another (i.e. disjoint ex-or strictly related).

(4) Child set (c in P), which holds (v in V), can now be understood to
represent the root set (r) of a sub-hierarchy. The iteration therefore
has to continue with step-2 and (c) as the corresponding root (r).

Note that (v) will either be the CE of a parent set ex-or the CE of a leaf set.

**CLARIFICATION**
Every (v in V) is a CE and every CE is an element in V.

* `(CE(h) == V)`
* `(CSS(h)-{})` is a partition of `V` into disjoint sets.

<!-- ======================================================================= -->
## ce(), ce-of-css(), ce-of-set()

A CE of a CSS can be retrieved as follows:

```
ce-of-css(css,h) begin
1: assert(#css > 0)
2: return oneElementOf(css)
end
```

Note that, provided the input parameter (css) does indeed represent an element
in CSS(h), the result is undefined if the CSS is empty. Furthermore, if the
CSS has more than one CE, the result is a random CE of the input CSS. That is,
because, even though each CE is different to all other CEs in that CSS, a simple
set of elements provides no means to retrieve a particular element (i.e. a CSS
has no first/last CE, etc). And even if a simple set of values had such means,
there is no information available to tell which CE to return.

```
ce-of-set(s,h) begin
1: css = css-of-set(s,h)
2: ce = ce-of-css(css,h)
return ce
end
```

Note that, as before, the result is either undefined (if (css(s)=={})),
the single CE of css(s), or a random element in css(s).

```
ce(x,h) begin
  if (x in P) then
    return ce-of-set(x,h)
  else
    return ce-of-css(x,h)
  end if
end
```

Note that any leaf set is identical to its CSS (i.e. css(l) == l) and
that the CSS of a parent set is not an element in P.

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

Note that, provided the input (ce) is indeed an element of an existing CSS,
the result is defined and unique. That is, step-2 can only trigger in case
of an input error, and step-3 only if the corresponding hierarchy is broken.

```
set-of-ce(ce,h) begin
1: c = css-of-ce(ce,h)
2: p = set-of-css(c,h)
3: return p
end
```

Note that, provided the input (ce) does not represent an input error, the
result is defined and unique. That is, because the corresponding CSS will
never be empty.

Note that neither `css-of-ce()` nor `set-of-ce()` allow to retrieve the empty
CSS of a parent set, or a parent set that has an empty CSS. None of those sets
can be retrieved by the above functions because there is no CE that would allow
to identify those sets.

<!-- ======================================================================= -->
## (#CE(s) == 1)

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
The following is true, iff each CSS holds exactly one CE:

* (#CE(s) == 1) is true for any (s in P)
* `ce-of-set()` is defined and unique for any (s in P)
* `set-of-ce()` allows to identify any (s in P)

**CLARIFICATION**
`(#V == #P)` is true, iff each CSS holds exactly one CE.

(1) (#CSS(h) == #P) -
That is, because each CSS is now required to be non-empty.
In addition to that, any non-empty CSS is distinct to any other CSS.

(2) (#CE(h) == #P) -
That is, because each CSS is required to hold exactly one CE.

(3) (#V == #P) -
That is, because (CE(h) == V).

**CLARIFICATION**
`ce-of-set()` is inverse to `set-of-ce()` iff each CSS holds exactly one CE.

* `(set-of-ce( ce-of-set(s) ) == s)` is true for any (s in P)
* `(ce-of-set( set-of-ce(ce) ) == ce)` is true for any (ce in CE(h))

**CLARIFICATION**
Any non-empty CSS can be minimized to hold exactly one CE.

Additional CEs do not add substantial information to a hierarchy. They merely
increase the storage requirement of a hierarchy (hint: ancestor sets). That is,
instead of having multiple distinct CEs per set, each of which can be understood
to represent a bit of information which is unique to a set, a set should hold
only one reference to the combined information of that set.
