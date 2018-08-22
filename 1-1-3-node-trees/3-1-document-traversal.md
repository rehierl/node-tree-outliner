
<!-- ======================================================================= -->
# Tree traversal

In order to create an outline that accurately represents a document's logical
structure, the node tree must be traversed by visiting each node. In general,
the traversal of a tree can be classified depending on certain characteristics:

* When is a node visited in relation to its child nodes? -
  e.g. depth-first search (DFS), breadth-first search (BFS)
* In which order are the child nodes visited? -
  left-to-right (LTR) (aka. first-to-last (FTL)) or
  right-to-left (RTL) (aka. last-to-first (LTF))

<!-- ======================================================================= -->
## DFS - depth-first search

The traversal of a tree is referred to as a depth-first (DFS) search, if
all the nodes of a branch are visited before the nodes of any other branch.

Note that, depending on the given tree, `for (child in node.childNodes) begin`
will visit the child nodes of a node in first-to-last, or some random order:

* If the tree is an ordered tree, then the child nodes of each node are
  visited in first-to-last (aka. left-to-right) order.
* If the tree is an unordered tree, then subsequent executions may result
  in visiting the nodes in a different order (i.e. seemingly random).

**DFS, Pre-order tree traversal**

```
traversePreOrder(node) begin
  visitPreOrder(node)
  for (child in node.childNodes) begin
    traversePreOrder(child)
  end
end
```

The `visitPreOrder()` operation marks the beginning of processing a node.
This operation represents a node's enter event, which corresponds with the
start tag of a node.

**DFS, Post-order tree traversal**

```
traversePostOrder(node) begin
  for (child in node.childNodes) begin
    traversePostOrder(child)
  end
  visitPostOrder(node)
end
```

The `visitPostOrder()` operation marks the end of processing a node. This
operation represents a node's exit event, which corresponds with the end
tag of a node.

**DFS, In-order**

```
traverseInOrderBin(node) begin
  traverseTree(node.left)
  traverseInOrderBin(node)
  traverseTree(node.right)
end
```

The in-order tree traversal of a binary tree is a strict tree traversal because
each node is visited exactly once.

Traversing a non-binary tree, which allows any number of child nodes per node
(the DOM tree is such a generic tree) via an in-order tree traversal, adds the
difficulty of having to generically define when to visit each node independently
of a tree's exact structure.

One way of solving this issue would be to execute a node's visit operation(s)
once per child node:

```
traverseInOrder(node) begin
  visitPreOrder(node)
  for (child in node.childNodes) begin
    visitInOrderBefore(node)
    traverseInOrder(child)
    visitInOrderAfter(node)
  end
  visitPostOrder(node)
end
```

It does not matter if either `visitInOrderBefore()`, or `visitInOrderAfter()`,
or even both are used. Both will be executed multiple times per node. Because
of that, the in-order tree traversal of a generic tree is not a strict tree
traversal.

<!-- ======================================================================= -->
## BFS - breadth-first search

A tree traversal is referred to as a breadth-first (BFS) search, if the nodes
of a tree are visited one level at a time.

```
//- visit the nodes in a given range of (relative) levels
//- the node.level property (in [0,+Inf]) is assumed to be
//  defined to return a node's absolute node level
//- the root node of a tree has a node level value of 0
//- begin with visiting all nodes at level n
//- then continue to visit all nodes at level n+1, etc.
//- the "root" input parameter is not necessarily
//  identical to the root of the overall tree

traverseBFS(root, min, max) begin
  queue = new Queue()
  queue.enqueue(root)

  while(not queue.isEmpty) begin
    node = queue.dequeue()

    //- the node's relative level
    level = (node.level - root.level)

    if(level in [min,max]) begin
      visitBFS(node)
    end

    for (child in node.childNodes) begin
      queue.enqueue(child)
    end
  end
end
```

* `BFS, BFS(node) := traverseBFS(node,-Inf,+Inf)`
* `BFS-N, BFS(node,N) := traverseBFS(node,N,N)`

Executing **BFS-0** will only visit the 1st level of the given node, which only
contains the specified node itself. Executing **BFS-1** will only visit the 1st
actual level, which only contains the child nodes of the root input parameter.

<!-- ======================================================================= -->
## Document traversal

```
traverseTree(node) begin
  onEnter(node)
  for (child in node.childNodes) begin
    traverseTree(child)
  end
  onExit(node)
end
```

In order to create the outline for a document, an algorithm needs to execute
certain operations depending on which node is being entered or exited.

Note that, because of the `onEnter()` and `onExit()` calls, the outline
algorithm can be understood to be **an event-driven process**. Furthermore,
the **enter** event can be understood to **open** a node and the **exit**
event to **close** a node.

When a node is being entered/opened, an algorithm might have to:

* close outer sections
* associate the node being entered with a section
* (seemingly) suspend an outer section
* initialize a new section

When a node is being exited/closed, an algorithm might have to:

* close inner sections
* (seemingly) resume an outer section
* initialize a new outer section

A design must unambiguously define which operations need to be processed
when entering/exiting a given node.
