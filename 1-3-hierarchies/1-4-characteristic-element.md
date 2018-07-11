
<!-- ======================================================================= -->
# Characteristic element (CE)

```
        |-------------|
CSS(h): | c1={}    c2 |
        |---------/|--|
                 / |
        |-------/--|--|
CE(h):  |      e1  e2 |
        |-------------|
```

**CLARIFICATION**
Any element within a CSS is referred to as **a characteristic element (CE)**.
The union of all characteristic subsets within a given hierarchy is said to
be the set of characteristic elements of the corresponding hierarchy. Similar
definitions are possible with regards to any CSS and any (s in P):

* `CE(h) := E(CSS(h))` for any hierarchy `h`
* `CE(s) := css(s)` for any `(s in P)`
* `CE(css) := css` for any `(css in CSS(h))`
* `(CE(x) subset-of V)`

Note that, depending on the context of a statement, (s in P) and css(s) may
both be referred to as **the parent set of** the CE, if the CE is an element
of the corresponding CSS.

Note that, like the set of elements (V) within a hierarchy, CE(h) may be a
homogenous, or heterogenous set of elements. That is, there is no requirement
of what kind of elements these sets hold.

**CLARIFICATION**
Any characteristic element (CE) is unique to its characteristic subset (CSS)
and therefore also unique to the parent set of its CSS. That is, because any
CSS is disjoint to any other CSS.

* `CSS-to-CE` is a `1:N` relationship.
* `(CSS(h) - {})` is a partition of `CE(h)` into disjoint sets.

Note that any CE is an element of exactly one CSS.
That is, there is no CE that does not belong to any CSS.

Note that the "uniqueness" of a CE is similar to the "uniqueness" of its CSS:
The parent set of a CSS is the least significant set which contains all the
characteristic elements in that CSS.

<!-- ======================================================================= -->
## (CE(h) == V)

**CLARIFICATION**
Any CE, as an element of some (s in P), is an element in V. As such, the
relationship of each set (s in P) that has one or more CEs, also depends on
all the CEs it has. After all, and similar to a CSS, any CE is an element of
its parent set (s) and an element in all the sets of A(s).

Because of that, two disjoint sets (s,t in P) can not hold the same CE. That is,
because both sets would then no longer be disjoint. In addition to that, both
sets would overlap each other as they were initially disjoint. Consequently,
the (disjoint ex-or strictly related) rule could no longer apply, which is why
such CEs, if added to disjoint sets, would disband/break the whole hierarchy.

* is any (v in V) a CE?
* relationship between #CE and #V?

<!-- ======================================================================= -->
## ce(), ce-of-css(), ce-of-set()

A CE of a CSS can be retrieved as follows:

```
ce-of-css(css,h) begin
1: assert(#css > 0)
2: return oneElementOf(css)
end
```

Note that, provided the input (css) is indeed an element in CSS(h), the result
is undefined if the CSS is empty. Furthermore, if the CSS has more than one CE,
the result is a "random" CE of the supplied CSS. That is, because, even though
each CE is different from all other CEs, a simple set of elements provides no
means to retrieve a particular element (i.e. a CSS has no first/last CE, etc).

```
ce-of-set(s,h) begin
1: css = css-of-set(s,h)
2: ce = ce-of-css(css,h)
return ce
end
```

Note that, as before, the result is either undefined (if (css(s)=={})),
the single CE of css(s), or a "random" element of css(s).

```
ce(x,h) begin
  if (x in LS) then
    return ce-of-css(x,h)
  else
    return ce-of-set(x,h)
  end if
end
```

Recall that any leaf set is identical to its CSS (i.e. (css(l) == l)) and
that only the CSS of a parent set is not an element in P.

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

**CLARIFICATION**
The following is true, iff each CSS holds one CE only:

* `(#CE(s) == 1)` is true for any (s in P)
* `ce-of-set()` is defined and unique for any (s in P)
* `set-of-ce()` can be used to identify any (s in P)

**CLARIFICATION**
`ce-of-set()` is inverse to `set-of-ce()` iff each CSS holds one CE only.

* `(set-of-ce( ce-of-set(s) ) == s)` is true for any (s in P)
* `(ce-of-set( set-of-ce(ce) ) == ce)` is true for any (ce in CE(h))

**CLARIFICATION**
Any non-empty CSS can be minimized to hold one CE only.

Additional CEs do not add substantial information to a hierarchy. They merely
increase the storage requirement of a hierarchy (hint: ancestor sets). That is,
instead of having multiple distinct CEs per set, each of which can be understood
to represent a bit of information that is unique to a set, a set should hold
only one reference to the combined data of that set.

<!-- ======================================================================= -->
## TODOs

* a tree of references
* what does a CSS allow to do?
* allow to verify that a hierarchy of sets corresponds with a node tree

if (#CSS(h) >= P) -
Because of that requirement, each set must have one or more elements, which
none of its descendant sets is allowed to have. Consequently, such a
hierarchy must have at least as many elements in V as it has sets in P
(i.e. `(#P <= #V)`).

* Recall that a root set `r in P` is the union of all of its descendant sets:
  i.e. `(#r == #V)`.
