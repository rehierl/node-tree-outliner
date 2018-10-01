
<!-- ======================================================================= -->
# Semantics of a graph

Without semantics, any graph/relation is more or less a meaningless set of
tuples. And because graphs are used to represent relationships between vertices,
semantics are in general implicitly associated with each graph. The following
content therefore attempts to grasp the formal aspects related to the semantics
of a graph.

* (/see/ "semantics" in "mixed" /)

<!-- ======================================================================= -->
## a general introduction

Generally speaking, an entity `e` that has semantics can be understood to be
accompanied by an expression that associates meaning with the entity. Because
of that, some operation is assumed to exist that can be used to retrieve an
entity's semantical expression.

* `(sem: Entity -> Expression)` where `sem(e)` returns the expression of `e`
* `sem(e)` may be defined as `sem(e) := <expression>`,

Such an expression is in general defined as a predicate. That is, for a given
entity, the corresponding expression is understood to return a single boolean
value such that it is true, if the semantical expression applies to the given
entity.

In the context of a relation `R`, the smallest relevant unit, that may
be associated with a semantical expression, are its edges `(e in E)`.
Some examples of semantical expressions are:

For edge `e := (a,b)`, one might define `sem(e)` as:

0. `a` is equal to `b`
1. `a` is smaller than `b`
2. `a` is subsequent to `b`
3. `a` is an element of `b`
4. `a` is a subset of `b`
5. `a` is a multiple of `b`
6. `b` is a multiple of `a`

For edge `e := (a,b,c)`, one might define `sem(e)` as:

7. `a` and `b` are (biological) parents of `c`
8. `c` is the sum of `a` and `b` (i.e. `(a + b == c)`)
9. `a` is the sum of `b` and `c` (i.e. `(a == b + c)`)

Note that expressions (5) and (6), as well as (8) and (9), are distinct from
one another. That is, the order of the elements in an expression is relevant
to the semantics of the corresponding entity/edge.

Note that the characteristic function of a relation `R()` merely states that
the vertices of the corresponding edge are in some way related. That is, the
result of a relation's characteristic function does, strictly speaking, not
allow to determine why the vertices of an edge are adjacent.

<!-- ======================================================================= -->
## semantics of an edge/graph

A graph `G := (V,E)` represents the relationships between its adjacent vertices.
Because of that, an expression is expected to exist for each edge that explains
why both of its endpoints are adjacent to each other. Such a reason will be
referred to as the **semantics of an edge**.

* `sem(e) := (x multiple-of y)` for some edge `((x,y) in E)`

In general, the semantics of two distinct edges `e1` and `e2` in a graph are
not required to correspond with each other. That is, the semantics of two edges
in the same graph may be distinct (for whatever reason).

* `sem(e1) := (x multiple-of y)` for `e1 := (x,y)`
* `sem(e2) := (u divisible-by v)` for `e2 := (u,v)`

Because of that, a graph can be understood to be associated with a set of
tuples that provides a mapping between an edge and its semantics.

* `G := (V,E,S)` where `S` could be defined as follows
* `S := { (e,s) | (e in E) and (s == sem(e)) }`

Based on that, the `sem()` operation can be defined as follows:

* `(sem: E -> Expression)`, where `(sem(e) == s)` if `((e,s) in S)`
* i.e. `sem(e)` returns the semantics of a given edge

A graph may be referred to as having a **homogenous set of edges**, if the
semantics of an edge is identical to the semantics of all the other edges.
Conversely, a graph is said to have a **heterogenous set of edges**, if that
is not the case. Put differently, a homogenous set of edges may be understood
to contain **edges of the same sort**.

* `E` is homogenous, if `(sem(e) == sem(f)` for all pairs of edges `(e,f in E)`
* `E` is heterogenous, if `(sem(e) != sem(f)` for a pair of edges `(e,f in E)`

In the context of this discussion, all graphs are expected to have homogenous
sets of edges. Because of that, the **semantics of a graph** `sem(G)` is said
to be the common semantics of its edges `sem(e)`.

* `(sem(G) == sem(e))` for all edges `(e in E)`

Note that the semantics of a graph, that has a heterogenous set of edges, is
strictly speaking undefined.

Note that, in addition to "homogenous vs. heterogenous", one could also speak
of a graph as having **mixed semantics** (if `E` is heterogenous) vs. a graph
that has **uniform semantics** (if `E` is homogenous).

<!-- ======================================================================= -->
## index-bound semantics

Each vertex in an edge has a specific role in the semantical expression of an
edge. Because of that, some means is required to identify the role of a vertex.

* `e := (1,3)` and `sem(e) := (x multiple-of y)`

The issue in this example is that a tuple does not strictly allow to identify
which vertex maps to `x` and which vertex maps to `y`, or vice versa. However,
a non-empty tuple, as a sequence of vertices, has a first and a last element.
As such, a tuple comes with a mapping of indexes to its elements. Because of
that, the semantics of an edge is implicitly **bound to the indexes of its
vertices**.

* `sem(f) := (f[1] multiple-of f[2])` if edge `(f in E)`
* `sem(g) := (g[2] multiple-of g[1])` if edge `(g in E)`

Both of these semantics are therefore distinct (i.e. `(sem(f) != sem(g))`).

<!-- ======================================================================= -->
## consistently oriented semantics

Because each edge `(x,y)` in a (directed) graph is defined as a tuple of two
vertices, each edge has a 1st and a 2nd vertex. As such, each edge is understood
to be directed from its 1st vertex `x` to its 2nd vertex `y` (i.e. `(x -> y)`),
which is why the edges in a graph may be referred to as being **oriented edges**.

* `dir(e) := (x -> y)` for `(e in E)` and `(e := (x,y))`

Similar to the orientation of an edge, the semantics of an edge may provide its
own sense of orientation (i.e. **oriented semantics**), if both vertices are
considered to be unequal.

For example, one vertex in an edge may be considered to be super-ordinate to the
other. Put differently, one vertex is considered to be sub-ordinate to the other.

Note that the semantics of the above edges `f` and `g` are oriented in opposite
directions. That is, the orientation of `sem(f)` corresponds with edge `f`. In
contrary to that, `sem(g)` is oriented against edge `g`.

* `dir(sem(f)) := (x -> y)`, if `(f == (x,y))`
* `dir(sem(g)) := (x <- y)`, if `(g == (x,y))`

Because of that, an edge `e` is said to have **consistently oriented semantics**,
if the orientation of its semantics `sem(e)` corresponds with the orientation
of its edge (e.g. `sem(f)`). Conversely, `e` is said to have **inconsistently
oriented semantics**, if that is not the case.

Likewise, the set of edges `E` is said to have consistently oriented semantics,
if all of its edges have consistently oriented semantics. Conversely, `E` is
said to have inconsistently oriented semantics, if that is not the case.

Similar to that, the semantics of a graph `G` is said to have consistently
oriented semantics, if its homogenous set of edges has consistently oriented
semantics. Conversely, `G` is said to have inconsistently oriented semantics,
if that is not the case.

Note that a graph that has mixed semantics can not be said to have consistently
oriented semantics because the graph's semantics is undefined. If applicable,
one could however still refer to its set of edges as being "a heterogenous set
of edges that has consistently (or inconsistently) oriented semantics".

<!-- ======================================================================= -->
## general remarks

Note that, in the context of this discussion, a graph is in general expected to
have a consistently oriented homogenous set of edges. All graphs are therefore
expected to have a semantical expression that applies to all of its edges.

Note that two distinct graphs `G` and `H`, that are based upon the same sort
of vertices, and that have the same semantics, may be referred to as being
**graphs of the same sort** (i.e. `(V(G) ~ V(H))` and (`(sem(G) == sem(H))`).
(Note that `~` needs to be understood to compare the types of both sets).

Note that, if an operation is defined for two input graphs, then both graphs
are implicitly expected to be of the same sort. Because of that, operations
may only be applicable after the execution of appropriate conversions.

<!-- ======================================================================= -->
## converse, transpose (°)

The standard definition of a converse graph `G°` is defined as follows:

* `G° := (V,E°)` such that `E° := { (b,a) | aEb }`
* i.e. the order of vertices in each edge is turned upside-down

Based on that definition, an operation can be defined which returns the
converse graph `G°` of a graph `G`:

* `(G°: Graph -> Graph)`, where `G°(G)` returns the converse `G°` of `G`
* `conv(G), := G°(G)` - `conv(conv(G)) <-> G`

Note that the definition does not state anything about the semantics of the
converse graph. That is, this operation only focuses on "flipping" all edges.

<!-- ======================================================================= -->
## converse semantics

Assumed that the semantics of a given graph `sem(G)` would be defined as
`(p parent-of c)` where each edge would be a tuple in the following order
`(e := (p,c))`, then the semantics of its edges would have to be strictly
defined as `sem(e) := (e[1] parent-of e[2])`.

* `(p,c)` in `G` => `(e[1] parent-of e[2])` => `(p parent-of c)`
* note - `sem(e)` is oriented in the direction of `dir(e)`

If such a graph would have to be conversed according to the above definition,
then, without further change, the graph's initial semantics could not apply
to its converse:

* `(c,p)` in `G°` => `(e[1] parent-of e[2])` => `(c parent-of p)` (error)

Obviously, the converse operation also needs to adjust the semantics of the
converse graph `G°`. That is because the order of components in the semantical
expression of `G°` would end up being broken. To resolve this issue, one also
needs to "adjust" the semantics of `G°`.

* `(c,p)` in `G°` => `(e[2] parent-of e[1])` => `(p parent-of c)` (ok)
* note - `sem(e)` is oriented against the direction of `dir(e)` (not quite ok)

Even though, the semantical expression now applies to the flipped edges, the
edges end up having inconsistently oriented semantics. In a context where the
semantics of a graph are of no importance, such an adjustment might seem to be
sufficient. However, if the semantics of a given graph are relevant, then that
aspect needs to be fixed as well.

In order to fix both of the above aspects, one needs to replace the semantics
of an initial graph with semantics that has the opposite meaning. That is, the
semantics of the initial graph needs to be replaced by its relational antonym
(aka. **converse semantics**, antonymous semantics).

* `(c,p)` in `G°` => `(e[1] child-of e[2])` => `(c child-of p)` (ok)

**Memory hook**
A converse/antonymous graph needs converse/antonymous semantics.

<!-- ======================================================================= -->
## general remarks

The following is a short list of possible, converse semantics:

* parent-of vs. child-of
* contains vs. element-of
* superset-of vs. subset-of
* subsequent-to vs. presequent-to

Note that, if the converse of a graph needs to be created in the context of
this discussion, then the converse graph is expected to have converse semantics.
That is, in the context of the following discussion, a converse graph includes
flipped edges and flipped semantics.
