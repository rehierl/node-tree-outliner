
<!-- ======================================================================= -->
# Single associations

What effects does it have,
if node `n` is associated with section `s`?

<!-- ======================================================================= -->
## pi: s -> ni

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

A path `pa` can be defined which connects
the ancestors of node `n` with section `s`.

*  `pa := (n-k,...,n,s) in N{+}S`
* `((n-k) ... contains ...){*} (n) belongs-to (s)`

The same applies, if such a path is inverted:

* `pa' := (s,n,...,n-k) in SN{+}`
* `(s) contains (n) (... belongs-to ... (n-k)){*}`

Here, the relations used to create such a path have antonymous semantics
(i.e. `contains` vs. `belongs-to`). Such a path is said to be semantically
inconsistent.

<!-- ======================================================================= -->
## derived statements

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

A path `pd` can be defined which connects
section `s` with nodes that all are descendant to `n`:

* `pd .= (s,x,...,x+k) in SN{+}`
* `(s) contains (x) (... contains ... (x+k)){*}`

The same applies, if such a path is inverted:

* `pd' := (x+k,...,x,s) in N{+}S`
* `((x+k) ... belongs-to ...){*} (x) belongs-to s`

Here, the relations used to create such a path all have the same orientation
(i.e. superordinate-to-subordinate, or subordinate-to-superordinate)! Such a
path is said to be semantically consistent (aka. unidirectional).

<!-- ======================================================================= -->
## derived statements

(downwards):
Section `s` loosely contains any descendant of node `x`,
if section `s` strictly contains node `x`.

* `(s strictly-contains x)` and `(s loosely-contains (x+i))`
* `(s contains x)` and `(s contains (x+i))`

(upwards):
Any descendant of node `x` loosely belongs to section `s`,
if node `x` strictly belongs to section `s`.

* `(x strictly-belongs-to s)` and `((x+i) loosely-belongs-to s)`
* `(x belongs-to s)` and `((x+i) belongs-to s)`

(upwards):
Node `y` loosely belongs to section `t`, if `y` is a descendant of node `x`
and if `x` strictly belongs to `t`:

* `(y loosely-belongs-to t)`, if some `x in N` exists
  such that `(x ancestor-of y)` and `(x strictly-belongs-to t)`

Consequently, any node automatically loosely belongs to any section that
strictly contains any of its ancestors. Each node can therefore belong to
any number of sections.

These loose relationships can not be undefined because they will be established
automatically as soon as an ancestor is strictly associated with a section.

The only method to break up these loose relationships is to change the structure
of the node tree. Obviously, that is not allowed because the purpose of these
associations is ultimately to represent the tree's logical structure as is.

**Memory hook**
The `NxN` relation can be understood to define a spacial relationship (e.g.
cities on a continent). In contrary to that, the `SxN` relation can be
understood to define a logical relationship (e.g. political affiliation).

Note that, this perspective is not overly accurate because a political
affiliation may span over multiple segments (e.g. continents and/or islands)
that are separated from each other.
