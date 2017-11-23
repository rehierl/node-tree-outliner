
<!-- ======================================================================= -->
# Single associations

What effects does it have,
if node `n` is associated with section `s`?

<!-- ======================================================================= -->
## pi := s -> nx

```
r x ... x (n:s) x ...
```

Section `s in S` strictly contains node `n` because it is directly connected
with it. That statement is however a direct result of the `SxN` relation and,
as such, does not state anything new.

<!-- ======================================================================= -->
## pa: (n-k) -> s

```
r x ... x (n-k) x ... x (n-1) x (n:s) x ...
```

A path `pa` can be defined that connects
the ancestors of node `n` with section `s`.

*  `pa := (n-k,...,n,s) in N{+}S`
* `(n-k) ... contains ... (n) belongs-to (s)`

The same applies, if such a path is inverted:

* `pa' := (s,n,...,n-k) in SN{+}`
* `(s) contains (n) ... belongs-to ... (n-k)`

Here, the relations used to create such a path have antonymous semantics
(i.e. `contains` vs. `belongs-to`). Such a path is said to be inconsistent.

<!-- ======================================================================= -->
## conclusion

The reason why no clear conclusion can be drawn is, that the ancestors of node
`n` may have any number of nodes that are descendant to the root `r`, but that
are not ancestral (i.e. not in `prefixOf(pa)`) to it. Hence, a path `p` could
be defined which connects some node `o` with section `s`

* `p := (o,...,r,...,n-k,...,n,s) in N{+}S`
* `(o) ... belongs-to ... (r) ... contains ... (nx) belongs-to s`

Obviously, such a path would be even more inconsistent.

<!-- ======================================================================= -->
## pd: s -> (n+k)

```
r x ... x (x:s) x (x+1) x ... x (x+k) x ...
                x (y+1) x ... x (y+l) x ...
```

A path `pd` can be defined that connects
section `s` with nodes that all are descendant to `n`:

* `pd .= (s,x,...,x+k) in SN{+}`
* `(s) contains (x) ... contains ... (x+k)`

The same applies, if such a path is inverted:

* `pd' := (x+k,...,x,s) in N{+}S`
* `(x+k) ... belongs-to ... (x) belongs-to s`

Here, the relations used to create such a path have equivalent semantics!
Such a path is said to be consistent.

<!-- ======================================================================= -->
## conclusion

Because of that, a section that strictly contains a node does also loosely
contain any descendant of that node:

* `(s contains x)` and `(s contains (x+i))`

Likewise, if a node strictly belongs to a section, then
any of its descendants loosely belong to the same section.

* `(x belongs-to s)` and `((x+i) belongs-to s)`

Consequently, any node automatically loosely
belongs to any section to which any of its ancestors strictly belong.

* `(y belongs-to s)`, if some `x in N` exists
  such that `(x ancestor-of y)` and `(x belongs-to s)`

These loose relationships can not be undefined because they will be established
automatically as soon as any of its ancestors is strictly associated with some
section.

The only method to break up these kind of loose relationships is to change the
structure of the node tree. Obviously, that is not allowed because the purpose
of these associations is ultimately to represent the tree's structure as is.

**TODO** - points towards a hierarchy of sections
