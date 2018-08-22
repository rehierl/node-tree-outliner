
<!-- ======================================================================= -->
# pre-/in-/sub-sequent (2)

Note that the pre-/in-/sub-sequent definitions (see sequences)
can be used in combination with ordered sequences of nodes:

* (x is **not sequent to** y) := distance(x,y) is undefined
* (x is **sequent to** y) := distance(x,y) has a defined value
* (x is **loosely sequent to** y) := (abs(distance(x,y)) > +1)
* (x is **strictly sequent to** y) := (abs(distance(x,y)) == +1)
* (x is **insequent to (<>)** y) := (distance(x,y) == 0)

### sub-sequent nodes

Node `y` is **subsequent to (>)** `x` with regards to an ordered sequence, if
`y` appears after `x` in that sequence (i.e. `y > x`). The properties of this
binary relation are:

* irreflexive, because `(x > x)` is never true
* asymmetric, because if `(x > y)`, then `(y > x)` is not true
* transitive, because if `((x > y) and (y > z))`, then also `(x > z)`

This relationship can be used to define a binary relation:

* `R := (N,N,G)` and `(G subset-of NxN)`
* relation `R`, set of nodes `N`, graph `G`
* `sem(R)` := `aRb` iff `(a subsequent-to b)`

Node `y` is **strictly subsequent to (>>)** `x`, if `y` appears directly after
`x` (i.e. `y >> x`). The properties of this binary relation are:

* irreflexive, because `(x >> x)` is never true
* asymmetric, because if `(x >> y)`, then `(y >> x)` is not true
* not transitive, because if `((x >> y) and (y >> z))`, then only `(x >> y)`
* `y` is either the next sibling, or the first child of `x`

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

Example 1: `y` is the next sibling to `x`: If `x` has child nodes, then `y`
is only subsequent to `x`. If `x` has no child nodes, then `y` is strictly
subsequent to `x`. In both cases, `y` will be exited after `x` was exited.

Example 2: `y` is a child node of `x`: If `y` is the first child node, then `y`
is strictly subsequent to `x`, otherwise it is merely subsequent to it. In both
cases, `y` will be exited before `x` is exited.

### pre-sequent nodes

The "presequent" relations can be defined in a similar way:

* Node `x` is **presequent to (<)** `y`, if `(x < y)`
* Node `x` is **strictly presequent to (<<)** `y`, if `(x << y)`
* node `x` is **loosely presequent to** `y`, if `(x < y)` but not `(x << y)`

### clarifications

Note that, if `(x << y)`, then `x` is said to be **covered by** `y`. Likewise,
`y` is said to be covered by `x` (i.e. `covered-by` is undirected). In short:
`(x covered-by y)` iff `(x strictly-sequent-to y)`.

Note that the terms **consecutive** and **contiguous** are both closely related
to **strictly sequent** and only "loosely" related to **loosely sequent**.

<!-- ======================================================================= -->
## A general concept

The following definitions need to be understood to provide an abstract view
to classify the relationship between certain nodes and/or sequences.

* `ns` refers to the node sequence of a tree
* any `si` is assumed to be a subsequence of `ns`
* that is, `(si subsequence-of ns)` is true
* any `ni` is a node in `si` - i.e. `(n1 in s1)`
* any `ni` is also a node in `ns`

Note that, with regards to two distinct nodes `n1` and `n2` (i.e. `(n1 != n2)`)
of an ordered sequence, `n1` is either subsequent ex-or presequent to `n2`.

Note that the below statements assume the corresponding sequences to be
non-empty. In order to allow to make similar statements with regards to
empty sequences, additional information would have to be taken into account
(e.g. with regards to the defining node of an empty sequence).

<!-- ======================================================================= -->
## Sequences of (strictly) subsequent nodes

```
//- test sequence 's' with regards to node sequence 'ns'
//- i.e. 'ns' represents the current context
isSubsequent(ns, s) begin
  for (i in 1 to s.length-1) begin
    n1 = s(i), n2 = s(i+1)
    i1 = indexOf(ns, n1)
    i2 = indexOf(ns, n2)
    if (i1 >= i2) return false
  end
  return true
end
```

In the context of a tree's node sequence, a sequence of nodes is **a sequence
of subsequent nodes**, if any node within that sequence is (strictly or loosely)
subsequent to its predecessor.

Note that all nodes in the given sequence of nodes must be elements of the
tree's node sequence. In addition to that, the order of nodes in the given
sequence must correspond with the tree's node sequence.

Note that any sequence of subsequent nodes is an ordered sequence. In addition
to that, the input sequence is a mathematical/removal-based subsequence of the
tree's node sequence.

```
//- prototype with a similar definition
isStrictlySubsequent(nodeSequence, sequence)
```

A sequence of nodes is **a sequence of strictly subsequent nodes**, if
any node within that sequence is strictly subsequent to its predecessor.

* any sequence of subsequent nodes may contain
  subsequences of strictly subsequent nodes
* any sequence of strictly subsequent nodes
  is also a sequence of subsequent nodes
* any (concatenation-based) subsequence (aka. substring) of a
  tree's node sequence is a sequence of strictly subsequent nodes
* a tree's node sequence is a sequence of strictly subsequent nodes

There is no definition for **a sequence of loosely subsequent nodes**
because there are multiple options to define such a term:

1. all nodes have to be loosely subsequent to their predecessor
   (i.e. the sequence must not contain any strictly subsequent nodes)
2. at least one node is loosely subsequent to its predecessor
   (i.e. the sequence may still contain strictly subsequent nodes).

For the time being, such a definition is not required.

<!-- ======================================================================= -->
## Sequences subsequent to a node

```
               |-------------
n1 n2 n3 n4 n5 | n6 n7 n8 n9 
      ^        |-------------
      "n2"     "s1"
```

Note that these kind of "images" are intended to "visualize"
the general context of the corresponding section.

```
isSubsequentTo(ns, s1, n2) begin
  return isSubsequentTo(ns, s1(1), n2)
end
```

Sequence `s1` is **a sequence that is subsequent to a node**
`n2`, if the first node of `s1` is subsequent to `n2`
(i.e. `(n2 < s1[1])` or simply `(n2 < s1)`).

```
//- prototype with a similar definition
isStrictlySubsequentTo(ns, s1, n2)
```

Sequence `s1` is **a sequence that is strictly subsequent to a node**
`n2`, if the first node of `s1` is strictly subsequent to `n2`
(i.e. `(n2 << s1[1])` or simply `(n2 << s1)`).

```
//- prototype with a similar definition
isLooselySubsequentTo(ns, s1, n2)
```

Sequence `s1` is **a sequence that is loosely subsequent to a node**
`n2`, if the first node of `s1` is loosely subsequent to `n2`
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
isLeftSubsequentTo(ns, n1, s2) begin
  return isSubsequentTo(ns, n1, s2[1])
end

//- prototypes with a similar definition
isStrictlyLeftSubsequentTo(ns, n1, s2)
isLooselyLeftSubsequentTo(ns, n1, s2)
```

Note that the general notion of "left" is to "imply" that a node could be
within the corresponding sequence.

* left =!> outside (if not the first node)

Note that a node must be subsequent to the first node of the corresponding
sequence. Consequently, a sequence's first node is not considered to be
left-subsequent to its sequence. However, the first node of a sequence is
still an element of that sequence.

### right subsequent to

```
//- right: with regards to the sequence's last node
isRightSubsequentTo(ns, n1, s2) begin
  return isSubsequentTo(ns, n1, s2[s2.length])
end

//- prototypes with a similar definition
isStrictlyRightSubsequentTo(ns, n1, s2)
isLooselyRightSubsequentTo(ns, n1, s2)
```

Note that the general notion of "right" is to "imply" that a node is outside
of the corresponding sequence.

* (left and !right) => inside
* (left and right) => outside
* right => left

Note that a sequence's last node is not considered to be right-subsequent to
its sequence. That is because the last node is considered to be within the
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
isLeftSubsequentTo(ns, s1, s2) begin
  n1 = s1(1), n2 = s2(1)
  return isSubsequentTo(ns, n1, n2)
end

//- prototypes with similar definition
isStrictlyLeftSubsequentTo(ns, n1, n2)
isLooselyLeftSubsequentTo(ns, n1, n2)
```

Sequence `s1` is **a sequence that is left subsequent to a sequence**
`s2`, if `s1` is subsequent to the first node of `s2`
(i.e. `(s2[1] < s1[1])`).

Sequence `s1` is **a sequence that is strictly left subsequent to a sequence**
`s2`, if `s1` is strictly subsequent to the first node of `s2`
(i.e. `(s2[1] << s1[1])`).

Sequence `s1` is **a sequence that is loosely left subsequent to a sequence**
`s2`, if `s1` is loosely subsequent to the first node of `s2`
(i.e. if there are one or more nodes in between).

* strictly left subsequent => left subsequent
* left subsequent =!> strictly left subsequent
* a sequence that is left subsequent to another sequence
  may begin and may even end inside of it.

### right subsequent

```
isRightSubsequentTo(ns, s1, s2) begin
  n1 = s1(1), n2 = s2(#s2)
  return isSubsequentTo(ns, n1, n2)
end

//- prototypes with similar definition
isStrictlyRightSubsequentTo(ns, n1, n2)
isLooselyRightSubsequentTo(ns, n1, n2)
```

Sequence `s1` is **a sequence that is right subsequent to a sequence**
`s2`, if `s1` is subsequent to the last node of `s2`
(i.e. `(s2[#s2] < s1[1])`).

Sequence `s1` is **a sequence that is strictly right subsequent to a sequence**
`s2`, if `s1` is strictly subsequent to the last node of `s2`
(i.e. `(s2[#s2] << s1[1])`).

Sequence `s1` is **a sequence that is loosely right subsequent to a sequence**
`s2`, if `s1` is loosely subsequent to the last node of `s2`
(i.e. if there are one or more nodes in between).

* strictly right subsequent => right subsequent
* right subsequent =!> strictly right subsequent
* a sequence that is left, but not right subsequent to another sequence
  begins and may even end inside of it
* a sequence that is right subsequent to another sequence
  is also left subsequent to it
* a sequence `s1` that is strictly right subsequent to sequence `s2` is
  also strictly left subsequent to `s2`
