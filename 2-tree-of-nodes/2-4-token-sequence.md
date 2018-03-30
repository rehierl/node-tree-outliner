
<!-- ======================================================================= -->
# Token sequence

With regards to a tree's outline, any node has one of the following two 
characteristics: Entering and/or exiting a node either changes the current
outline by creating and/or closing sections, or it has no such effect at all.

When processing nodes that do not have an effect on the current outline (if
no node that has an effect on the current outline is located in between), it
does not matter if it is a single node, a subtree of such nodes, sequences
of subtrees of such nodes, or no such node at all: The current outline will
remain unchanged.

Replacing the tags of a tag sequence by tokens therefore allows to generalize
tag sequences into token sequences:

* Tokens in lower-case letters represent nodes that have an effect on
  the current outline. Each of these corresponds with a single node.
* Tokens in upper-case letters represent any number of nodes (single nodes,
  whole subtrees, sequences of subtrees, or no such node at all) that have
  no effect on the current outline. These kind of tokens can be seen as
  variables that represent any content which has no effect.

```
seq-0 := [body, #text, /#text, h1, #text, /#text, /h1, #text, /#text, h1,
          #text, /#text, /h1, #text, /#text, /body]

seq-1 := [body, A, /A, h1, B, /B, /h1, C, /C, h1, D, /D, /h1, E, /E, /body]

seq-2 := [body, h1, B, /B, /h1, h1, D, /D, /h1, /body]
```

Note that `seq-1` corresponds with `seq-2`, but not vice versa. These two
sequences are not equivalent because `seq-2` is, due to missing nodes, a
special case of `seq-1`.

```
<body>
  <h1>B</h1>
  <h1>D</h1>
  <div>
    F
  </div>
</body>
```

Token sequence `seq-1` can also be seen to correspond with this fragment (or
vice versa). Tokens A and C correspond with whitespace text nodes and token E
with subsequence `div, F, /div`).

In general, any token sequence corresponds with an infinite number of HTML
fragments that all have similar, if not identical, structure. By limiting ones
view to content that matters, token sequences can be used to describe certain
patterns of events.

As a flat list of tokens, a token sequence obfuscates the hierarchical structure
of a node tree. Care must be taken to not ignore a tree's actual structure.

<!-- ======================================================================= -->
## simplifications

The following simplifications may be used:

```
seq-1 := [body, A, /A, h1, B, /B, /h1, C, /C, h1, D, /D, /h1, E, /E, /body]

seq-2 := [body, A/, h1, B/, /h1, C/, h1, D/, /h1, E/, /body]

seq-3 := [body, A, h1, B, /h1, C, h1, D, /h1, E, /body]

seq-4 := [body, A, h1:B, C, h1:D, E, /body]
```

* A token of the form `name/` may be used to represent subsequences of the
  form `name, /name` (i.e. nothing in between).
* The final slash character `/` may be dropped, if it is clear that a token
  with no final slash character (i.e. `name` instead of `name/`) represents
  an enter *and* an exit event.
* Subsequences like `h1, B, /h1` may be merged into a single token `h1:B` if
  the inner nodes represented by token `B` are unimportant in a given context.

In general, tokens of the form `name:A` can be seen to represent all events
related to processing a container element that only has unimportant inner
content.

```
seq-4 := [body, A, h1:B, C, h1:D, E, /body]

seq-5 := [SR, A, h1:B, C, h1:D, E, /SR]
```

If the unique characteristics of a specific node is of no interest, constants
may be used to guide ones view to the relevant characteristics of a node:

* `SR` - some sectioning root element
* `SC` - some sectioning content element
* `HC` - some heading content element

<!-- ======================================================================= -->
## points of interest, cursors

```
seq-x := [body, A, /body]
                ^

seq-x := [body, A, /body]
          ^        ^

seq-x := [body, A, /body]
          1     2
```

* If a single point is of interest, a single `^` character may be used
  to point towards the relevant token.
* Multiple `^` characters may be used to point out the most critical parts
  within a given token sequence.
* If a following discussion needs to refer to multiple different points,
  then numbers may be used clearly identify the corresponding tokens.

<!-- ======================================================================= -->
## past, present and future

```
seq-5 := [SR, A, h1:B, C, h1:D, E, /SR]
                 ^

seq-6 := [BEGIN, SR, A, h1:B, C, h1:D, E, /SR, END]
          ^                                    ^
```

All operations associated with a single token need to be seen as being executed
in a single step (i.e. as a single atomic operation). As such, any pointer can
only refer to all operations (associated with that token) as a whole.

A token is said to have been executed if, and only if, all of the events that
are associated with it have been executed (partially executing a token is not
possible). If an inner substep of a token is relevant, the corresponding token
needs to be broken apart into separate tokens.

Placing a cursor at a certain point of interest has the following meaning:

* Any preceeding token was already executed (past).
* The token at the cursor's position is about to be executed (present).
* None of the subsequent tokens has been executed yet (future).

At no point within a sequence is it allowed to make any assumptions with
regards to subsequent/future tokens other than what is guaranteed by the
tree traversal itself:

* Each enter event corresponds with an exit event. This means that once
  some node was entered, it is guaranteed that, at some point, there will
  be a corresponding exit event.
* Unless guaranteed, it must not be assumed that, once some node was entered,
  another node with certain characteristics will be entered some time after,
  or even at all.
* Likewise, similar assumptions must not be made when exiting a node.

If needed, the following two constants may be used to indicate the beginning
and the end of processing a token sequence:

* `BEGIN` may be used to mark the beginning. This constant can be seen to
  correspond with operations needed to initialize a process (i.e. allocate
  certain resources). In short: The execution is about to begin.
* `END` may be used to mark the end. This constant can be seen to correspond
  with operations that are required to finalize a process (i.e. release
  certain resources). In short: The execution is about to end.

The `END` constant therefore has an additional meaning: That is, the last
token was already executed. Because of that, the traversal of the tree has
already ended. Consequently, no operation executed while processing the
`END` tag will have any effect on the result.
