
# Notes

<!-- ======================================================================= -->
## Open/Closed Sections

A section is considered open, if it is still allowed to associate entities
(nodes, headings, subsections) with it. A section has ended (is closed), if
that is no longer possible.

Similar to binary streams, certain resources (e.g. memory) are associated with
a section. These must be allocated (locked) when a section is opened and
released (freed, unlocked) when it is closed.

Once created, a new section object is automatically opened for associations.
As this step will lock resources, there needs to be a point for each section at
which its resources can be released. Ultimately, that point is reached for any
section when the traversing the tree has ended. But, at that point, certain
sections might no longer be accessible. As a result, resources allocated for
sections that are no longer accessible, will remain locked (e.g. memory leaks).

<!-- ======================================================================= -->
## Implied headings

The following cases need to be distinguished:

0. A section object is created and automatically opened for associations
   (i.e. `(section.heading == null)` is true).
1. A section is still open, but no heading element was associated with it
   (i.e. `(section.heading == null)` is still true).
2. The first heading element within an open section was visited.
   (i.e. `(section.heading != null)` is true - step F.1.1).
3. A section is closed, but no heading element was associated with it
   (i.e. `(section.heading == null)` is still true).
   The algorithm will then associate a pseudo heading (aka. implied heading)
   with it. From that point on, `(section.heading != null)` is true.

If an implied heading would not be associated with a closed section, the
expression `(section.heading == null)` would be ambiguous: It would be true for
a section that is open (1) and one that is closed (3). It would be impossible
to determine if a section is still open for associations or not.

1. `(section.heading == null)` states that a section that is open and that no
   heading was associated with it.
2. `(section.heading != null)` states that a section has a heading (open or
   closed), or an implied heading (closed) associated with it.

The expression `(section.heading != null)` therefore does not allow to determine
if it is still open or not. During that time, this expression is ambiguous (with
regards to a section's open-or-closed state).

Once the tree traversal is done, each section is either associated with a heading
or an implied heading (`(section.heading != null)` is true for any section --
That is at least the intention behind the concept of implied headings). From that
point on, this expression is no longer ambiguous because all sections are closed.

The expression `section.setImpliedHeading()` implicitly states, that the
corresponding section can be closed. It is an error to associate an implied
heading with a section that is still open and that has no heading associated
with it (because a heading element could still follow).

Overwriting an implied heading would also be an error, because this would
represent an attempt to continue a section that has already been closed. Once
resources associated with a section are released, they can no longer be accessed
(e.g. access violation).

<!-- ======================================================================= -->
### What is the rank of an implied heading?

**TODO** - Each heading element has a rank. The remaining questions are:
Is it necessary to associate a rank (highest or lowest) with an implied heading?
Does the algorithm implicitly associate a rank with an implied heading?

<!-- ======================================================================= -->
## Tag sequences

Walking over the nodes of a DOM tree in order to produce an outline needs to
execute the following pseudocode fragment:

```
visitNode(node)
  onEnter(node)
  child = node.firstChild
  while(child != null)
    visitNode(child)
    child = child.nextSibling
  onExit(node)
```

With some modifications, this fragment can be used to create a tag sequence:

```
visitNode(node, sequence)
  name = node.tagName.toLowerCase
  sequence.append(name)
  child = node.firstChild
  while(child != null)
    visitNode(child)
    child = child.nextSibling
  sequence.append("/" + name)
```

Executing that pseudocode with the following example HTML fragment as input ...

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
corresponds with the structure of one or more, possibly infinitely many, HTML
fragments that have identical structure.

<!-- ======================================================================= -->
## Token sequences

Switching ones own point of view allows to make the following observation: Tag
sequences can be seen to describe the sequence of events that will be triggered
when processing a document that has a structure which corresponds with a given
sequence.

With regards to a document's outline, any node has one of the following two 
characteristics: Entering and/or exiting a node either changes the current
outline by creating and/or ending sections, or it has no such effect.

When processing nodes that do not have an effect on the current outline, it does
not matter if it is a single node, a subtree of such nodes, sequences of subtrees
of such nodes, or no such node at all: The current outline will not change.

Replacing the tags of a tag sequence by tokens therefore allows to generalize
tag sequences as token sequences:

* Tokens in lower-case letters represent nodes that have an effect on
  the current outline. Each of these corresponds with a single node.
* Tokens in upper-case letters represent any number of nodes (single nodes,
  whole subtrees, sequences of subtrees, or no such node at all) that have no
  effect on the current outline. These kind of tokens are similar to variables
  that represent content which has no effect on the current outline.

The above tag sequence corresponds with the following token sequence:

```
seq-0 := [body, #text, /#text, h1, #text, /#text, /h1, #text, /#text, h1, #text,
          /#text, /h1, #text, /#text, /body]

seq-0 := [body, A, /A, h1, B, /B, /h1, C, /C, h1, D, /D, /h1, E, /E, /body]

seq-1 := [body, h1, B, /B, /h1, h1, D, /D, /h1, /body]
```

Note that `seq-0` also corresponds with `seq-1` (but not vice versa), because
`seq-1` is a special case of `seq-0`. Both sequences are therefore not entirely
equivalent.

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

Token sequence `seq-0` can also be seen to correspond with HTML fragment E-2
(or vice versa). Tokens A and C correspond with whitespace text nodes and token
E with the subsequence `div, F, /div`).

In general, any token sequence corresponds with an infinite number of HTML
fragments that all have similar, if not identical, structure. As such, token
sequences can be used to describe common patterns of events.

As a flat list of tokens, a token sequence obfuscates the hierarchical structure
of an HTML fragment. Care must be taken to not ignore the structure of a fragment.

<!-- ----------------------------------------------------------------------- -->
### Simplifications

The following simplifications may be used:

```
seq-0 := [body, A, /A, h1, B, /B, /h1, C, /C, h1, D, /D, /h1, E, /E, /body]

seq-1 := [body, A/, h1, B/, /h1, C/, h1, D/, /h1, E/, /body]

seq-2 := [body, A, h1, B, /h1, C, h1, D, /h1, E, /body]

seq-3 := [body, A, h1:B, C, h1:D, E, /body]
```

* A token of the form `name/` may be used to represent the subsequence
  `name, /name` (i.e. nothing in between).
* The final slash character `/` may be dropped, if it is clear that an un-slashed
  token (i.e. `name` instead of `name/`) represents an enter *and* an exit event
  at the same time.
* Subsequences like `h1, B, /h1` may be merged into a single token `h1:B`.

In general, tokens of the form `name:A` can be seen to represent all events
related to processing a container element that has non-substantial inner content.

```
seq-3 := [body, A, h1:B, C, h1:D, E, /body]

seq-4 := [SR, A, h1:B, C, h1:D, E, /SR]
```

If the unique characteristics of a specific node is of no interest, constants
may be used to guide ones view to a node's relevant characteristics:

* `SR` - some sectioning root element
* `SC` - some sectioning content element
* `HC` - some heading content element

Note that any token representing content, that has no effect on the current
outline, may correspond with content that contains inner sectioning root
elements. These elements have, by definition, no effect on the current outline.

<!-- ----------------------------------------------------------------------- -->
### Points of interest, Cursors

```
seq-x := [body , A , /body]
          ^        ^

seq-x := [body , A , /body]
          0        1
```

If a single point is of interest, a single `^` character may be used to point
out the relevant location. Multiple `^` characters may be used to point out the
most critical parts within a given sequence. If a following discussion needs to
refer to multiple different points, numbers may be used clearly identify these.

```
seq-x := [..., A, ...] = [..., A , /A, ...]
               ^                 ^
```

All operations associated with a single token need to be seen as being grouped
into a single atomic operation and as being executed in one step. As such, any
pointer can only refer to all associated operations as a whole. If an inner
substep of such an atomic operation is relevant, the corresponding token needs
to be split up into separate tokens.

<!-- ----------------------------------------------------------------------- -->
### Past, present, future

```
seq-0 := [body, A, /A, h1, B , /B, /h1, C, /C, h1, D, /D, /h1, E, /E, /body]
                             ^
```

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

<!-- ======================================================================= -->
## The current/active section

* At any given time, multiple sections can be open.
* Only one open section is considered to be the current/active section.
