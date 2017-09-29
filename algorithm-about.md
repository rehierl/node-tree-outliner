
# Notes

<!-- ======================================================================= -->
## Open/Closed Sections

A section is considered open, if it is still allowed to associate entities
(nodes, a heading and subsections) with it. A section is closed (has ended), if
that is no longer allowed.

Similar to binary streams, certain resources (e.g. memory) will be associated
with a section. These must be allocated (locked) when a section is opened and
released (freed, unlocked) when it is closed.

Once created, a new section object is automatically opened for associations.
As this step will allocate resources, there needs to be a point for each section
at which these can be released.

Ultimately, that point is reached for any section when tree traversal ends. But,
at that point, certain sections might no longer be accessible. In such a case,
resources allocated for sections that are no longer accessible will remain
locked (e.g. memory leaks).

<!-- ======================================================================= -->
## Implied headings

During tree traversal, the following states can be observed:

0. A section object is created and automatically opened for associations
   (i.e. `(section.heading == null)` is true).
1. A section is still open, but no heading was associated with it
   (i.e. `(section.heading == null)` is still true).
2. The first heading element within an open section was entered and associated
   with that section (i.e. `(section.heading != null)` is true - step F.1.1).
3. A section has ended and *a heading* element was associated with it
   (i.e. `(section.heading != null)` remains to be true).
4. A section has ended and *no heading* element was associated with it
   (i.e. `(section.heading == null)` remains to be true).

From these states, the following statements can be derived:

1. The expression `(section.heading == null)` is true for sections that
   have *no heading* and that are either *open or closed*.
2. The expression `(section.heading != null)` is true for sections that
   have *a heading* and that are either *open or closed*.

Note that both expressions are ambiguous with regards to a section's
is-open-or-closed state.

Obviously, it would be preferable to have a dedicated is-open-or-closed state
property for each section. But, such a property would only have a use for as
long as tree traversal has not finished. Once tree traversal is done, all
sections are closed and such a property would hold the exact same value for any
section (i.e. such a state property would be wasting memory).

The current algorithm will therefore associate a non-null pseudo heading
(aka. implied heading) with a section that has ended and that has no heading.
This allows to make the following statements:

1. The expression `(section.heading == null)` is true for sections that
   have *no heading* and that are *still open*.
2. The expression `(section.heading != null)` is true for sections that
   have *a heading* (implied or not) and that are either *open or closed*.

Therefore, if expression (1) (i.e. `section.hasNoHeading()`) evaluates to true,
a heading can still be associated with the corresponding section. --
This is at least the intention behind the concept of implied headings.

Obviously, it would be an error to associate an implied heading with an open
section that has no heading (because a heading element could still follow). As
a result, the expression `section.setImpliedHeading()` implicitly states, that
the corresponding section has no heading *and* that it has ended.

Overwriting an implied heading would also be an error, because this would
represent an attempt to continue a section that has already ended. Once a
section ends, any resources associated with it can be released. After that,
those resources can no longer be accessed because any such attempt would
inevitably trigger an access violation error.

**TODO** - Each heading element has a rank.
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
therefore corresponds with the structure of one or more, possibly infinitely
many, HTML fragments that have identical structure.

<!-- ======================================================================= -->
## Token sequences

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
## HTML-4 heading elements

In HTML-4, any heading element is defined to introduce (i.e. mark the beginning
of) a new section.

Note that there is no explicit definition which states when such a section ends.
The only definitive statement that can be made right away is that: Any remaining
open section ends with the body element.

```
Example 3 (E-3):
================

<body>
  <h1>A</h1>
  B
</body>
```

In general, E-3's table of contents (TOC) is as follows:

```
1. A
```

Questions start to arise as soon as example E-3 is slightly modified:

```
Example 4 (E-4):
================

<body>
  A
  <h1>B</h1>
  C
</body>
```

There are two possible ways to print E-4's TOC:

```
TOC-1:                          TOC-2:
======                          ======

1. Untitled section             1. Untitled section
2. B                               1.1. B
```

Both TOCs are obviously not equivalent because they represent different structures.
As a result, only one of these TOCs truly represents E-4's structure, the other
one does not. So which of these is invalid?

### Relationship between sections and nodes

Any node within a document always belongs to (i.e. is located in) some section,
regardless if that section has a title or not. In addition to that, no node can
have a direct relationship with (i.e. is associated with) two different sections
at the same time. In short: Any node either belongs to some section, or it is
located in a different one.

From a section's perspective: Any section is always directly contains (i.e. is
associated with) no node at all, a single node or more than one (in theory even
infinitely many) nodes.

The direct relationship between sections and nodes can therefore be classified
as a two-way one-to-many (i.e. 1:N) relationship.

In order to simplify discussion, assume that any heading element can be uniquely
identified by the heading's inner nodes. Likewise, any section introduced by a
heading element can be identified by the inner nodes of the heading element that
introduced said section.

In example E-4, heading `B` is said to introduce section `B`. In addition to that,
and because node `C` is located inside section `B`, node `C` is said to belong to
section `B`. In short: Node `C` is associated with section `B`.

### Relationship between sections

```
Example 5 (E-5):
================

<body>
  <h1>A</h1>
  B
  <h2>C</h2>
  D
</body>
```

The general consensus to print E-5's TOC is as follows:

```
TOC-3:
======

1. A
   1.1. C
```

As a result, any document can be broken up into sections that do not overlap
with regards to this direct relationship between sections and nodes.

### Where does a section end?

### Continue...

```
Example 5 (E-5):
================

<h1>A</h1>
B
<h2>C</h2>
D
```

The partial TOC of the above fragment is:

```
TOC-3:
======

1. A
   1.1. C
```

HTML-4 associates a level of importance with each heading with `h1` representing
the most and `h6` the least important heading.

However, any section of a document always has some relationship with all other
sections of the same document.

Between any two sections of the same document there
exists a path that can be used to traverse from one section to another. 

The most important ones are the following two direct
relationships:

* A section may directly follow another one.
* A section may be a direct subsection to another one.

Some section can
be more important (superordinate) than another one (subordinate), which means that
a section may contain subsections.

As a result, any node has a direct relationship with a section and, in addition
to that, possibly infinitely many indirect
relationships with other sections.

Obviously, `A` must belong to some section because the corresponding nodes simply
can not be ignored. As a result, `h1`'s section has content that is preceeding it,
or (put differently) `h1`'s section has some relationship with an untitled section.

The problem therefore is to decide what the relationship between both sections
is: Does heading element `h1` introduce a section that is on the same level as
the section that implicitly precedes it, or does the heading element introduce
a section that is on a different level?

So the actual question that must be answered is:
Does that heading element introduce **a section, or a sub-section**?

### Where does a heading's section end?

Obviously, any section has to end as soon as body's end tag is reached, because
no content node will ever appear beyond that point. This observation is of course
not helpful because it does not allow to derive a statement that allows to answer
the above question.

There is nothing that indicates that the heading's section ends before the
implicit section that precedes it. Anything between the heading element's start
and end tag defines the section's title. A heading element itself does not define
where its section ends. Better, but still not good enough.

The situation starts to improve as soon as one takes a closer look at the example
of the [HTML 4 spec](https://www.w3.org/TR/html401/struct/global.html#h-7.5.5):

```
Example 5 (E-5):
================

<div class="section">
  <h1>A</h1>
  
  <div class="subsection">
    <h2>B</h2>
  </div>
</div>
```

The obvious intention behind surrounding a heading element with a parent `div`
container is that the heading's section is supposed to end with the parent
container element.

Note that, despite the parent container element, the section is still introduced
by the heading element, not by the parent container element. A `div` element
is still defined merely as a "generic mechanism for adding structure to
documents" - nothing more.

If a `div` container would introduce a new section, titled or not, then any `div`
container would suddenly introduce its own section. By that change, authors would
loose the ability to group nodes without changing a document's outline.

The important questions here are if E-5's structure adds new characteristics to
`div` container elements or not:

* Can `div` elements end a section?
* 

The answer here must be a decisive "No!", because any section must end with its
parent container element. This characteristic is independent of which kind of
container element it is surrounded.

(Note here, that any section is always
surrounded by some container element, the topmost container element is the `body`

```
Example 6 (E-6):
================

<X>
  <h1>A</1>
</X>
B
```

To answer that question, one must decide if node `B` can be associated with
the heading's section or not.

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
