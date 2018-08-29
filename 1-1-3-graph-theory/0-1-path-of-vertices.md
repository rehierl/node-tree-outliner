
<!-- ======================================================================= -->
# Paths of vertices

<!-- ======================================================================= -->
## wikipedia, path (graph theory)

* a sequence of edges which connect a sequence of vertices
* a directed path (dipath) - edges are directed in the same direction

definition

* `p := [a, (a,b), b, (b,c), c, ...]` or `p := [v0,e0,v1,e1, ...]`
* infinite path - no first and last vertex
* semi-infinite path (ray) - first, but no last vertex
* simple path - no repeated vertices
* weighted graph - each edge has a weight
* weight of path - sum of all weight values - aka. cost/length

glossary - trail, walk

* trail - a walk without repeated edges
* exception - first vertex may be equal to the last
* tour - a closed trail
* walk - a sequence of vertices and edges
* the vertex in between two neighboring edges is common to both edges
* simple path - a walk without repeated vertices/edges
* open - first and last vertices are different
* closed (cycle) - begins and ends at the same vertex

notational aspects

* alternatively - `p := [e1,e2,...]` - a sequence of adjacent edges
* alternatively - `p := [v1,v2,...]` - a sequence of adjacent vertices
* `xPy` := a path exists that connects `x` with `y`
* i.e. a path `p := [x,...,y]` exists

<!-- ======================================================================= -->
## wikipedia, induced path
