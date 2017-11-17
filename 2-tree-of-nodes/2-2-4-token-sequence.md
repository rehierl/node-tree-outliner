
<!-- ======================================================================= -->
# Token sequence

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

<!-- ======================================================================= -->
## Simplifications

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

<!-- ======================================================================= -->
## Execution, inner and outer effect/view

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

<!-- ======================================================================= -->
## Points of interest, Cursors

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

<!-- ======================================================================= -->
## Past, present and future

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
