
<!-- ======================================================================= -->
# Paths of vertices

Note that, in the context of this discussion, and unless specified otherwise,
all paths are by default assumed to be uni-directional and oriented according
to the relation of a graph.

<!-- ======================================================================= -->
## paths over relations

An **undirected path** over a graph `G := (V,A)` is a sequence of vertices
`p := (V1,...,vk)` such that `(p in ×V^k)` - i.e. `(xi in V)`. In addition
to that, any consecutive pair of vertices in `p` represents an arc `(a in A)`
- i.e. `({vi,vi+1} in A)`.

A **directed path** over a graph `G := (V,E)` is a sequence of vertices
`p := (v1,...,vk)` such that `(p in ×V^k)` - i.e. `(xi in V)`. In addition
to that, any consecutive pair of vertices in `p` represents an edge `(e in E)`
- i.e. `((vi,vi+1) in E)`.

Defined such way, all definitions for sequences can be used in combination
with paths (e.g. subsequence-of, prefix-of).

Note that, because a (directed) graph is defined as a binary relation, a
(directed) path may also be referred to as "a path over the graph's relation",
or short as "a path over a relation".

**Memory hook**
A path is a sequence of adjacent vertices.

<!-- ======================================================================= -->
## direction/orientation

With each edge `(e in E)` in a graph `G := (V,E)`, a statement (i.e. meaning,
aka. semantics) is associated. Because the vertices of an edge are understood
to be un-equal, the edges support in general a notion of **direction** and/or
**orientation**.

However, that sense of orientation is broken, if two vertices are connected
in both ways (i.e. `aPb` and `bPa`). Because of that, and in order for a graph
to have a strict orientation, a graph must be acyclic. (Note that each acyclic
graph is by definition an oriented graph, but not necessarily vice versa).

With that in mind, any path directed `p=(v1,v2,...)` over an (acyclic) graph
`G` can be understood to be **uni-directional**, if `((vi,vi+1) in G)` for all
pairs of consecutive vertices.

An uni-directional path may be referred to as **consistent with** (or **in the
direction of**) `G`, if each pair `(vi,vi+1)` is an edge in `E`. In contrary to
that, a path may be referred to as being uni-directional but **inverted** (or
**antonymous**), if each pair `(vi,vi+1)` represents an edge in the inverted
(aka. antonymous) graph - i.e. `(e in ant(G))`.

A path may be referred to as being **multi-directional**, if it contains pairs
of consecutive vertices such that `(vi,vi+1)` and/or `(vi+1,vi)` in `G`. Put
differently, if a path contains pairs in `G` and `ant(G)`.

Note that an uni-directional path (antonymous or not) may be said to have one
direction only. In contrary to that, a multi-directional path has no consistent
orientation.

In general: A multi-directional path `(p in ×V^k)` is a sequence of vertices
`p := (v1,...,vk)` such that `(vi covered-by vi+1)` for `(i in [1,#p-1])`.

Example: In a tree of nodes `T := (N,E)`, a multi-directional path of length
3 connects a child `c`, over its parent `n`, with one of its siblings `s`.
Hence, if such paths are allowed, then `c` and `s` are connected via a path
`p(c,s) := (c,n,s)` such that `((c,n) in ant(E))` and `((n,s) in E)`.

<!-- ======================================================================= -->
## length of a path

* by default, `#p` is used to refer to the vertex-length of a path
* i.e. `(#p == k)` if `p := (v1,...,vk)`

A hop/pair/edge-based view

* `#p := (k-1)`
* i.e. the number of consecutive pairs in `p`
* aka. the edge-length of `p`

A vertex-based view

* `#p := k`
* i.e. the number of components in `p`
* aka. the component-length or vertex-length of `p`

Note that a path may in general have any (even infinite) length. However, in
the context of this discussion, all paths are assumed to have finite length.

<!-- ======================================================================= -->
## set of paths P

The following is an inductive definition of the set of all possible paths that
can be formed based on the set of edges `E` of a graph `G := (V,E)`:

(0) `P0 := { () }`

That is, `P0` only contains the empty path `p := ()` (i.e. vertex-length 0).

(1) `P1 := { (v) | (v in V) }`

That is, `P1` only contains all trivial paths `p := (v)` (i.e. vertex-length 1).

(2) `P2 := { (a × b) | (a in P1), (b in V), ((a[#a],b) in E) }`

That is, `P2` holds all paths of vertex-length 2.
Hence, `P2` is identical to the set of edges `E`.

(i) `Pi := { (a × b) | (a in P(i-1)), (b in V), ((a[#a],b) in E) }`

That is, the next set of paths `Pi` for `(i > 1)` is formed from the previous
set of paths `P(i-1)` by concatenating all those vertices `b` to each path `a`
in `P(i-1)`, if there is an edge `(e in E)` such that `(e == (a[#a],b))`.

* `P := P0 + P1 + ... + P(i-1) + Pi` for `(i in [0,*])`
* `P := (union-of Pi)` for all `(i in [0,*])`
* note - `(E subset-of P)`

Because of that, each graph `G` can be understood to have a set of all possible
paths `P` associated with it. Like any other binary relation, a graph can be
understood to be seen as a triplet of sets: `G := (V,E,P)`.

Note that any path in `(P0 + P1)` may be referred to a "degenerated path".
That is, because such a path does not contain any consecutive pair of vertices.

Note that, if a discussion is with regards to multiple graphs, a specific set
of paths `P` may be clarified as `P[E]` or `P[G]`, which needs to be read as
"the set of paths `P`, induced by the set of edges `E` in graph `G`".

Note that a finite graph, that has loops and/or cycles, allows to form an
infinite number of paths. That is, the graph's set of paths `P` has infinitely
many elements. The set of paths `P` therefore has finite size, if and only
if the corresponding graph is acyclic.

<!-- ======================================================================= -->
## in, contains

A sequence of vertices can be understood to represent a path `p` in graph `G`,
if `p` is an element of the graph's set of paths `P`. In such a case, graph `G`
is understood to contain path `p`.

* `(p in P), (p in P[G]), (p in G)` := `p` is a path in `G`
* synonymous - contains, element-of

<!-- ======================================================================= -->
## aPb, p(a,b)

The following selector function can be defined:

* `(p: V×V -> P(P) )`
* `p(a,b) := { (a) }` iff `(a == b)`
* `p(a,b) := { p | (p := (a,...,b)) and (p in G) }`
* i.e. the set of paths in `G` that begin in `a` and end in `b`

Note that, in cases where a graph has exactly one such path, `p(a,b)` is seen
to return a single path `p := (a,...,b)` rather than a set of paths. That is,
`p()` is understood to be defined as `(p: V×V -> P)`.

* `(p: V×P(V) -> P(P) )`
* `p(a,B) := { p(a,b) | for all (b in B) and (p in R) }`
* i.e. the set of paths in `G` that begin in `a` and end in a vertex in `B`

Indicator function

* `aPb := (p(a,b) != {})` - if multiple paths are possible
* i.e. one or more paths `p` exist that begin in `a` and end in `b`
* `aPb := (p(a,b) in G)` - if only one such path is possible

Notational inaccuracy

* `aPb` may also be used instead of `p(a,b)`
* i.e. `aPb` may be used to refer to the corresponding path (or set of paths)
