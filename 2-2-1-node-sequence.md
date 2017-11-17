
# Node sequences

The tree traversal pseudocode fragment can be used to produce a sequence of
nodes (i.e. a traversal trace) that contains the nodes of a document in the
order in which these are entered:

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

The sequence of nodes generated this way is referred to as **the node sequence
of** a given root. As such, these sequences represent the path an algorithm
will take through the tree when visiting each node.

* The document's node sequence := `nodeSequenceOf(body)`.
* The root element will always be the first node in its node sequence.

A memory hook: The start tags of an HTML file have the exact same order.

<!-- ======================================================================= -->
## Subsequent nodes

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

isLooselySubsequentTo(sequence, n1, n2) begin
  return (distanceBetween(sequence, n1, n2) > 1)
end
```

Node `Y` is **subsequent to** `X` with regards to some node sequence, if `Y`
appears after `X` in that sequence (i.e. `X < Y`). The properties of this
binary relation are:

* irreflexive, because `(X < X)` is never true
* asymmetric, because if `(X < Y)`, then `(Y < X)` is not true
* transitive, because if `((X < Y) && (Y < Z))`, then also `(X < Z)`

Node `Y` is **strictly subsequent to** `X`, if `Y` appears directly after `X`
(i.e. `X << Y`). The properties of this binary relation are:

* irreflexive, because `(X << X)` is never true
* asymmetric, because if `(X << Y)`, then `(Y << X)` is not true
* not transitive, because if `((X << Y) && (Y << Z))`, then only `(X < Z)`
* Node `X` is not necessarily parent of `Y`!

Node `Y` is **loosely subsequent to** `X`, if `Y` is subsequent, but not
strictly subsequent to `X` (i.e. there are nodes in between `X` and `Y`).

A node that is strictly subsequent to another node is also subsequent to it. In
contrary to that, a node that is subsequent to another node is not necessarily
strictly subsequent to it (there may be one or more nodes in between).

* strictly subsequent => subsequent
* subsequent => not necessarily strictly subsequent

**structural relationship**: Both relations only state that `Y` will be entered
after `X`. It can not be determined if `Y` will be exited before or after `X`
is (or was) exited. Consequently, it can not be determined where inside the
tree `Y` is located in relation to `X`:

Example (1): `Y` is next sibling to `X`: If `X` has child nodes, then `Y` is
merely subsequent to `X`. If `X` has no child nodes, then `Y` is strictly
subsequent to `X`. In both cases, `Y` will be exited after `X` was exited.

Example (2): `Y` is a child node of `X`: If `Y` is the first child node, then
`Y` is strictly subsequent to `X`, otherwise it is merely subsequent to it. In
both cases, `Y` will be exited before `X` is exited.

<!-- ======================================================================= -->
## Presequent nodes

The presequent-to relation could be defined in a similar way:

* Node `X` is **presequent to** `Y` with regards to some node sequence,
  if `X` appears before `Y` in that sequence (i.e. `X < Y`).
* Node `X` is **strictly presequent to** `Y`,
  if `X` appears directly before `Y` (i.e. `X << Y`).
* Node `X` is **loosely presequent to** `Y`,
  if `X` is presequent but not strictly presequent to `Y`.

<!-- ======================================================================= -->
## Sequences of subsequent nodes

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

//- prototypes with similar definition
isStrictlySubsequent(nodeSequence, sequence)
```

A sequence of nodes is **a sequence of subsequent nodes**, if any node within
that sequence is (strictly or loosely) subsequent to its predecessor.

A sequence of nodes is **a sequence of strictly subsequent nodes**, if any node
within that sequence is strictly subsequent to its predecessor.

There is no definition for a sequence of loosely subsequent nodes because there
are multiple options to define such a term:
(1) all nodes have to be loosely subsequent to their predecessor
   (i.e. the sequence must not contain any strictly subsequent nodes), or -
(2) at least one node is loosely subsequent to its predecessor
   (i.e. the sequence may still contain strictly subsequent nodes).
For the moment, such a definition is not required.

* The node sequence of some root
  is a sequence of strictly subsequent nodes.
* Any subsequence of such a node sequence
  is a sequence of strictly subsequent nodes.
* Any sequence of subsequent nodes
  may still contain subsequences of strictly subsequent nodes.

<!-- ======================================================================= -->
## Sequences subsequent to a node

```
isSubsequentTo(seq, n1, s2) begin
  return isSubsequentTo(seq, n1, s2(0))
end

//- prototypes with similar definition
isStrictlySubsequentTo(seq, n1, s2)
isLooselySubsequentTo(seq, n1, s2)
```

* Sequence s1 is a sequence of subsequent nodes.
* n1 does itself not belong to s1.

A sequence (s1) is **a sequence that is subsequent to a node** (n1),
if the first node of that sequence is subsequent to that node
(i.e. `(n1 < s1[0])` or simply `(n1 < s1)`).

A sequence (s1) is **a sequence that is strictly subsequent to a node** (n1),
if the first node of that sequence is strictly subsequent to that node
(i.e. `(n1 << s1[0])` or simply `(n1 << s1)`).

A sequence (s1) is **a sequence that is loosely subsequent to a node** (n2),
if the first node of that sequence is loosely subsequent to that node
(i.e. if there are one or more nodes in between).

* These definitions are based upon non-empty sequences.

**TODO** -
empty section subsequent to a node

A sequence that is strictly subsequent to a node is also subsequent to it. In
contrary to that, a sequence that is subsequent to a node is not necessarily
strictly subsequent to it (there may one or more nodes in between).

* strictly subsequent => subsequent
* subsequent => not necessarily strictly subsequent

<!-- ======================================================================= -->
## Sequences subsequent to a sequence

```
isLeftSubsequentTo(ns, s1, s2) begin
  n1 = s1(0), n2 = s2(0)
  return isSubsequentTo(ns, n1, n2)
end

//- prototypes with similar definition
isStrictlyLeftSubsequentTo(ns, s1, s2)
isLooselyLeftSubsequentTo(ns, s1, s2)

isRightSubsequentTo(ns, s1, s2) begin
  len1 = s1.length, n1 = s1(len1-1), n2 = s2(0)
  return isSubsequentTo(ns, n1, n2)
end

//- prototypes with similar definition
isStrictlyRightSubsequentTo(ns, s1, s2)
isLooselyRightSubsequentTo(ns, s1, s2)
```

* s1 and s2 are sequences of subsequent nodes
* "left" with regards to the first, "right" with regards to the last node
* s2 is left subsequent to s1 => s2 begins after s1 has begun
* s2 is right subsequent to s1 => s2 begins after s1 has ended
* "left" is the default perspective - hence "left"

### left subsequent

A sequence (s2) is **a sequence that is left subsequent
to a sequence** (s1), if s2 is subsequent to the first node of s1
(i.e. `(s1[0] < s2[0])`).

A sequence (s2) is **a sequence that is strictly left subsequent
to a sequence** (s1), if s2 is strictly subsequent to the first node of s1
(i.e. `(s1[0] << s2[0])`).

A sequence (s2) is **a sequence that is loosely left subsequent
to a sequence** (s1), if s2 is loosely subsequent to the first node of s1
(i.e. if there are one or more nodes in between).

* strictly left subsequent => left subsequent
* left subsequent => not necessarily strictly left subsequent
* A sequence that is left subsequent to another sequence
  may begin and may even end inside of it.

### right subsequent

A sequence (s2) is **a sequence that is right subsequent
to a sequence** (s1), if s2 is subsequent to the last node of s1
(i.e. `(s1[N-1] < s2[0])`).

A sequence (s2) is **a sequence that is strictly right subsequent
to a sequence** (s1), if s2 is strictly subsequent to the last node of s1
(i.e. `(s1[N-1] << s2[0])`).

A sequence (s2) is **a sequence that is loosely right subsequent
to a sequence** (s1), if s2 is loosely subsequent to the last node of s1
(i.e. if there are one or more nodes in between).

* strictly right subsequent => right subsequent
* right subsequent => not necessarily strictly right subsequent
* A sequence that is left, but not right subsequent to another sequence
  begins and may even end inside of it.
* A sequence that is right subsequent to another sequence
  is also left subsequent to it.
* A sequence right subsequent to another sequence
  may even be strictly left subsequent to it.
