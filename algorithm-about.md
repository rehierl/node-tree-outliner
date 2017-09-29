
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
a heading can still be associated with the corresponding section because that
section is still open. -- This is at least the intention behind implied headings.

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
## HTML-4 heading elements

In HTML-4, any heading element is defined to introduce (i.e. mark the beginning
of) a new section.

Note that there seems to exist no explicit definition which states when such a
section ends. The only definitive statement that can be made right away is that:
If no other rule applies, any remaining open section ends with the body element.

```
Example:
========
<body>
  <h1>A</h1>
  B
</body>
```

In general, the table of contents (TOC) of this fragment is as follows:

```
TOC:
====
1. A
```

Questions start to arise as soon as that fragment is slightly modified:

```
Example:
========
<body>
  A
  <h1>B</h1>
  C
</body>
```

Obviously, node `A` must belong to some section, because that node can not be
ignored. As a direct consequence, heading elements are not the only elements in
HTML-4, that have the ability to introduce new sections.

There are two possible ways to print a TOC for the modified fragment:

```
TOC-1:                          TOC-2:
======                          ======
1. Untitled section             1. Untitled section
2. B                               1.1. B
```

Both TOCs are obviously not equivalent because each of these represents a
different structure. As a result, only one of these truly represents the
fragment's structure, the other one does not. So which of these is invalid?

### Relationship between sections and nodes

From a node's perspective: Any node within a document always belongs to (i.e. is
located in) some section, regardless if that section has a title or not. In
addition to that, no node can have a direct relationship with (i.e. is associated
with) two different sections at the same time. In short: Any node either directly
belongs to some section, or it belongs to a different one. Note that multiple
different nodes may belong to the same section.

From a section's perspective: Any section always directly contains (i.e. is
associated with) no node at all, a single node or more than one (in theory even
infinitely many) nodes. Note that a section, that does not directly contain any
nodes, does not have to be empty (i.e. these sections may still contain
subsections - see below).

The direct relationship between sections and nodes can therefore be classified
as a two-way one-to-many (i.e. 1:N) relationship.

In order to simplify discussion, assume that any heading element can be uniquely
identified by the heading's inner nodes. Likewise, assume that any section
introduced by a heading element can be identified by the inner nodes of the
heading element that introduced said section.

```
Example:
========
<body>
  <h1>A</h1>
  B
</body>
```

In this example, heading `A` is said to introduce section `A`. In addition to
that, and because node `B` is located inside section `A`, node `B` is said to
belong to section `A`. In short: Node `B` is associated with section `A`.

Note that node `B` is located inside section `A` because there is nothing that
introduces a new section in between heading `A` and node `B`. There is also
nothing that indicates that section `A` ends before node `B` is reached.

### Relationship between sections

```
Example:
========
<body>
  <h1>A</h1>
  B
  <h2>C</h2>
  D
</body>
```

The general consensus to print the TOC for this fragment is as follows:

```
TOC:
======
1. A
   1.1. C
```



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
## The current/active section

* At any given time, multiple sections can be open.
* Only one open section is considered to be the current/active section.
