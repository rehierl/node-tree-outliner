
<!-- ======================================================================= -->
# Path sequence

The tree traversal fragment can be used to produce a sequence of paths.
This sequence contains the rooted path of each node in enter-order.

```
pathSequenceOf(root) begin
  sequence = new Array()

  pathOf(sequence, node) begin
    if(node.parent != null) begin
      pathOf(sequence, node.parent)
    end
    sequence.add(node)
  end

  pathOf(node) begin
    sequence = new Array()
    pathOf(sequence, node)
    return sequence
  end

  onEnter(node) begin
    path = pathOf(node)
    sequence.add(path)
  end

  onExit(node) begin
    return
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

The sequence of paths generated this way will be referred to as
**the sequence of (rooted) paths** of a given root/tree.

* `pathSequenceOf(root)` := the tree's sequence of rooted paths
* the first path in such a sequence has length 1 and only contains the root
* the root node will be the first node in each path - i.e. `(p(1) == r)`
* no path in this sequence will be empty

The path `(p(n) in RD)` that begins in a tree's root `r` and that ends
in node `n` is referred to as **the (rooted) path of a node**.

Each path in `p(n)` holds all nodes that have been entered, but not yet
exited, when node `n` is being visited. Because of that, such a path may
also be loosely referred to as **the (current) stack of open nodes**.

The definitions for sequences also apply to a sequence of rooted paths.

* `p1` is (strictly|loosely)? pre-/in-/sub-sequent to `p2`
* `p1 (<<|<|<>|>|>>) p2`

This sequence can also be defined by the tree's node sequence:

* path sequence `PS`, node sequence `NS`
* `PS := (p1,...,pn)` where `pi := pathOf(ni)`
* put differently: `PS := (p(n1),...,p(nk))`

Note that each path in such a sequence of paths is unique.
Because of that, `PS` is an ordered set of sequences.

<!-- ======================================================================= -->
## alternative definition - child node

Node `c` is **a child of** node `n`,
if `(prefix(pc,#pc-1) == pn)`.

Node `c` is **the first child of** node `n`, if `c` is a child of `n`
and if `n` has no other child `d` such that `(pd < pc)`.

Node `c` is **the last child of** node `n`, if `c` is a child of `n`
and if `n` has no other child `d` such that `(pc < pd)`.

Note that the latter two statements essentially only state that a node's
first child will be entered first, and that a node's last child will be
entered last.

<!-- ======================================================================= -->
## alternative definition - sibling

Node `x` is **a sibling of** node `y`,
if `(prefix(px,#px-1) == prefix(py,#py-1))`.

Node `x` is **the previous sibling of** node `y`, if `x` is a sibling of `y`
and if there is no other sibling `z` such that `(px < pz < py)`.

Node `y` is **the next sibling of** node `x`, if `x` is a sibling of `y`
and if there is no other sibling `z` such that `(px < pz < py)`.

Note however that siblings are not strictly connected:

* there is no uni-directional path `p=(x,...,y) in (TD or BU)`
* siblings share common ancestors but are, other than that, unrelated
