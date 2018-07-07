
<!-- ======================================================================= -->
# Graph/Tree traversal

* aspects related to traversing graphs/trees

<!-- ======================================================================= -->
## wikipedia, graph traversal

* graph search is the process of visiting each vertex
* each visit involves the execution of operations (check, update, etc)
* classified by the order in which vertices are visited

graph traversal

* graph traversal may have to visit vertices more than once
* graph traversal needs to handle revisits (e.g. a visited flag)

depth-first search (DFS)

* visit child vertices before the neighbors
* depth before breadth
* stack/recursion-based implementation
* stack/recursion used when backtracking
* e.g. topological sorts, planetarity testing, etc.

breadth-first search (BFS)

* visit the neighbors before visiting the children
* queue-based implementation
* e.g. shortest path, bipartiteness, flood fill, etc.

graph exploration

* a variant of graph traversal
* in cases where the knowledge of a graph is limited
* e.g. web pages, seemingly infinite graphs

<!-- ======================================================================= -->
## wikipedia, tree traversal

* tree search is a special case of graph traversal
* will visit each vertex/node exactly once
* classified by the order in which nodes are visited
* there are several options to traverse trees
* e.g. depth-first, breadth-first and hybrids/variations
* unlike lists, a tree search is non-linear
* needs use stacks/queues to defer nodes for later visit

depth-first search (DFS)

* children before siblings
* children in left-to-right or first-to-last order
* alternatively in right-to-left or last-to-first order
* preorder (NLR) - visit the node before any child nodes
* inorder (LNR) - visit the node in between its left and right child
* postorder (LRN) - visit the node after all child nodes
* generic trees - nodes may have any number of child nodes
* generic search - NC*, C*N, N(C*N)*N, N(NC*)*N

breadth-first search (BFS)

* visit the nodes on a level before going any deeper

other search algorithms are possible

* which are neither DFS nor BFS

infinite trees

* obviously, no strict/complete traversal
* also used in combination with over-sized trees
* DFS and BFS may end up not visiting any node at all
* hybrid methods exist that can visit countably infinite trees

<!-- ======================================================================= -->
## wikipedia, depth-first search (DFS)

* visit a branch prior to moving to the next neighbor
* time complexity is O(#V + #E)
* O(#E) may vary between O(1) and O((#V)²)

types of edges

* tree edges - edges of the spanning tree
* forward edges - point to a leaf of a previous branch
* back edges - point to an ancestor in the current branch
* cross edges - point to a parent of a previous branch

DFS ordering

* s = [v(1) .. v(i-1), v(i), v(i+1) .. v(n)] is in DFS ordering, if
* prefix(i) = [v(1) .. v(i-1)], suffix(i) = [v(i+1) .. v(n)]
* index(s,v) = index of last neighbor of v in s, otherwise 0
* for all i in [2,n-1], v = s(i) is the vertex such that
* (index(prefix(i),v) >= index(prefix(i),w)) for all w in suffix(i)

comments

* in graph speech, neighbors share edges
* in tree speech, replace "neighbors" by "parent or child"

Vertex ordering

* use DFS to linearly order the vertices
* preordering - order the vertices in the order they were first visited
* postordering - order the vertices in the order they were last visited
* reverse post-ordering - flipped postordering

reverse post-ordering

* not the same as preordering
* produces a topological sorting of any DAG
* often represents a natural linearization of control flow
* example if-then-else construct

<!-- ======================================================================= -->
## wikipedia, breadth-first search (BFS)

* visits all neighbors prior to moving to the next level
* enqueue each node on a level as the root of a subtree to search
* which algorithm to use DFS/BFS depends on the problem domain
* same complexity as DFS

BFS ordering

* s = [v(1) .. v(i-1), v(i), v(i+1) .. v(n)] is in BFS ordering, if
* prefix(i) = [v(1) .. v(i-1)], suffix(i) = [v(i+1) .. v(n)]
* index(s,v) = index of first neighbor of v in s, otherwise +Infinity
* for all i in [2,n-1], v = s(i) is the vertex such that
* (index(prefix(i),v) <= index(prefix(i),w)) for all w in suffix(i)
