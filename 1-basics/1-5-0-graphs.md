
<!-- ======================================================================= -->
# Graph Theory

* used to model pairwise relations between objects
* in general, sets of vertices/nodes that are connected by edges
* a binary relation `R := (A,A,G)` defines a directed graph

definition

* `G := (V,E)` <=> `R := (A,B,G)` if `(A == B)`
* `e := (a,b)` tuples are referred to as edges
* `G` is in general assumed to not be empty, `E` may be empty
* a vertex `a` may not be an end to any edge, i.e. there is no `aEb` or `bEa`

basic definitions

* `order(G) := #V`
* `size(G) := #E`
* `in-degree(v) := #({ (a,v) : aEb })`
* `out-degree(v) := #({ (v,b) : vEb })`
* `degree(v) := in-degree(v) + out-degree(v)`,
  i.e. loops on `v` are counted twice
* `degree(a,b) := #({ (a,b) : aEb }) + #({ (b,a) : bEa })`
* symmetric => if `aEb`, then also `bEa`
* loops => `aEa`
* link => `aEb` for `(a != b)`
* planar => can draw `G` without intersecting edges
* tree => connected with no cycles

<!-- ======================================================================= -->
## adjacent to (~)

adjacent vertices

* `(a ~ b), (a adjacent-to b)` is true, if `aEb` or `bEa`
* `a` and `b` are adjacent to one another
* synonymous - adjacent, strictly related

adjacent edges

* e.g. `e1 := (a,b)` and `e2 := (b,c)`
* adjacent/consecutive edges share the common vertex

<!-- ======================================================================= -->
## simple/multigraph

multiple edges

* if `(#({ (a,b) : aEb }) == 2)` for some vertices
* also multi-edges

multigraph

* undirected and may have multi-edges
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
* `(a,b)` is also referred to "arrow" from `a` to `b`
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

<!-- ======================================================================= -->
## path

* directed graph, digraph => directed path, dipath
* dipath => all edges in the same direction

common definition

* `path := (v0,e0,v1,e2,v2,...,v(n-1),e(n-1),vn)`
* a path is a trail in which all vertices are distinct
* a trail is a walk without repeated edges
* a walk is an alternating sequence of vertices and edges
* `G` is directed => `ei` connects `vi` with `v(i+1)`

miscellaneous

* vertex-independent paths := `p1` and `p2` have no vertex in common
* edge-independent paths := `p1` and `p2` have no edge in common
* vertex-independent => edge-independent
* distance between vertices := length of shortest path `(p1,p2)`
* diameter of a connected graph := length of longest path

<!-- ======================================================================= -->
## connected

vertices

* two vertices are connected, if
  a path exists that leads from one vertex to the other
* strongly connected vs. weakly connected
* connected <=> not disconnected

strong vs. weak

* two connected vertices in a directed graph are strongly connected
* if not, create `G*` by replacing any edge in `G` with undirected edges
* if two vertices are connected in `G*`, but not in `G`, then
  those vertices are weakly connected

graph

* `G` has no unreachable vertices
* any two vertices in `G` are connected
* connected <=> not disconnected

<!-- ======================================================================= -->
## further definitions

directed acyclic graph (DAG)

* a DAG is a finite directed graph with no directed cycles

cyclic/acyclic graph

* cyclic - a path exists that
  leads away from one vertex `v` and eventually back to `v`
* acyclic - no such path exists

orientation of an undirected graph

* an assignment of a direction (orientation) to each undirected edge

acyclic orientation

* an orientation that does not form any directed cycle

strong orientation

* an orientation that turns the graph into a strongly connected one

aboresence

* there is exactly one path from the root to any other node
* a directed, rooted tree in which all edges point away from the root
* aborecence => (but not <=) directed acyclic graph (DAG)
