
<!-- ======================================================================= -->
# Semantics of a graph

Without semantics, any graph/relation is more or less a meaningless set of
tuples. And because graphs are used to represent relationships between vertices,
semantics are in general implicitly associated with each graph. The following
content therefore attempts to grasp the formal aspects related to the semantics
of a graph.

<!-- ======================================================================= -->
## a general introduction

Generally speaking, an entity `e` that has semantics can be understood to be
accompanied by an expression that associates meaning with the entity. Because
of that, an operation exists that can be used to retrieve the corresponding
expression.

* `(sem: Entity -> Expression)` where `sem(e)` returns the expression of `e`
* `sem(e)` may be defined as `sem(e) := <expression>`,

Such an expression is in general defined as a predicate. That is, for a given
entity, the corresponding expression is understood to return a single boolean
value such that it is true, if the expression applies to the given entity.

In the context of a relation `R`, the smallest relevant units, that may be
associated with a semantical expression, are its edges `(e in E)`. Some
examples are:

For `e := (a,b)`, one might define `sem(e)` as:

0. `a` is equal to `b`
1. `a` is smaller than `b`
2. `a` is subsequent to `b`
3. `a` is an element of `b`
4. `a` is a subset of `b`
5. `a` is a multiple of `b`
6. `b` is a multiple of `a`

For `e := (a,b,c)`, one might define `sem(e)` as:

7. `a` and `b` are (biological) parents of `c`
8. `c` is the sum of `a` and `b` (i.e. `(a + b == c)`)
9. `a` is the sum of `b` and `c` (i.e. `(a == b + c)`)

Note that the expressions (5) and (6), as well as (8) and (9), are distinct.
That is, the order of the elements in statement is relevant to the semantics
of an entity/edge.

Note that the characteristic function of a relation `R()` merely states that
the vertices of the corresponding edge are in some way related. That is, the
result does strictly speaking not allow to determine why the vertices of an
edge are adjacent.

<!-- ======================================================================= -->
## semantics of an edge/graph

A graph `G := (V,E)` represents the relationships between its adjacent vertices.
Because of that, an expression is expected to exist for each edge, that explains
why both of its endpoints are adjacent to each other. Such a reason will be
referred to as the **semantics of an edge**.

* `sem(e) := (x multiple-of y)` for some edge `(e in E)`

In general, the semantics of two distinct edges `e1` and `e2` in a graph are
not required to correspond with each other. That is, the semantics of two edges
in the same graph may be distinct (for whatever reason).

* `sem(e1) := (x multiple-of y)` for `e1 := (x,y)`
* `sem(e2) := (u divisible-by v)` for `e2 := (u,v)`

Because of that, a graph can be understood to be associated with a set of
tuples that provides a mapping between an edge and its semantics.

* `G := (V,E,S)` where `S` is defined as follows
* `S := { (e,s) | (e in E) and (s == sem(e)) }`
* `SEM := { s | ((e,s) in S) }`
* i.e. the set of all semantical expressions

Based on that, the following operation can be defined:

* `(sem: E -> Expression)`, where `(sem(e) == s)` if `((e,s) in S)`
* i.e. `sem(e)` returns the semantics of a given edge

A graph may be referred to as having a **heterogenous set of edges**, if it
contains edges that have distinct semantics. In contrary to that, a graph
is said to have a **homogenous set of edges**, if the semantics of an edge
corresponds with the semantics of all the other edges. Put differently, a
homogenous set of edges can be understood to hold **edges of the same sort**.

* `E` is heterogenous, if `(sem(e) != sem(f)` for a pair of edges `(e,f in E)`
* `E` is homogenous, if `(sem(e) == sem(f)` for all pairs of edges `(e,f in E)`
* in short: homogenous if `(#SEM == 1)`, heterogenous if `(#SEM > 1)`

In the context of this discussion, all graphs are expected to have homogenous
sets of edges. Because of that, the **semantics of a graph** `sem(G)` is said
to be the common semantics of its edges `sem(e)`.

* `(sem(G) == sem(e))` for all edges `(e in E)`

Note that the semantics of a graph, that has a heterogenous set of edges, is
strictly speaking undefined. One could however still speak of a graph that
has **mixed semantics** (if `E` is heterogenous) vs. a graph that has
**consistent semantics** (if `E` is homogenous).

<!-- ======================================================================= -->
## index-bound semantics

<!-- ======================================================================= -->
## consistent semantics

Any edge `(x,y)` in a (directed) graph is defined as a tuple of two vertices.
Because of that, each edge has a 1st and a 2nd vertex. As such, each edge is
understood to be directed from its 1st vertex `x` to its 2nd vertex `y` (i.e.
`(x -> y)`), which is why the edges in a directed graph may be referred to as
being oriented (i.e. **oriented edges**).

* `dir(e) := (x -> y)` for `(e in E)` and `(e == (x,y))`

Furthermore, each vertex in an edge is understood to have a specific role in
the expression of an edge. Because of that, some means to identify the role
of a vertex is required to exist for the semantics to make sense.

* `e := (1,3)` and `sem(e) := (x multiple-of y)`

The issue here is that there is no definition as to which element in a given


And because each
edge is defined as a tuple of elements, the only means available is via the
index of a vertex. That is, the semantics of an edge is implicitly **bound to
the indexes of its vertices**.

* `sem(f) := (f[1] multiple-of f[2])` if edge `(f in E)`
* `sem(g) := (g[2] multiple-of g[1])` if edge `(g in E)`
* note - both semantics are distinct (i.e. `(sem(f) != sem(g))`)

Similar to the orientation of an edge, the semantics of an edge may provide its
own sense of orientation (i.e. **oriented semantics**), if both vertices are
considered to be unequal. For example, one vertex in an edge may be considered
to be super-ordinate to the other. Consequently, one vertex is also considered
to be sub-ordinate to the other.

Note that the semantics of the above edges `f` and `g` are oriented differently.
That is, the orientation of `sem(f)` corresponds with edge `f`, whereas `sem(g)`
is oriented against edge `g`.

* `dir(sem(f)) := (x -> y)`, if `(f == (x,y))`
* `dir(sem(g)) := (x <- y)` or `(y -> x)`, if `(g == (x,y))`

Because of that, an edge `e` is said to be have **consistently oriented
semantics**, if the orientation of its semantics `sem(e)` corresponds with
the orientation of its edge (e.g. `sem(f)`). Conversely, `e` is said to
have **inconsistently oriented semantics**, if that is not the case.

Likewise, the set of edges `E` is said to have consistently oriented semantics,
if all of its edges have consistently oriented semantics. Conversely, `E` is
said to have inconsistently oriented semantics, if that is not the case.

Similar to that, the semantics of a graph `G` is said to have consistently
oriented semantics, if its homogenous set of edges has consistently oriented
semantics. Conversely, `G` is said to have inconsistently oriented semantics,
if that is not the case.

Note that a heterogenous set of edges in a graph may have consistently oriented
semantics. However, the corresponding graph can not be said to have consistently
oriented semantics, as the graph's semantics is undefined.

<!-- ======================================================================= -->
## general remarks

Note that, in the context of this discussion, a graph is in general expected to
have its semantics `sem(G)` oriented according to its homogenous set of edges.

Note that two distinct graphs `G` and `H`, that are based upon the same sort
of vertices, and that have identical semantics, may be referred to as being
**graphs of the same sort** (i.e. `(V(G) ~ V(H))` and (`(sem(G) == sem(H))`).
(Note that `~` needs to be understood to compare the types of both sets).

Note that, if an operation is defined for two input graphs, then both graphs
are implicitly expected to be of the same sort. Because of that, operations
may only be applicable after the execution of appropriate conversions.

<!-- ======================================================================= -->
## converse, inverse (°)

The converse/inverse graph `G°` of a graph `G` is defined as follows:

* `G° := (V,E°)` such that `E° := { (b,a) | aEb }`
* i.e. the order of vertices in each edge is turned upside-down

Based on that definition, an operation can be defined which returns the
inverse graph `G°` of a graph `G`:

* `(G°: Graph -> Graph)`, where `G°(G)` returns the inverse `G°` of `G`
* `conv(G), inv(G) := G°(G)`
* `inv(inv(G)) <-> G`

Note that this operation does not state anything about the semantics of the
inverted graph. That is, this operation only focuses on "flipping" all edges.

<!-- ======================================================================= -->
## inverse semantics?

Assumed that the semantics of a given graph `sem(G)` would be defined as
`(p parent-of c)` where each edge would be tuple in the following order
`(e := (p,c))`, then the semantics of its edges would have to be strictly
defined as `sem(e) := (e[1] parent-of e[2])`.

Because of that, if such a graph would have to be inverted according to the
above operation, then the graph's semantics could not apply to its inverse:

* `(p,c)` in `G` => `(e[1] parent-of e[2])` => `(p parent-of c)`
* note - `dir(e) := (p -> c)` and `dir(sem(e)) := (p -> c)`
* `(c,p)` in `G°` => `(e[1] parent-of e[2])` => `(c parent-of p)` (!!)

Obviously, the inverse operation also needs to adjust the semantics of the
inverse graph `G°`. That is because the order of components in the semantical
expression of `G°` would end up being broken. In order to resolve this
inconsistency, one would also have to "fix" the semantics of `G°`.

* `(c,p)` in `G°` => `(e[2] parent-of e[1])` => `(p parent-of c)`
* note - `dir(e) := (c -> p)` but `dir(sem(e)) := (c <- p)` (!!)

Even though, the semantical expression would now apply to the inverted edges,
the edges would now inconsistently oriented semantics. In a context where the
semantics of a graph are of no importance, such an adjustment might seem to be
sufficient. However, if the semantics of a given graph are relevant, then the
resulting inconsistently oriented semantics needs to be fixed as well.

<!-- ======================================================================= -->

Strictly speaking, the reason as to why two vertices are adjacent in `G` no
longer applies to the same vertices in its inverse. Because of that, inverting
a given graph needs to be 

clarification

* inverting a relation usually drops the initial semantics
* the inverted relation has no meaning under the initial semantics
* that is because the order of elements has changed

<!-- ======================================================================= -->
## semantics

the order of elements is relevant to the semantics of a relation

* `R in (A × B × C)` := `c` is the sum of `a` and `b`
* i.e. the 3rd element is the sum of the 1st and 2nd element
* not - `inv(R) in (C × B × A)` => `a` is the sum of `c` and `b`
* but - `inv(R) in (C × B × A)` => `c` is the sum of `a` and `b`
* i.e. the 1st element is the sum of the 2nd and 3rd element
* e.g. `(1,2,3)` vs. `(3,2,1)`

<!-- ======================================================================= -->
## antonymous semantics/graph

Given a graph `G := (V,E)`, associated with the semantics `sem(e)`, then
:= (e[1]

examples

* parent-of <=> child-of
* contains <=> element-of
* super-set-of <=> sub-set-of
* super-sequence-of <=> sub-sequence-of

<!-- ======================================================================= -->
## antonymous relation

relation `S` is antonymous to `R`

* `S := ant(R)`, if `(S == inv(R))` and
* `sem(S)` is antonymous to `sem(R)`

if `S` is antonymous to `R`, then `R` is also antonymous to `S`

* `(S == ant(R)) <=> (R == ant(S))`

examples for `R,S in (A × B)` that have antonymous semantics

* assume `R:=(A,B,G)` and `S:=(B,A,G°)`
* `R` := (`a` is a subset of `b`), and
  `S` := (`b` is a superset of `a`)
* `R` := (`a` contains `b`), and
  `S` := (`b` is an element of `a`)
* `R` := (`a` divides `b` without remainder), and
  `S` := (`b` is a multiple of `a`)

examples for `R,S in (A × B × C)` that have antonymous semantics

* assume `R := (A,B,C,G)` and `S := (C,B,A,G)`
* `R` := (`a` and `b` are the biological parents of `c`), and
  `S` := (`c` is a biological child of `b` and `a`)

`R` and `inv(R)` are not necessarily antonymous to each other

* assume `R := (A,B,C,G)` and `T := (C,B,A,G) := inv(R)`
* `R` := (set `c` is the intersection of sets `a` and `b`) =: `T`
* where `(R: (A,B) -> C)` and `(T: C -> (B,A))`

**Memory hook**
Antonymous relations require antonymous semantics.
