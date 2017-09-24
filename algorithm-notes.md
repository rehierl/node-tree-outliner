
# Notes

<!-- ======================================================================= -->
## Open/Closed Sections

A section is considered open, if it is still allowed to associate entities
(notes, headings, subsections) with it. A section has ended (is closed), if
that is no longer possible.

Similar to binary streams, certain resources (e.g. memory) are associated with a
section. These must be allocated (locked) when a section is opened and released
(freed, unlocked) when it is closed.

Once created, a new section object is automatically opened for associations. As
this step will lock resources, there needs to be a point for each section at
which locked resources can be released. Ultimately, that point is reached for
any section when the tree traversal ends. But, at that point, certain sections
might no longer be accessible. As a result, resources allocated for sections
that are no longer accessible, will remain locked (e.g. memory leaks).

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

**TODO** - Each heading element has a rank. The remaining questions are:
Is it necessary to associate a rank (highest or lowest) with an implied heading?
Does the algorithm implicitly associate a rank with an implied heading?

<!-- ======================================================================= -->
### Tag sequences

Walking over the nodes of a DOM tree in order to produce an outline can be seen
as executing the following pseudocode fragment:

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

Executing that pseudocode with the following HTML fragment as input ...

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

Any tag in such a sequence is the result of the corresponding enter or exit
event: start tag `name` represents an enter and end tag `/name` an exit event.
Any tag sequence therefore corresponds with the structure of one or more,
possibly even infinitely many, HTML fragments that have identical structure.

<!-- ======================================================================= -->
## Token sequences

Each tag in a tag sequence corresponds with a single node. Replacements are
therefore required in order to use such sequences as an analytical tool:



be used to describe sequences of events that will happen when processing
fragments whose structure matches a given token sequence.



of infinitely many HTML fragments. As such, each token
sequence can represent infinitely tag sequences.

Therefore, those tag sequences are referred to as token sequences, with
each token representing the corresponding operation.


from being a result of a 

Unfortunately, such a sequence is difficult to follow because the tokens related
to text nodes can not be distinguished from one another:

```
seq-0 := [body, A, /A, h1, B, /B, /h1, C, /C, h1, D, /D, /h1, E, /E, /body]
```

* In general, text related tokens should be replaced by one that best reflects
  the corresponding text node (e.g. `A` instead of `#text`).
* To clearly distinguish these from element related tokens, element names should
  be displayed using lower-case and text related nodes using upper-case letters.

Strictly, tokens A through E, represent text nodes that are entered and immediately
exited (they have no child nodes). These kind of nodes have no side effect in a
given context. As such, these tokens can also be seen to represent enter or exit
events related to any possible subtree that has the same characteristic (i.e. no
side effect in a given context). - placeholder, variable, pattern, ...

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

`seq-0` can also be seen to represent the HTML fragment E-2. Nodes A and C
represent whitespace text nodes and node E the subsequence `div, F, /div`).

Generalized: Any token sequence represents an infinite number of HTML fragments
that all have similar, if not identical, semantics.

As a flat list of tokens, a token sequence obfuscates the hierarchical structure
of an HTML fragment. Care must be taken to not ignore the structure of a fragment.

<!-- ----------------------------------------------------------------------- -->
### Simplifications

The following simplifications can be used:

```
seq-0 := [body, A, /A, h1, B, /B, /h1, C, /C, h1, D, /D, /h1, E, /E, /body]

seq-1 := [body, A/, h1, B/, /h1, C/, h1, D/, /h1, E/, /body]

seq-2 := [body, A, h1, B, /h1, C, h1, D, /h1, E, /body]

seq-3 := [body, A, h1:B, C, h1:D, E, /body]
```

* Sequence `seq-0` can be simplified as seen in `seq-1`:
  A token of the form `name/` represents the subsequence `A, /A`.
* If tokens allow to clearly distinguish nodes that have no side effect from
  those that do have some side effect in a given context (e.g. upper-case vs.
  lower-case letters), the final slash character may even be dropped (`seq-2`):
  A token of the form `A` may represent the subsequence `A, /A`.
* Depending on a given context, it is even possible to further merge
  subsequences like `h1, B, /h1` into a single token `h1:B` (`seq-3`).

```
seq-3 := [body, A, h1:B, C, h1:D, E, /body]

seq-4 := [SR, A, h1:B, C, h1:D, E, /SR]
```

If the unique characteristics of a specific node is of no interest, constants
may be used to guide ones view to a node's relevant characteristics:

* `SR` - some sectioning root element
* `SC` - some sectioning content element
* `HC` - some heading content element

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
