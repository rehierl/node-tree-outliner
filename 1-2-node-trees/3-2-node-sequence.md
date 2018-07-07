
<!-- ======================================================================= -->
# The node sequence of a tree

Given a directed rooted tree of nodes (no loops, no cycles),
the following traversal algorithms will visit each node exactly once:

* DFS, pre-order
* DFS, post-order
* BFS

As such, any of these can be used to create a trace of nodes, which reflects
the executed traversal algorithm. And because a trace of nodes is a linear
sequence of nodes (i.e. an ordered set of nodes), such a node trace represents
a topological sort order.

<!-- ======================================================================= -->
## Linear node sequence in enter-order

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
    for (child in node.childNodes) begin
      traverseTree(child)
    end
    onExit(node)
  end

  return sequence
end
```

The linear node sequence generated this way will be referred to as **the node
sequence of** the tree's root and therefore also as the node sequence of
the tree itself. That is, the node sequence of a tree is identical to the
node sequence of its root node. As such, these sequences represent the path
an algorithm will take through the tree when entering each node.

* the tree's node sequence := `nodeSequenceOf(root)`
* the root node will always be the first node in such a linear sequence

Note that the node sequence is said to be in **enter-order** if the nodes
added while the nodes are being entered. The node sequence is said to be
in **exit-order**, if the nodes are added while exiting them.

**Memory hook**
The node sequence of a tree (in enter-order)
corresponds with the order of all start tags.

<!-- ======================================================================= -->
## Sequent nodes

Note that the in-/pre-/sub-sequent definitions (see sequences) can be used in
combination with linear node sequences:

* x is **insequent to** y - i.e. neither pre- nor sub-sequent
* x is **strictly sequent to** y - i.e. absolute distance is +1
* x is **loosely sequent to** y - i.e. absolute distance is >1

### sub-sequent nodes

Node `y` is **subsequent to** `x` with regards to a linear sequence, if `y`
appears after `x` in that sequence (i.e. `X < Y`). The properties of this
binary relation are:

* irreflexive, because `(X < X)` is never true (`x` is insequent to itself)
* asymmetric, because if `(X < Y)`, then `(Y < X)` is not true
* transitive, because if `((X < Y) and (Y < Z))`, then also `(X < Z)`

This relationship can be used to define a binary relation:

* relation `R`, graph `G`, set of nodes `N`, edge `e`
* `R := (N,N,G)` and `G in NxN`
* where `e := (a,b) in G`, if `a` is subsequent to `b`
* `sem(R)` := "subsequent-to"

Node `y` is **strictly subsequent to** `x`, if `y` appears directly after `x`
(i.e. `X << Y`). The properties of this binary relation are:

* irreflexive, because `(X << X)` is never true (`x` is insequent to itself)
* asymmetric, because if `(X << Y)`, then `(Y << X)` is not true
* not transitive, because if `((X << Y) && (Y << Z))`, then only `(X < Z)`
* `y` is either the next sibling to, or the first child of `x`

Node `y` is **loosely subsequent to** `x`, if `y` is subsequent, but not
strictly subsequent to `x` (i.e. there are nodes in between `x` and `y`).

A node that is strictly subsequent to another node is also subsequent to it. In
contrary to that, a node that is subsequent to another node is not necessarily
strictly subsequent to it (there may be one or more nodes in between).

* strictly subsequent -> subsequent
* subsequent =!> strictly subsequent

**structural relationship**: Both relations only state that `y` will be entered
after `x`. It can not be determined if `y` will be exited before or after `x`
is (or was) exited. Consequently, it can not be determined where inside the
tree `y` is located in relation to `x`:

Example 1: `y` is next sibling to `x`: If `x` has child nodes, then `y` is only
subsequent to `x`. If `x` has no child nodes, then `y` is strictly subsequent
to `x`. In both cases, `y` will be exited after `x` was exited.

Example 2: `y` is a child node of `x`: If `y` is the first child node, then `y`
is strictly subsequent to `x`, otherwise it is merely subsequent to it. In both
cases, `y` will be exited before `x` is exited.

### pre-sequent nodes

A "presequent-to" relation can be defined in similar fashion:

* node `x` is **presequent to** `y` with regards to some node sequence,
  if `x` appears before `y` in that sequence (i.e. `X < Y`)
* node `x` is **strictly presequent to** `y`,
  if `x` appears directly before `y` (i.e. `X << Y`)
* node `x` is **loosely presequent to** `y`,
  if `x` is presequent but not strictly presequent to `y`

<!-- ======================================================================= -->
## Sequences of subsequent nodes

```
isSubsequent(sequence, nodeSequence) begin
  for (i in 1 to sequence.length-1) begin
    n1 = sequence(i), n2 = sequence(i+1)
    if(not isPreSequentTo(n1, n2, nodeSequence)) then
      return false
    end
  end
  return true
end
```

A sequence of nodes is **a sequence of subsequent nodes**, if any node
within that sequence is (strictly or loosely) subsequent to its predecessor.

Note that all nodes in the given sequence of nodes must be elements of the
corresponding linear node sequence. In addition to that, the order of nodes
in the given sequence of nodes must correspond with the tree's node sequence.

Note that any sequence of subsequent nodes is itself a linear sequence.
In addition to that, the input sequence is a mathematical/removal-based
subsequence of the corresponding linear sequence.

```
//- prototype with a similar definition
isStrictlySubsequent(sequence, nodeSequence)
```

A sequence of nodes is **a sequence of strictly subsequent nodes**,
if any node within that sequence is strictly subsequent to its predecessor.

* the node sequence of a tree's root
  is a sequence of strictly subsequent nodes
* any sequence of strictly subsequent nodes
  is a sequence of subsequent nodes
* any (concatenation-based) subsequence (aka. substring)
  of a tree's node sequence is a sequence of strictly subsequent nodes
* any sequence of subsequent nodes
  may still contain subsequences of strictly subsequent nodes

There is no definition for **a sequence of loosely subsequent nodes**
because there are multiple options to define such a term:

1. all nodes have to be loosely subsequent to their predecessor
   (i.e. the sequence must not contain any strictly subsequent nodes)
2. at least one node is loosely subsequent to its predecessor
   (i.e. the sequence may still contain strictly subsequent nodes).

For the moment, such a definition is not required.

<!-- ======================================================================= -->
## A general perspective/idea

The following definitions need to be understood to attempt to provide a general
idea of the relationship between certain nodes and/or sequences.

(With regards to the following definitions:)

* `ns` refers to the complete node sequence of a tree
* `si` are assumed to be subsequences of `ns`
* that is, `isSubsequent(si,ns)` is assumed to be true
* `ni` is a node in `si` - e.g. `n1 in s1`
* any node `ni` is still a node in `ns`

Note that the naming convention is such that the name of a binary operation
refers to the 1st parameter, which needs to be tested against the 2nd parameter
(i.e. the context of the corresponding operation).

Note that the below statements assume the corresponding sequences to be
non-empty. In order to allow to make similar statements with regards to
empty sequences, additional information would have to be taken into account
(e.g. with regards to the node that defines the empty sequence).

Note that, with regards to the two distinct nodes `n1` and `n2` of a linear
sequence (i.e. `(n1 != n2)`), `n1` is either subsequent ex-or presequent to `n2`.

<!-- ======================================================================= -->
## Sequences subsequent to a node

```
               |-------------
n1 n2 n3 n4 n5 | n6 n7 n8 n9 
      ^        |-------------
      "n2"     "s1"
```

Note that these kind of "images" are intended to "visualize"
the context of the corresponding section.

```
isSubsequentTo(s1, n2, seq) begin
  return isSubsequentTo(s1(1), n2, seq)
end
```

The non-empty sequence `s1` is **a sequence that is subsequent to a node**
`n2`, if the first node of `s1` is subsequent to `n2`
(i.e. `(n2 < s1[1])` or simply `(n2 < s1)`).

```
//- prototype with a similar definition
isStrictlySubsequentTo(s1, n2, seq)
```

The non-empty sequence `s1` is **a sequence that is strictly subsequent to a
node** `n2`, if the first node of `s1` is strictly subsequent to `n2`
(i.e. `(n2 << s1[1])` or simply `(n2 << s1)`).

```
//- prototype with a similar definition
isLooselySubsequentTo(s1, n2, seq)
```

The non-empty sequence `s1` is **a sequence that is loosely subsequent to a
node** `n2`, if the first node of `s1` is loosely subsequent to `n2`
(i.e. if there are one or more nodes in between).

A sequence that is strictly subsequent to a node is also subsequent to it. In
contrary to that, a sequence that is subsequent to a node is not necessarily
strictly subsequent to it (there may be one or more nodes in between).

* strictly subsequent -> subsequent
* subsequent =!> strictly subsequent

<!-- ======================================================================= -->
## Nodes subsequent to a sequence

Note that this is the counter part to "Sequences subsequent to a node".

```
      |-------------------|
n1 n2 | n3 n4 n5 n6 n7 n8 | n9
      |----------^--------| ^
      "s2"       "n1"       "n1"
```

**Memory hook**
"left" is with regards to the first node of the sequence,
and "right" with regards to the last node.

### left subsequent to

```
//- left: with regards to the sequence's first node
isLeftSubsequentTo(n1, s2, seq) begin
  return isSubsequentTo(n1, s2[1], seq)
end

//- prototypes with a similar definition
isStrictlyLeftSubsequentTo(n1, s2, seq)
isLooselyLeftSubsequentTo(n1, s2, seq)
```

Note that the general notion of "left" is to "imply" that a node could be
within the corresponding sequence.

* !left => outside (if not the first node)

Note that a node must be subsequent to the first node of the corresponding
sequence. Consequently, a sequence's first node is not considered to be
left-subsequent to its sequence. However, the first node of a sequence is
still an element of that sequence.

### right subsequent to

```
//- right: with regards to the sequence's last node
isRightSubsequentTo(n1, s2, seq) begin
  return isSubsequentTo(n1, s2[s2.length], seq)
end

//- prototypes with a similar definition
isStrictlyRightSubsequentTo(n1, s2, seq)
isLooselyRightSubsequentTo(n1, s2, seq)
```

Note that the general notion of "right" is to "imply" that a node is outside
of the corresponding sequence.

* (left and !right) => inside
* (left and right) => outside
* right => (left and right)

Note that a sequence's last node is not considered to be right-subsequent to
its sequence. That is, because the last node is considered to be within the
boundaries of its sequence.

<!-- ======================================================================= -->
## Sequences subsequent to a sequence

```
      |----------------|    |-----
n1 n2 | n3 n4 n5 n6 n7 | n8 | n9 
      |----------------|    |-----
      "s2"                  "s1"
```

### left subsequent

```
isLeftSubsequentTo(s1, s2, ns) begin
  n1 = s1(1), n2 = s2(1)
  return isSubsequentTo(n1, n2, ns)
end

//- prototypes with similar definition
isStrictlyLeftSubsequentTo(n1, n2, ns)
isLooselyLeftSubsequentTo(n1, n2, ns)
```

A sequence `s1` is **a sequence that is left subsequent
to a sequence** `s2`, if `s1` is subsequent to the first node of `s2`
(i.e. `(s2[1] < s1[1])`).

A sequence `s1` is **a sequence that is strictly left subsequent
to a sequence** `s2`, if `s1` is strictly subsequent to the first node of `s2`
(i.e. `(s2[1] << s1[1])`).

A sequence `s1` is **a sequence that is loosely left subsequent
to a sequence** `s2`, if `s1` is loosely subsequent to the first node of `s2`
(i.e. if there are one or more nodes in between).

* strictly left subsequent => left subsequent
* left subsequent =!> strictly left subsequent
* a sequence that is left subsequent to another sequence
  may begin and may even end inside of it.

### right subsequent

```
isRightSubsequentTo(s1, s2, n2) begin
  len1 = s1.length, n1 = s1(len1), n2 = s2(1)
  return isSubsequentTo(n1, n2, ns)
end

//- prototypes with similar definition
isStrictlyRightSubsequentTo(n1, n2, ns)
isLooselyRightSubsequentTo(n1, n2, ns)
```

A sequence `s1` is **a sequence that is right subsequent
to a sequence** `s2`, if `s1` is subsequent to the last node of `s2`
(i.e. `(s2[#s2] < s1[1])`).

A sequence `s1` is **a sequence that is strictly right subsequent
to a sequence** `s2`, if `s1` is strictly subsequent to the last node of `s2`
(i.e. `(s2[#s2] << s1[1])`).

A sequence `s1` is **a sequence that is loosely right subsequent
to a sequence** `s2`, if `s1` is loosely subsequent to the last node of `s2`
(i.e. if there are one or more nodes in between).

* strictly right subsequent => right subsequent
* right subsequent =!> strictly right subsequent
* a sequence that is left, but not right subsequent to another sequence
  begins and may even end inside of it
* a sequence that is right subsequent to another sequence
  is also left subsequent to it
* a sequence `s1` that is strictly right subsequent to sequence `s2` is
  also strictly left subsequent to `s2`
