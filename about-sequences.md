
# Notes

<!-- ======================================================================= -->
## Tree traversal

* [en.wikipedia.org, tree traversal](https://en.wikipedia.org/wiki/Tree_traversal)
* [en.wikipedia.org, depth-first search (DFS)](https://en.wikipedia.org/wiki/Depth-first_search)

In order to create an outline that accurately represents a document's structure,
the document's DOM tree must be traversed by visiting each node. In general,
the traversal of such a node tree can be classified depending on certain
characteristics - such as:

* When is a node visited in relation to its child nodes? -
  e.g. depth-first search (DFS), breadth-first search (BFS)
* In which order are the child nodes visited? - e.g. left-to-right (LTR)
  (aka. first-to-last (FTL)), right-to-left (RTL) (aka. last-to-first (LTF))

### Depth-first search (DFS)

The traversal of a tree is referred to as a depth-first (DFS) search, if all
the nodes of a branch are visited before the nodes any other branch.

**FTL, DFS, Pre-order tree traversal**

```
traversePreOrder(node) begin
  visitPreOrder(node)
  child = node.firstChild
  while(child != null) begin
    traversePreOrder(child)
    child = child.nextSibling
  end
end
```

The `visitPreOrder()` operation marks the beginning of processing a node.
It therefore represents a node's enter event.

**FTL, DFS, Post-order tree traversal**

```
traversePostOrder(node) begin
  child = node.firstChild
  while(child != null) begin
    traversePostOrder(child)
    child = child.nextSibling
  end
  visitPostOrder(node)
end
```

The `visitPostOrder()` operation marks the end of processing a node.
It therefore represents a node's exit event.

**FTL, DFS, In-order**

```
traverseInOrderBin(node) begin
  traverseTree(node.left)
  traverseInOrderBin(node)
  traverseTree(node.right)
end
```

The in-order tree traversal of a binary tree is a strict tree traversal because
each node is visited exactly once. Traversing a non-binary tree, that allows more
than two child nodes per node (the DOM tree is such a generic tree), via in-order
tree traversal would have to execute the visit operation multiple times per node:

```
traverseInOrder(node) begin
  child = node.firstChild
  while(child != null) begin
    visitInOrderBefore(node)
    traverseInOrder(child)
    visitInOrderAfter(node)
    child = child.nextSibling
  end
end
```

It does not matter if either `visitInOrderBefore()`, or `visitInOrderAfter()`,
or even both are used. Both will be executed multiple times per node. An in-order
tree traversal of a generic tree is therefore no traversal that corresponds with
the strict definition of a tree traversal.

### Breadth-first (BFS) search

A tree traversal is referred to as a breadth-first (BFS) search, if the nodes
of a tree are visited one level at a time.

**FTL, BFS**

```
//- visit the nodes in a given range of (relative) levels
//- node.level in [1,+Infinity] returns a node's (absolute) level
//- the root node of a tree has a level value of 1

traverseBFS(root, min, max) begin
  assert((min >= 1) && (max >= 1) && (min <= max))

  queue = new Queue()
  queue.enqueue(root)

  while(not queue.isEmpty) begin
    node = queue.dequeue()

    //- the node's relative level
    level = 1 + (node.level - root.level)

    if(level in [min,max]) begin
      visitBFS(node)
    end

    child = node.firstChild
    while(child != null) begin
      queue.enqueue(child)
      child = child.nextSibling
    end
  end
end
```

Executing `traverseTree(node, 1, 1)` (= **BFS-1**) will only visit the 1st level,
which only contains the specified node. Executing `traverseTree(node, 2, 2)`
(= **BFS-2**) will only visit the 2nd level, which only contains a node's
immediate descendants (i.e. child nodes).

### Tree Traversal

```
traverseTree(node) begin
  onEnter(node)
  child = node.firstChild
  while(child != null) begin
    traverseTree(child)
    child = child.nextSibling
  end
  onExit(node)
end
```

In order to create the outline for a document, an algorithm needs to execute
certain actions depending on which node is being processed.

When a node is entered, an algorithm has to:

* end outer sections
* associate the node being entered with a section
* suspend an outer section
* create and initialize a new inner section

When a node is exited, an algorithm has to:

* end inner sections
* reactivate an outer section, or
* create and initialize a new one

Which of these actions need to be executed must be defined for each node type.

<!-- ======================================================================= -->
## Node sequences

The above tree traversal fragment can be used to produce a sequence of nodes that
contains the nodes of a document in the order in which these nodes are entered:

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

The sequence of nodes created this way is said to be **the document's sequence
of nodes**, or simply the document's **node sequence**. As such, a node sequence
represents the path an algorithm will take through a document when traversing
its tree of nodes.

A memory hook: The start tags of an HTML file have the exact same order.

### Subsequent nodes

```
indexOf(sequence, node) begin
  for(i in 0 to sequence.length-1) begin
    if(sequence(i) == node) then
      return i
    end
  end
  throw error
end

//- distanceBetween(n1, n2) := (indexOf(n2) - indexOf(n1))
//- the result is negative, if n2 appears before n1

distanceBetween(sequence, n1, n2) begin
  i1 = indexOf(sequence, n1)
  i2 = indexOf(sequence, n2)
  return (i2 - i1)
end

isSubsequentTo(sequence, n1, n2) begin
  return (distanceBetween(sequence, n1, n2) >= 1)
end

isDirectlySubsequentTo(sequence, n1, n2) begin
  return (distanceBetween(sequence, n1, n2) == 1)
end
```

With regards to some node sequence, `Y` is said to be **(merely) subsequent to**
`X`, if `Y` appears after `X` in that sequence. Node `Y` is said to be
**directly subsequent to** `X`, if `Y` appears directly after `X`.

Consequently, a node that is directly subsequent to another node is also
subsequent to it. In contrary to that, a node that is subsequent to another
node is not necessarily directly subsequent to it (because there could be any
number of other nodes in between).

This relationship is not reflexive because node `X` can not appear after node
`Y` and `Y` after `X` at the same time. It is therefore an error to state that
two nodes are subsequent to each other.

This relationship is however transitive, because if `Y` is subsequent to `X`
and `Z` to `Y`, then `Z` is automatically subsequent to `X`
(i.e. if `((X < Y) && (Y < Z))`, then `(X < Z)`).

The structural relationship between `X` and `Y` (i.e. Where inside the DOM tree
is `X` located in relation to `Y`?) can not be determined if `Y` is (directly)
subsequent to `X`. This relationship merely states that `Y` will be entered after
`X`. Consequently, it can also not be determined if `Y` will be exited before or
after `X` is (or was) exited:

Example (1): `Y` is next sibling to `X`: If `X` has child nodes, then `Y` is
merely subsequent to `X`. If `X` has no child nodes, then `Y` is directly
subsequent to `X`. In both cases, `Y` will be exited after `X` was exited.

Example (2): `Y` is a child node of `X`: If `Y` is the first child node, then
`Y` is directly subsequent to `X`, otherwise it is merely subsequent to it. In
both cases, `Y` will be exited before `X` is exited.

### Sequence of subsequent nodes

```
isSubsequent(docSequence, sequence) begin
  for(i in 0 to sequence.length-2) begin
    n1 = sequence(i), n2 = sequence(i+1)
    if(not isSubsequentTo(docSequence, n1, n2)) then
      return false
    end
  end
  return true
end

isDirectlySubsequent(docSequence, sequence) begin
  for(i in 0 to sequence.length-2) begin
    n1 = sequence(i), n2 = sequence(i+1)
    if(not isDirectlySubsequentTo(docSequence, n1, n2)) then
      return false
    end
  end
  return true
end
```

A sequence of nodes is said to be **a sequence of (merely) subsequent nodes**,
if any node within that sequence is subsequent to its predecessor.

A sequence of nodes is said to be **a sequence of directly subsequent nodes**,
if any node within that sequence is directly subsequent to its predecessor.

Consequently, the node sequence of a document is a sequence of directly
subsequent nodes. The same obviously applies to all the subsequences of a node
sequence.

Also, any sequence of subsequent nodes may contain subsequences that are directly
subsequent (i.e. if a sequences is itself not directly subsequent, then portions
of such a sequence may still be directly subsequent).

<!-- ======================================================================= -->
## Section

A **section** is a sequence of subsequent nodes.

This definition does not state anything about a section's first and last nodes.
It merely states that a section is not some sequence of arbitrarily selected
nodes. The order of the nodes associated with a section always corresponds with
the document's node sequence.

explain ...

A section that has no subsections is a sequence of directly subsequent nodes.
Consequently, such a section is a subsequence of its document's node sequence.

*From the perspective of subsequences:*
A section that has subsections is a sequence of directly subsequent nodes, if
it is considered to also contain all nodes within all of its subsections.

*From the perspective of objects directly connected with each other:*
A section is a sequence of sequences of directly subsequent nodes, if the nodes
of its subsections are considered to be *not* included (i.e. `section := [
sequence-1, sequence-2, ...]`). All subsections of a section can therefore be
seen to fill the gaps in between the sequences of a section.

### Sequence of subsequent sections - TODO

Document = sequence of subsequent sections -

Any section has a node that precedes it (i.e. the section's sectioning element).

A section is a subsection to the outer section of its sectioning element. Put
differently, the outer section of a sectioning element tells the section that
is introduced to which section it is a subsection.

The section of a sectioning root belongs to a document. As such, it contributes
to the outline (tree of sections) of its document. The choice to not include
such an inner outline in a document's TOC is a choice by preference, (i.e. not
a strict requirement).

<!-- ======================================================================= -->
## Tag sequence

The above tree traversal fragment can also be used to produce a sequence of tags:

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

The sequence of tags created this way is said to be **the document's tag
sequence (TS)**.

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
therefore corresponds with the structure of one or more, possibly infinitely
many, HTML fragments that have identical structure.

<!-- ======================================================================= -->
## Token sequence

Switching ones own point of view allows to make the following observation: Tag
sequences can be seen to describe the sequence of events that will be executed
when processing a document that matches the given sequence (i.e. the document's
structure corresponds with the sequence).

With regards to a document's outline, any node has one of the following two 
characteristics: Entering and/or exiting a node either changes the current
outline by creating and/or ending sections, or it has no such effect at all.

When processing nodes that do not have an effect on the current outline (if no
node has an effect on the current outline is located in between), it does not
matter if it is a single node, a subtree of such nodes, sequences of subtrees
of such nodes, or no such node at all: The current outline will not change.

Replacing the tags of a tag sequence by tokens therefore allows to generalize
tag sequences into token sequences:

* Tokens in lower-case letters represent nodes that have an effect on
  the current outline. Each of these corresponds with a single node.
* Tokens in upper-case letters represent any number of nodes (single nodes,
  whole subtrees, sequences of subtrees, or no such node at all) that have no
  effect on the current outline. These kind of tokens can be seen as variables
  that represent any content which has no effect.

The above tag sequence therefore corresponds with token sequence `seq-1`:

```
seq-0 := [body, #text, /#text, h1, #text, /#text, /h1, #text, /#text, h1, #text,
          /#text, /h1, #text, /#text, /body]

seq-1 := [body, A, /A, h1, B, /B, /h1, C, /C, h1, D, /D, /h1, E, /E, /body]

seq-2 := [body, h1, B, /B, /h1, h1, D, /D, /h1, /body]
```

Note that `seq-1` corresponds with `seq-2`, but not vice versa. These two
sequences are not equivalent because `seq-2` is a special case of `seq-1`.

```
Example 2 (E-2):
----------

<body>
  <h1>B</h1>
  <h1>D</h1>
  <div>
    F
  </div>
</body>
```

Token sequence `seq-1` can also be seen to correspond with fragment E-2 (or
vice versa). Tokens A and C correspond with whitespace text nodes and token E
with subsequence `div, F, /div`).

In general, any token sequence corresponds with an infinite number of HTML
fragments that all have similar, if not identical, structure. By limiting ones
view to content that matters, token sequences can be used to describe certain
event patterns.

As a flat list of tokens, a token sequence obfuscates the hierarchical structure
of an HTML fragment. Care must be taken to not ignore a fragment's structure.

### Simplifications

The following simplifications may be used:

```
seq-1 := [body, A, /A, h1, B, /B, /h1, C, /C, h1, D, /D, /h1, E, /E, /body]

seq-2 := [body, A/, h1, B/, /h1, C/, h1, D/, /h1, E/, /body]

seq-3 := [body, A, h1, B, /h1, C, h1, D, /h1, E, /body]

seq-4 := [body, A, h1:B, C, h1:D, E, /body]
```

* A token of the form `name/` may be used to represent subsequences of the form
  `name, /name` (i.e. nothing in between).
* The final slash character `/` may be dropped, if it is clear that a token with
  no final slash character (i.e. `name` instead of `name/`) represents an enter
  *and* an exit event.
* Subsequences like `h1, B, /h1` may be merged into a single token `h1:B` if the
  inner nodes represented by token `B` are not important in a given context.

In general, tokens of the form `name:A` can be seen to represent all events
related to processing a container element that only contains unimportant inner
content.

```
seq-4 := [body, A, h1:B, C, h1:D, E, /body]

seq-5 := [SR, A, h1:B, C, h1:D, E, /SR]
```

If the unique characteristics of a specific node is of no interest, constants
may be used to guide ones view to a node's relevant characteristics:

* `SR` - some sectioning root element
* `SC` - some sectioning content element
* `HC` - some heading content element

### Execution, inner and outer effect/view

Any token that represents content which has no effect on the current outline may
correspond with content that contains inner sectioning root elements. These
elements have by definition no effect on the current outline (i.e. they do not
contribute to the outline of an ancestor).

Sectioning content elements are different in that they have an effect on the
current outline: By definition, sectioning content elements contribute to the
outline of an ancestor. As such, no token that represents content which has no
effect on the current outline can correspond with content that contains an inner
sectioning content element.

**TODO** - expand

### Points of interest, Cursors

```
seq-x := [body, A, /body]
                ^

seq-x := [body, A, /body]
          ^        ^

seq-x := [body, A, /body]
          1     2
```

* If a single point is of interest, a single `^` character may be used to point
  out the relevant location.
* Multiple `^` characters may be used to point out the most critical parts
  within a given sequence.
* If a following discussion needs to refer to multiple different points, numbers
  may be used clearly identify these.

### Past, present and future

```
seq-5 := [SR, A, h1:B, C, h1:D, E, /SR]
                 ^

seq-6 := [BEGIN, SR, A, h1:B, C, h1:D, E, /SR, END]
          ^                                    ^
```

All operations associated with a single token need to be seen as being executed
in a single step (i.e. as a single atomic operation). As such, any pointer can
only refer to all associated operations as a whole.

A token is said to have been executed if, and only if, all of the events that
are associated with it have been executed (partially executing a token is not
possible). If an inner substep of a token is relevant, the corresponding token
needs to be broken apart into separate tokens.

Placing a cursor at a certain point of interest has the following meaning:

* Any preceeding token was already executed (past).
* The token at the cursor's position is about to be executed (present).
* None of the subsequent tokens has been executed yet (future).

At no point within a sequence is it allowed to make any assumptions with regards
to subsequent/future tokens other than what is guaranteed by HTML or the tree
traversal itself:

* Each enter event corresponds with an exit event. This means that once some node
  was entered, it is guaranteed that, at some point, there will be corresponding
  exit event.
* Unless guaranteed by HTML, it must not be assumed that, once some node was
  entered, another node with certain expected characteristics will be entered
  some time after (or even at all).
* Likewise, similar assumptions must not be made when exiting a node.

If needed, the following two constants may be used to indicate the beginning
and the end of processing a token sequence:

* `BEGIN` may be used to mark the beginning. This constant can be seen to
  correspond with operations needed to initialize a sequence's execution (i.e.
  allocate certain resources). In short: The execution is about to begin.
* `END` may be used to mark the end. This constant can be seen to correspond
  with operations that are needed to finalize a sequence's execution (i.e.
  release certain resources). In short: The execution is about to end.

The `END` constant therefore has the additional meaning, that the last token
was already executed (i.e. traversal of the subtree has already ended).

<!-- ======================================================================= -->
## Stack of open sections

Traversing the relevant tree in order to produce an outline needs to (implicitly
or explicitly) create and update stacks of open sections.

```
Example 3 (E-3):
----------------

<h1>A</h1>
B
<h2>C</h2>
D
<h3>E</h3>
F
<h2>G</h2>
H
```
