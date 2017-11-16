
<!-- ======================================================================= -->
# Graph Theory

* used to model pairwise relations between objects
* in general, sets of vertices/nodes that are connected by edges

definition

* `G := (V,E)` <=> `R := (A,B,G)` if `(A == B)`
* `e := (a,b)` tuples are referred to as edges
* `G` is in general assumed to not be empty, `E` may be empty
* a vertex `a` may not be an end to any edge, i.e. there is no `aEb` or `bEa`

<!-- ======================================================================= -->
## mixed definitions

* `order(G) := #V`
* `size(G) := #E`
* `in-degree(v) := #({ (a,v) : aEb })`
* `out-degree(v) := #({ (v,b) : vEb })`
* `degree(v) := in-degree(v) + out-degree(v)`,
  i.e. loops on `v` are counted twice
* `degree(a,b) := #({ (a,b) : aEb }) + #({ (b,a) : bEa })`
* symmetric => if `aEb`, then also `bEa`
* loops => if `aEa`
* link => if `aEb` for `(a != b)`
* planar => can draw `G` without intersecting edges
* tree => connected and no cycles

**TODO** - cycles

<!-- ======================================================================= -->
## adjacent to (~)

adjacent vertices

* `(a ~ b)` is true, if `aEb` or `bEa`
* `(a adjacent-to b) := (a ~ b)`
* `a` and `b` are adjacent to one another

adjacent edges

* e.g. `(a,b)` and `(b,c)` share the common vertex `b`
* also consecutive edges

<!-- ======================================================================= -->
## connected

vertices

* two vertices are connected, if
  a path exists that connects them with each other
* strongly connected vs. weakly connected
* connected <=> not disconnected

graph

* `G` has no unreachable vertices
* a path exists between any two vertices
* connected <=> not disconnected

<!-- ======================================================================= -->
## simple/multigraph

multiple edges

* if `(#({ (a,b) : aEb }) == 2)` for some vertices
* also multi-edges

multigraph

* undirected, may have multi-edges
* in such a case, `G` must be a multi-set

simple graph

* undirected, no multi-edges and no loops

<!-- ======================================================================= -->
## directed/undirected

* directed/undirected is determined by the underlying semantics
* similar for directed/undirected edges

undirected

* if `aEb`, then `G` can be seen to also contain `bEa`
* i.e. `((a,b) == (b,a))` is meant to be true
* i.e. edges have no specific orientation
* i.e. essentially turns edges into 2-element sets - `{a,b}`

directed, digraph

* if `aEb` must be understood to not include `bEa`,
  unless `bRa` is itself explicitly mentioned to be included
* `(a,b)` is also referred to `arrow` from `a` to `b`
* `a` reflects the arrow's tail, and `b` the arrow's `head`
* `b` is a direct successor of `a`
* `a` is a direct predecessor of `b`
* `b` is a successor-of and reachable-from `a`,
  if a path exists that leads from `a` to `b`

oriented

* if `(degree(a,b) <= 1)` for any two vertices `a` and `b`
* `a` and `b` are either not strictly related, or `(aEb xor bEa)` is true

mixed

* some edges are directed, others are undirected
