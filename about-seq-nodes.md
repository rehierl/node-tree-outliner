
<!-- ======================================================================= -->
## Node sequences

The tree traversal fragment can be used to produce a sequence of nodes (i.e.
traversal trace) that contains the nodes of a document in the order in which
these are entered:

```
nodeSequenceOf(root) begin
  sequence = new Array()

  onEnter(node) begin
    sequence.add(node)
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

The sequence of nodes generated this way is referred to as the document's
**node sequence**. As such, these sequences represent the path an algorithm
will take through the DOM tree when visiting each node.

A memory hook: The start tags of an HTML file have the exact same order.

### Subsequent nodes

```
indexOf(sequence, node) begin
  for(i in 0 to sequence.length-1) begin
    if(sequence(i) == node) then
      return i
    end
  end
  throw new NodeNotFoundException()
end

//- distanceBetween(n1, n2) := (indexOf(n2) - indexOf(n1))
//- the result is negative, if n2 appears before n1
//- the result is in [0,+Infinity] for any other pair of nodes

distanceBetween(sequence, n1, n2) begin
  i1 = indexOf(sequence, n1)
  i2 = indexOf(sequence, n2)
  return (i2 - i1)
end

isSubsequentTo(sequence, n1, n2) begin
  return (distanceBetween(sequence, n1, n2) >= 1)
end

isStrictlySubsequentTo(sequence, n1, n2) begin
  return (distanceBetween(sequence, n1, n2) == 1)
end
```

* [en.wikipedia.org, binary relation](https://en.wikipedia.org/wiki/Binary_relation)

Node `Y` is **(merely) subsequent to** `X` with regards to some node sequence,
if `Y` appears after `X` in that sequence (i.e. `X < Y`).
The properties of this binary relation are:

* irreflexive, because `(X < X)` is never true
* asymmetric, because if `(X < Y)`, then `(Y < X)` is not true
* transitive, because if `((X < Y) && (Y < Z))`, then also `(X < Z)`

Node `Y` is **strictly subsequent to** `X`, if `Y` appears directly after `X`
(i.e. `X << Y`). The properties of this binary relation are:

* irreflexive, because `(X << X)` is never true
* asymmetric, because if `(X << Y)`, then `(Y << X)` is not true
* not transitive, because if `((X << Y) && (Y << Z))`, then only `(X < Z)`

Consequently, a node that is strictly subsequent to another node is also
subsequent to it. In contrary to that, a node that is subsequent to another
node is not necessarily strictly subsequent to it (because there could be any
number of other nodes in between).

**structural relationship**: Both relations only state that `Y` will be entered
after `X`. It can not be determined if `Y` will be exited before or after `X`
is (or was) exited. Consequently, it can not be determined where inside the DOM
tree `Y` is located in relation to `X`:

Example (1): `Y` is next sibling to `X`: If `X` has child nodes, then `Y` is
merely subsequent to `X`. If `X` has no child nodes, then `Y` is directly
subsequent to `X`. In both cases, `Y` will be exited after `X` was exited.

Example (2): `Y` is a child node of `X`: If `Y` is the first child node, then
`Y` is directly subsequent to `X`, otherwise it is merely subsequent to it. In
both cases, `Y` will be exited before `X` is exited.

### Sequences of subsequent nodes

```
isSubsequent(nodeSequence, sequence) begin
  for(i in 0 to sequence.length-2) begin
    n1 = sequence(i), n2 = sequence(i+1)
    if(not isSubsequentTo(nodeSequence, n1, n2)) then
      return false
    end
  end
  return true
end

isStrictlySubsequent(nodeSequence, sequence) begin
  for(i in 0 to sequence.length-2) begin
    n1 = sequence(i), n2 = sequence(i+1)
    if(not isStrictlySubsequentTo(nodeSequence, n1, n2)) then
      return false
    end
  end
  return true
end
```

A sequence of nodes is **a sequence of (merely) subsequent nodes**,
if any node within that sequence is subsequent to its predecessor.

A sequence of nodes is **a sequence of strictly subsequent nodes**,
if any node within that sequence is strictly subsequent to its predecessor.

Consequently, the node sequence of a document is a sequence of strictly
subsequent nodes. Obviously, the same applies to all of its subsequences.

Also, any sequence of subsequent nodes may contain subsequences that are strictly
subsequent (i.e. if a sequences is itself not strictly subsequent, then portions
of such a sequence may still be strictly subsequent).

### Sequences that are subsequent to a node

```
isSubsequentTo(nodeSequence, n1, sequence) begin
  n2 = sequence(0)
  return isSubsequentTo(nodeSequence, n1, n2)
end

isStrictlySubsequentTo(nodeSequence, n1, sequence) begin
  n2 = sequence(0)
  return isStrictlySubsequentTo(nodeSequence, n1, n2)
end
```

A sequence of subsequent nodes (s1) is **a sequence that is (merely) subsequent
to a node** (n1), if the first node of that sequence is subsequent to that node
(i.e. `(n1 < s1[0])`).

A sequence of subsequent nodes (s1) is **a sequence that is strictly subsequent
to a node** (n1), if the first node of that sequence is strictly subsequent to
that node (i.e. `(n1 << s1[0])`).

### Sequences that are subsequent to a sequence

```
isSubsequentTo(nodeSequence, sequence1, sequence2) begin
  n1 = sequence1(0)
  n2 = sequence2(0)
  return isSubsequentTo(nodeSequence, n1, n2)
end
```

A sequence (s2) is **a sequence that is (merely) subsequent to a sequence** (s1),
if s2 is subsequent to the first node of s1 (i.e. `(s1[0] < s2[0])`).
(Both sequences need to be sequences of subsequent nodes.)

Because this definition is based upon the first node of s1, the sequences may
be interleaved. As a result, a "strictly subsequent" definition is left out.
It would be different, if the definition would be based upon "last node of s1".
