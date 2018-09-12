
<!-- ======================================================================= -->
# Paths of vertices

Note that, in the context of this discussion, and unless specified otherwise,
all paths are by default assumed to be uni-directional and oriented according
to the corresponding relation.

<!-- ======================================================================= -->
## uni-directional paths

A path over a graph `G := (V,E)` is a sequence of vertices `p := (v1,v2,...,vk)`
where `(p in ×V^k)` such that `(xi in V)`. In addition to that, any consecutive
pair of vertices in `p` represents an edge `(e in E)` - i.e. `((vi,vi+1) in E)`
for `(i in [1,#p-1])`. Defined such way, all definitions for sequences may be
used in combination with paths (e.g. subsequence-of, prefix-of).

Note that, because a graph is defined as a binary relation, a path may also be
referred to as "a path over the graph's relation", or short as "a path over a
relation".

**Memory hook**
A path is a sequence of adjacent vertices.

<!-- ======================================================================= -->
## length of a path

* by default, `#p` refers to the vertex-length of a path

A hop/pair/edge-based view:

* `#p := (k-1)`
* i.e. the number of consecutive pairs in `p`
* aka. the edge-length of `p`

A vertex-based view:

* `#p := k`
* i.e. the number of components in `p`
* aka. the vertex-length of `p`

Degenerated paths

* `p` is the "empty path", if `(p == [])`
* `p` is a "trivial path", if `(#p == 1)`
* i.e. empty and trivial paths are seen as (degenerated) paths
* i.e. even though these have no consecutive pairs of vertices

Note that a path may in general have any/infinite length. However, in the
context of this discussion, all paths have finite length.

<!-- ======================================================================= -->
## set of paths P over G

The following is an inductive definition of the set of all possible paths that
can be formed based on the set of edges `E` of a graph `G := (V,E)`:

(0) `P0 := { () }`

That is, the empty path is used as the initial path.

(1) `P1 := { (v) | (v in V) }`

That is, `P1` holds all trivial paths.

(2) `P2 := { (a × b) | (a in P1), (b in V), ((a[#a],b) in E) }`

That is, `P2` holds all paths of vertex-length 2.

(i) `Pi := { (a × b) | (a in P(i-1)), (b in V), ((a[#a],b) in E) }`

That is, the next set of paths `Pi` for `(i > 1)` is formed from the previous
set of paths `P(i-1)` by concatenating all those vertices `b` to each path `a`
in `P(i-1)`, if there is an edge `(e in E)` such that `(e == (a[#a],b))`.

* `P := P0 + P1 + ... + P(i-1) + Pi` for `(i in [0,*])`
* `P := (union-of Pi)` for all `(i in [0,*])`
* i.e. `(E subset-of P)` - i.e. each edge `(e in E)` is a path (in `P2`).

Because of that, each graph `G` can be understood to have a set of all possible
paths `P` associated with it. Like any other binary relation, a graph can be
understood to be defined as a triplet of sets: `G := (V,E,P)`.

Note that a finite graph which has loops and/or cycles allows to form infinitely
many paths. That is, the graph's set of paths `P` may have infinitely many
elements. Consequently, the set of paths `P` has finite size, if and only if
the corresponding graph has neither loops nor cycles (see below).

<!-- ======================================================================= -->
## in, contains

A sequence of vertices can be understood to represent a path `p` in graph `G`,
if `p` is an element of the graph's set of paths `P`. In such a case, graph `G`
is understood to contain path `p`.

* `(p in P), (p in G)` := `p` is a path in `P`
* synonymous - contains, element-of

<!-- ======================================================================= -->
## aPb, p(a,b)

The following selector function can be defined:

* `(p: V×V -> P(P) )`
* `p(a,b) := { (a) }` iff `(a == b)`
* `p(a,b) := { p | (p := (a,...,b)) where (p in G) }`
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
* `aPb := (p(a,b) in G)` - if only one path is possible

Notational inaccuracy

* `aPb` may also be used instead of `p(a,b)`
* i.e. `aPb` may be used to refer to the corresponding path (or set of paths)

<!-- ======================================================================= -->
## loops, cycles

* in this discussion, a graph is assumed to have neither loops nor cycles
* (trees have by definition neither loops nor cycles)

cycles

* `(p in P)` is a cycle, if `(p == p(v,v))` for some `(v in V)`
* i.e. `p` begins and ends with the same vertex `v`
* `p` is cyclic, if `(#E(p) < #p)`
* i.e. `(p[i] == p[j])` for some `(i != j)`
* `p` is acyclic, if `(#E(p) == #p)`
* `G` is cyclic, if `P` contains a cyclic paths
* `G` is acyclic, if `P` contains no cyclic path
* i.e. all paths `(p in P)` are acyclic

Note that a path is cyclic, if it contains a vertex more than once.
That is, the corresponding vertex is presequent and subsequent to itself.

loops

* `(p in P)` is a loop, if `(p == (v,v))` for some `(v in V)`
* i.e. `p` is a cycle of vertex-length 2 (aka. edge-length 1)
* i.e. `p` is a 1-cycle

Note that an acyclic graph is also loop-less. However, an irreflexive
relation (i.e. no loops) may or may not be acyclic.

<!-- ======================================================================= -->
## direction/orientation

With each edge `(e in E)` in a graph `G := (V,E)`, a statement (i.e. meaning,
aka. semantics) is associated. The edges therefore support in general a notion
of **direction** and/or **orientation**, if the vertices of an edge are
considered to not be equal.

However, that sense of orientation is broken, if two vertices are connected
in both ways (i.e. `aPb` and `bPa`). In order for all edges to have strict
orientation, the relation `R` of a graph `G` must be anti-symmetric and
irreflexive (i.e. asymmetric). In general, `G` must be **acyclic**.

With that in mind, any path `p=(v1,v2,...)` over a graph `G` can be understood
to be **uni-directional**, if `((vi,vi+1) in G)` for all pairs of consecutive
vertices.

An uni-directional path may be referred to as **consistent with**, or **in the
direction of** `G`, if each pair `(vi,vi+1)` is an edge in `E`. In contrary to
that, a path may be referred to as being uni-directional but **inverted**, or
**antonymous**, if each pair `(vi,vi+1)` represents an edge `(e in ant(E))`.

Note that an uni-directional path (antonymous or not) has one direction only.

<!-- ======================================================================= -->
## multi-directional paths

A path may be referred to as being **multi-directional**, if it contains pairs
of consecutive vertices such that `(vi,vi+1)` and/or `(vi+1,vi)` in `G`. Put
differently, if a path contains pairs in `G` and `ant(G)` (i.e. antonymous
relation/graph).

In general: A path `(p in ×V^k)` is a sequence of vertices `p := (v1,...,vk)`
such that `(vi covered-by vi+1)` for `(i in [1,#p-1])`.

Example: In a tree of nodes `T := (N,E)`, a multi-directional path of length 3
connects a child `c` over its parent `n` with one of its siblings `s`. Hence,
and if such paths are allowed, then `c` and `s` are connected via the following
path `p(c,s) := (c,n,s)` such that `((c,n) in ant(E))` and `((n,s) in E)`.

Note that multi-directional paths have no strict/consistent orientation.

<!-- ======================================================================= -->
## reachability-based qualifiers

* covered-by := strictly-connected-to

(a connected-to b)

* `(a connected-to b)`, if `aPb` and/or `bPa`
* `a` is connected-to `b` and/or `b` is connected-to `a`
* synonymous - related-to, comparable-to
* note - connected-to is undirected

(a not-connected-to b)

* `(a not-connected-to b)`, if neither `aPb` nor `bPa`
* synonymous - disconnected-from, unrelated-with, incomparable-to

(a strictly-connected-to b)

* `(a strictly-connected-to b)`, if `aEb` and/or `bEa`
* `a` is directly connected-to `b` and/or `b` is directly connected-to `a`
* synonymous - strictly-related-to, covered-by

(a loosely-connected-to b)

* `(a loosely-connected-to b)` := connected-to, but not strictly-connected-to
* i.e. there are vertices in between `a` and `b` - i.e. `(#p > 2)`
* i.e. connected-to <-> (strictly- or loosely-connected-to)
* synonymous - loosely-related-to

(a simply/strongly-connected-to b)

* simply, if `aPb` ex-or `bPa`
* strongly, if `aPb` and `bPa`

<!-- ======================================================================= -->
## sequence-based qualifiers

(a sequent-to b)

* `(a sequent-to b)`, if `aPb` and/or `bPa`
* i.e. equivalent to connected/related/comparable
* note - "sequent-to" is undirected

(a insequent-to b)

* `(a insequent-to b)`, if neither `aPb` nor `bPa`
* i.e. equivalent to disconnected/unrelated/incomparable
* i.e. "insequent" is antonymous to "sequent"
* **TODO** - an unexpected, path-based perspective
* i.e. could use some additional thought

(a predecessor-of b)

* `(a predecessor-of b)`, if `aPb`
* i.e. predecessor-of is directed
* synonymous - presequent-to
* note - "predecessor-of" is directed

(b successor-of a)

* `(b successor-of a)`, if `bPa`
* i.e. successor-of is directed
* note - `aPb` and `bPa` may both be true
* synonymous - subsequent-to

similar definitions possible for ...

* strict/loose predecessor-of
* strictly/loosely presequent-to
* strict/loose/distant successor-of
* strictly/loosely subsequent-to

Note that, because each edge `((x,y) in E)` is a path of vertex-length 2,
two adjacent vertices can be said to be sequent to each other. That is, `x`
is (strictly) presequent to `y`, and `y` (strictly) subsequent to `x`.
