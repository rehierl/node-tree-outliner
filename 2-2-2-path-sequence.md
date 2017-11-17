
<!-- ======================================================================= -->
# Path sequence

The tree traversal fragment can also be used to produce a sequence of paths.
This sequence contains the rooted path of each node in the order of the node
sequence:

```
pathOf(node, sequence) begin
  if(node.parent != null) begin
    pathOf(node.parent, sequence)
  end
  sequence.add(node)
end

pathOf(node) begin
  sequence = new Array()
  pathOf(node, sequence)
  return sequence
end

pathSequenceOf(root) begin
  sequence = new Array()

  onEnter(node) begin
    path = pathOf(node)
    sequence.add(path)
  end

  onExit(node) begin
    return
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

The sequence of paths generated this way is referred to as
**the path sequence of** a given root.

* the document's path sequence (PS) := `pathSequenceOf(body)`
* the root will always be the first node in each path - i.e. `(p(1) == r)`
* any path in this sequence is a rooted path

The definitions for elements of sequences also apply to these paths.

* `p1` is (strictly|loosely)? pre- or sub-sequent to `p2`
* `p1 (<<|<|<>|>|>>) p2`

The path sequence can also be defined by the corresponding node sequence:

* `PS := (p1,...,pn)` where `pi := pathOf(ni)` for `ni in NS`
* path sequence `PS`, node sequence `NS`

<!-- ======================================================================= -->
## the (rooted) path of a node

The path that connects a tree's root `r` with a node `n` is referred to as
**the rooted path of node** `n`, or simply **the path of node** `n`.

* the path of a node will be referred to as `p(n)` or `pn`
* e.g. `pn in RD`

<!-- ======================================================================= -->
## children

Node `c` is **a child of** node `n`,
if `(prefix(pc,#pc-1) == pn)`.

Node `c` is **the first child of** node `n`, if `c` is a child of `n`
and if `n` has no other child `d` such that `(pd < pc)`.

Node `c` is **the last child of** node `n`, if `c` is a child of `n`
and if `n` has no other child `d` such that `(pc < pd)`.

Note - tree traversal requires a `firstChild` property -
i.e. a clarification that is based upon its own definition.

<!-- ======================================================================= -->
## siblings

Node `s` is **a sibling of** node `n`,
if `(prefix(pn,#pn-1) prefix-of ps)` and `(#ps == #pn)`.

Node `s` is **the previous sibling of** node `n`, if `s` is a sibling of `n`
and there is no other sibling `t` such that `(ps < pt < pn)`.

Node `s` is **the next sibling of** node `n`, if `s` is a sibling of `n`
and there is no other sibling `t` such that `(pn < pt < ps)`.

Note - tree traversal requires a `nextSibling` property -
i.e. a clarification that is based upon its own definition.

However, siblings are not strictly connected:

* there is no uni-directional path `p=(n,...,s) in TD or BU`
* siblings all share common ancestors but are, other than that, unrelated
