
<!-- ======================================================================= -->
# Tree traversal

In order to create an outline that accurately represents a document's structure,
the node tree must be traversed by visiting each node. In general, the traversal
of a node tree can be classified depending on certain characteristics - such as:

* When is a node visited in relation to its child nodes? -
  e.g. depth-first search (DFS), breadth-first search (BFS)
* In which order are the child nodes visited? -
  left-to-right (LTR) (aka. first-to-last (FTL)) or
  right-to-left (RTL) (aka. last-to-first (LTF))

<!-- ======================================================================= -->
## depth-first search (DFS)

The traversal of a tree is referred to as a depth-first (DFS) search, if
all the nodes of a branch are visited before the nodes of any other branch.

Note that the `firstChild` and `nextSibling` node properties are needed.
That is, the underlying node tree must be an ordered rooted tree of nodes.

**FTL, DFS, Pre-order tree traversal**

```
traversePreOrder(node) begin
  visitPreOrder(node)
  child = node.firstChild
  while(child != null) begin
    traversePreOrder(child)
    child = child.nextSibling
  end
end
```

The `visitPreOrder()` operation marks the beginning of processing a node. This
operation represents a node's enter event which corresponds with a node's start
tag.

**FTL, DFS, Post-order tree traversal**

```
traversePostOrder(node) begin
  child = node.firstChild
  while(child != null) begin
    traversePostOrder(child)
    child = child.nextSibling
  end
  visitPostOrder(node)
end
```

The `visitPostOrder()` operation marks the end of processing a node. This
operation represents a node's exit event which corresponds with a node's end
tag.

**FTL, DFS, In-order**

```
traverseInOrderBin(node) begin
  traverseTree(node.left)
  traverseInOrderBin(node)
  traverseTree(node.right)
end
```

The in-order tree traversal of a binary tree is a strict tree traversal because
each node is visited exactly once.

Traversing a non-binary tree, which allows more than two child nodes per node
(the DOM tree is such a generic tree) via an in-order tree traversal, has the
difficulty of generically defining when to visit each node independently of its
inner structure.

One way of solving this issue would be to execute a node's visit operation(s)
once per child node:

```
traverseInOrder(node) begin
  child = node.firstChild
  while(child != null) begin
    visitInOrderBefore(node)
    traverseInOrder(child)
    visitInOrderAfter(node)
    child = child.nextSibling
  end
end
```

It does not matter if either `visitInOrderBefore()`, or `visitInOrderAfter()`,
or even both are used. Both will be executed multiple times per node. Because of
that, the in-order tree traversal of a generic tree is no strict tree traversal.

<!-- ======================================================================= -->
## breadth-first (BFS) search

A tree traversal is referred to as a breadth-first (BFS) search, if the nodes
of a tree are visited one level at a time.

**FTL, BFS**

```
//- visit the nodes in a given range of (relative) levels
//- node.level in [1,+Inf] returns a node's (absolute) node level
//- the root node of a tree has a node level value of 1
//- first visit all nodes at level n, then those at level n+1, etc.

traverseBFS(root, min, max) begin
  assert((1 <= min) && (min <= max))

  queue = new Queue()
  queue.enqueue(root)

  while(not queue.isEmpty) begin
    node = queue.dequeue()

    //- the node's relative level
    level = 1 + (node.level - root.level)

    if(level in [min,max]) begin
      visitBFS(node)
    end

    child = node.firstChild
    while(child != null) begin
      queue.enqueue(child)
      child = child.nextSibling
    end
  end
end
```

Executing `traverseBFS(node, 1, 1)` (= **BFS-1**) will only visit the 1st level,
which only contains the specified node. Executing `traverseBFS(node, 2, 2)`
(= **BFS-2**) will only visit the 2nd level, which only contains a node's
immediate descendants (i.e. child nodes).

<!-- ======================================================================= -->
## an event-driven process

```
traverseTree(node) begin
  onEnter(node)
  child = node.firstChild
  while(child != null) begin
    traverseTree(child)
    child = child.nextSibling
  end
  onExit(node)
end
```

In order to create an outline for a document, an algorithm needs to execute
certain operations depending on which node is being entered or exited.

Note that, because of the `onEnter()` and `onExit()` calls, the outline
algorithm can be understood to be an event-driven process.

When a node is entered, an algorithm might have to:

* end outer sections
* associate the node being entered with a section
* "suspend" outer sections
* create and initialize a new inner section

When a node is exited, an algorithm might have to:

* end inner sections
* reactivate a "suspended" outer section, or
* create and initialize a new outer section

Which operations need to be executed while an event is being executed, must
be defined for each type of node.
