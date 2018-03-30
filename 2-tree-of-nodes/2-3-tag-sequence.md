
<!-- ======================================================================= -->
# Tag sequence

Similar to the generation of a tree's node sequence, the tree traversal
fragment can be used to produce the tag sequence of a tree:

```
tagSequenceOf(root) begin
  sequence = new Array()

  onEnter(node) begin
    name = node.tagName.toLowerCase
    sequence.add(name)
  end

  onExit(node) begin
    name = node.tagName.toLowerCase
    sequence.add("/" + name)
  end

  traverseTree(node) begin
    onEnter(node)
    child = node.firstChild
    while(child != null) begin
      traverseTree(child)
      child = child.nextSibling
    end
    onExit(node)
  end

  return sequence
end
```

Executing this pseudocode on the following example fragment as input ...

```
<body>
  A
  <h1>B</h1>
  C
  <h1>D</h1>
  E
</body>
```

... will produce the following tag sequence:

```
seq-0 := [body, #text, /#text, h1, #text, /#text, /h1, #text, /#text, h1, #text,
          /#text, /h1, #text, /#text, /body]
```

Any tag in such a sequence corresponds with the enter or the exit event of a
node: start tag `name` represents a node's enter and end tag `/name` a node's
exit event. Any tag sequence therefore corresponds with the structure of one
or more fragments that have the same, if not identical, structure.

**Memory hook**
Essentially, a document's tag sequence corresponds with an HTML
file that was stripped of its contents.
