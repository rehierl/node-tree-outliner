
<!-- ======================================================================= -->
# Path sequence

The tree traversal fragment can be used to produce a sequence of paths.
This sequence contains the rooted path of each node in the order of the
node sequence:

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
**the path sequence of** a given root/tree.

* the tree's path sequence := `pathSequenceOf(root)`
* the root node will be the first node in each path - i.e. `(p(1) == r)`
* the first path in such a sequence has length 1 and only contains the root node
* any path in this sequence is a rooted path

The definitions for elements of such sequences also apply to these paths.

* `p1` is (strictly|loosely)? pre-, in- or sub-sequent to `p2`
* `p1 (<<|<|<>|>|>>) p2`

The path sequence can also be defined by the corresponding node sequence:

* path sequence `PS`, node sequence `NS`
* `PS := (p1,...,pn)` where `pi := pathOf(ni)` for `ni in NS`

<!-- ======================================================================= -->
## the (rooted) path of a node

The path that connects a tree's root `r` with a node `n` is referred to as
**the rooted path of node** `n`, or simply as **the path of node** `n`.

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

Note that these statements are limited to the child nodes of a node. As such,
the latter two statements essentially only state that a node's first child
will be entered first, and that a node's last child will be entered last.

<!-- ======================================================================= -->
## siblings

Node `s` is **a sibling of** node `n`,
if `(prefix(pn,#pn-1) prefix-of ps)` and `(#ps == #pn)`.

Node `s` is **the previous sibling of** node `n`, if `s` is a sibling of `n`
and if there is no other sibling `t` such that `(ps < pt < pn)`.

Node `s` is **the next sibling of** node `n`, if `s` is a sibling of `n`
and if there is no other sibling `t` such that `(pn < pt < ps)`.

Note however that siblings are not strictly connected:

* there is no uni-directional path `p=(n,...,s) in TD or BU`
* siblings all share common ancestors but are, other than that, unrelated
