
<!-- ======================================================================= -->
# Path-based, vertex-related definitions

* distance between vertices - the length of the shortest path

<!-- ======================================================================= -->
## components

* (/see/ "connectivity" in "characteristics" /)
* connected graph - a path exists for any pair of vertices
* strongly connected - a directed path exists for any pair
* weakly connected - an undirected path exists for any pair
* disconnected graph - not (|strongly|weakly) connected
* diameter of a component `C` - the length of the longest possible path in `C`

Note that a vertex `(v in V)` is said to be "connected", if `vEx` and/or `xEv`
is true for some `(x in V)`. In addition to that, vertex `v` is said to be
"connected with" the corresponding vertex `x`.

Note that a vertex `(v in V)` may exist such that neither `vEx` nor `xEv` is
true for any vertex `(x in V)`. That is, a graph may contain vertices that
are no endpoint to any edge `(e in E)`. These kind of vertices may in general
be referred to as being "isolated" or "disconnected".

<!-- ======================================================================= -->
## (connected) components

In general, a graph `G := (V,E,P)` is said to be "connected", if there is a
path `xPy` or `yPx` for any pair of vertices `(x,y in V)`. However, graphs
may be created such that it contains disconnected pairs of vertices.
