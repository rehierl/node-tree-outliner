
<!-- ======================================================================= -->
# The node sequence of a tree

Given a directed rooted tree of nodes (no loops, no cycles), the DFS and BFS
algorithms will visit each node exactly once. As such, any of these can be used
to create a trace of nodes that represents the executed tree traversal as an
ordered sequence of nodes.

```
nodeSequenceOf(root) begin
  sequence = new Array()

  onEnter(node) begin
    sequence.add(node)
  end

  onExit(node) begin
    //- do nothing
  end

  traverseTree(node) begin
    onEnter(node)
    for (child in node.childNodes) begin
      traverseTree(child)
    end
    onExit(node)
  end

  return sequence
end
```

A node sequence generated this way will be referred to as **the node sequence
of** the tree's root and therefore also as the node sequence of the tree itself.
That is, the node sequence of a tree is identical to the node sequence of its
root. As such, these sequences represent the path an algorithm will take through
the tree when entering each node.

* the tree's node sequence := `nodeSequenceOf(root)`
* the root node will always be the first node in such a sequence

Note that the node sequence is said to be in **enter-order** if the nodes are
added to it while the nodes are being entered. The node sequence is said to be
in **exit-order**, if the nodes are added while exiting them.

**Memory hook**
The node sequence of a tree (in enter order) corresponds with the order of
the start/enter tags. In contrary to that, the node sequence of a tree (in
exit order) corresponds with the order of the end/exit tags.
