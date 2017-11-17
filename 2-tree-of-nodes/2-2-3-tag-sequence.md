
<!-- ======================================================================= -->
# Tag sequence

Similar to generating the node sequence of a document, the tree traversal
fragment can be used to produce **a document's tag sequence**:

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

Executing this pseudocode with the following example HTML fragment as input ...

```
Example 1 (E-1):
----------

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

Any tag in such a sequence corresponds with an enter or exit event: start tag
`name` represents an enter and end tag `/name` an exit event. Any tag sequence
therefore corresponds with the structure of one or more fragments that have the
same, if not identical, structure.

Memory hook: Essentially, a document's tag sequence corresponds with an HTML
file that was stripped of any content.
