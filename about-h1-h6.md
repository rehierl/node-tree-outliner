
# HTML-4 heading elements

* [HTML-4, 7.5.5 Headings](https://www.w3.org/TR/html401/struct/global.html#h-7.5.5)

<!-- ####################################################################### -->
## Introduction

In HTML-4, each heading element is defined to introduce (i.e. mark the beginning
of) a new section.

Note that there seems to exist no explicit definition which states when such a
section ends. The only statement that can be made right away is that
**by default, any section ends with the body element.**

```
Example:
========
<body>
  <h1>A</h1>
  B
</body>
```

The the consensus to print the table of contents (TOC) for this fragment is:

```
TOC:
====
1. A
```

A slight modification of the above fragment reveals that this TOC can only be a
commonly accepted simplification:

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
ignored. As a consequence, and even in HTML-4, **heading elements are not the
only elements that introduce new sections.**

There are two possible ways to print a TOC for this modified fragment:

```
TOC-1:                          TOC-2:
======                          ======
1. Untitled section             1. Untitled section
2. B                               1.1. B
```

Both TOCs are obviously not equivalent because each of these represents a
different structure. Therefore, only one of these can truly represent the
fragment's structure, the other one does not. So which of these is invalid?

<!-- ####################################################################### -->
## Definitions

```
Example:
========
<body>
  <h1>A</h1>
  B
</body>
```

**Heading X introduces section X**

Assume that any heading element can be identified by the heading's inner nodes
(or some other unique characteristic - e.g. the heading's `id`).

Heading `A` is said to introduce section `A`.

The intention behind this definition is to identify a section by the heading
element that introduced it. Note that each heading element always introduces a
single section (i.e. never more than one).

A reference of the form "section `A`" therefore refers to the section introduced
by the corresponding heading element.

**Node X (is located inside | belongs to | is associated with) section Y**

Node `B` is said to be located inside section `A` because there is nothing that
introduces a new section in between heading `A` and node `B`. There is also
nothing that indicates that section `A` ends before node `B` is reached.

Node `B` is also said to belong to, or to be associated with, section `A`.

Note that this definition is based upon the direct relationship between a node
and its section (i.e. no subsections in between).

**Section X (contains | is associated with) node Y**

Section `A` contains, or is associated with, node `B`
because node `B` is located inside of it.

**Parent container X of section Y**

Except for the body element, any node within a document always has a parent
element. In addition to that, this parent element is always a container element
(because it contains nodes as its child nodes).

The parent container of the section introduced by the body element is the body
element itself. Likewise, if element X introduces section Y as an inner section,
then element X is said to be the section's parent container element.

The parent container of a section introduced by a heading element is the parent
element of that heading. Likewise, if element X introduces section Y as a
subsequent section (i.e. not inside of it), then the parent element of element
X is said to be the section's parent container element.

A section's parent container is said to contain its section as an inner section.

Note that the element that introduced a section and the section's parent
container element are not always identical (i.e. can be different elements).

Note that this definition does not state that all inner section of such a
container's also have to end inside of the container (i.e. a section might
contain nodes that are located outside of its parent container ...).

**Section X (is located inside | belongs to | is associated with) container Y**

A section is said to be located inside of its parent container.

In addition to that, a section can also be said to be belong to, or to be
associated with, its parent container element.

Note that a section's belongs-to-node (outwards) and contains-node (inwards)
associations have different direction!

<!-- ####################################################################### -->
## Relationship between sections and nodes

From a node's perspective: Any node within a document always belongs to some
section, regardless if that section has a title or not. In addition to that, no
node can have a direct relationship with (i.e. is associated with) two different
sections at the same time. As a result, any node either directly belongs to some
section, or it belongs to a different one.

Note that multiple nodes may still belong to the same section.

From a section's perspective: Any section always directly contains no node at
all, a single node or more than one (in theory even infinitely many) nodes.

Note that a section, that does not directly contain any nodes, does not have to
be empty (i.e. a section that only contains subsections is not empty - e.g. the
content of a body element may consist of subsections only - see below).

The direct relationship between sections and nodes can therefore be classified
as **a two-way, one-to-many (i.e. 1:N) relationship**.

<!-- ####################################################################### -->
## Level of heading elements

The definition that a heading element introduces a new section merely states
that a document can be broken up into different sections.

Without any further definition, all sections would have to be considered equal
and there would have been no reason to define 6 different heading elements.

HTML-4 therefore also states that each heading element has a level value
associated with it (`h1` is most important, `h6` is least important). As a
consequence, all heading elements can be ordered with regards to this level
value:

```
=> h1 > h2 > h3 > h4 > h5 > h6 - (order of importance)
=> [h1, h2, h3, h4, h5, h6]    - (ordered sequence)
```

The definition of an order for the set of heading elements has no meaning, if
there is no statement that defines the semantics associated with that order,
because that oder does not define what the semantics are, if ...

* a subsequent heading is just as (i.e. equally) important.
* a less important heading follows a more important one.
* a more important heading follows a less important one.

Unfortunately, HTML-4 contains no such explicit definition.

<!-- ####################################################################### -->
## HTML-4 example fragment

HTML-4 states that "Visual browsers usually render more important headings in
larger fonts than less important ones.", which does not define any semantics,
because a font size is merely a visual indication.

Although example fragments should not be understood to express any definition
(they should only be used to clarify existing ones), the example of the HTML-4
specification that follows the above statement is quite revealing:

```
Example:
========
<div id="X" class="section">
  <h1>A</h1>
  B
  <div id="Y" class="subsection">
    <h2>C</h2>
    D
  </div>
  E
</div>
```

(This fragment is a modified version of that example -
i.e. modified to emphasize the example's relevant parts):

Note that HTML-4 defines `div` elements to "offer a generic mechanism for adding
structure to documents". The word "structure" in this context means that `div`
elements allow to group nodes without introducing new sections. If that were not
true, then authors would have no means to group nodes at block level without
changing a document's outline at the same time.

From the above fragment, the following statements can be derived:

<!-- ======================================================================= -->
### (1) Section C begins inside container Y

Section `C` exists because it is introduced by heading `C`, not by container `Y`.
As a result, container `Y` can not be associated with section `C` because that
section does not exist at the time container `Y` is entered.

The very first node that could possibly be associated with section `C` is heading
`C`. (Note that it has yet to be determined if associating a heading element with
the section it introduces would even make any sense ...)

What if container `Y` would have to be associated with section `C`?

This would mean that container `Y` would gain the characteristic to introduce a
new section because that section would begin before heading `C`. At the same
time, heading `C` would loose that characteristic because it is not intended to
introduce yet another section. The semantics of these elements would therefore
depend on the context in which these elements are used (i.e. the semantics would
have to change under certain conditions).

As a result, an implementation would therefore always have to first determine the
context of these elements in order to select the appropriate action (i.e. begin
a new section or not). To achieve this, an implementation would have to look ahead
in order to determine the actual semantics (i.e. if a `div` container begins, then
read ahead until the first heading element, or the end of the container is reached).

In theory, that could even be impossible to implement because HTML allows to
place any number of unessential nodes (i.e. nodes that do not affect the current
context in any way) in between the beginning of a `div` container and the first
heading element.

Conclusion: **A node can not be associated with a section that still has to be
introduced by some subsequent element.**

<!-- ======================================================================= -->
### (2) Node D is located inside section C

There is nothing that introduces a new section in between heading `C` and node
`D`. If that were the case, node `D` would have to be associated with that new
section instead.

There is also nothing that indicates that section `C` ends before node `D`. If
that were the case, node `D` would have to be associated with some other
pre-existing section (e.g. section `A`).

As a consequence, node `D` is located inside section `C` and must be associated
with that section.

<!-- ======================================================================= -->
### (3) Section C ends with container Y

```
<div id="X" class="section">
  <h1>A</h1>
  B
  <div id="Y" class="subsection">
    <h2>C</h2>
    D
  </div>
  E
</div>
```

It should be obvious, that the intention behind surrounding node `D` with
container `Y` is to state that section `C` ends with said container.

Still, could node `E` in theory also be associated with section `C`?

???????????????????????????

The answer to the initial question therefore is:
No, node `E` must not be associated with section `C`, because ...

**Conclusion**: No section can reach past its parent container.

Note that this conclusion is a mere generalization of: Any section ends with the
body element. That is not because there is nothing that follows the body element,
but because the body element is the topmost ancestor container of any node within
a document.

**Conclusion**: Any section has a parent container.

This conclusion is a mere observation, because any node has a parent container.
Depending on ones point of view, the only exception to that rule is the body
element itself.

**(4) Node E belongs to section A**

asdf

### A definition based upon a choice

### Continue...

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

There is nothing that indicates that the heading's section ends before the
implicit section that precedes it. Anything between the heading element's start
and end tag defines the section's title. A heading element itself does not define
where its section ends. Better, but still not good enough.

The situation starts to improve as soon as one takes a closer look at the example
of the [HTML-4 fragment](https://www.w3.org/TR/html401/struct/global.html#h-7.5.5):

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

The important questions here are if E-5's structure adds new characteristics to
`div` container elements or not:

* Can `div` elements end a section?

The answer here must be a decisive "No!", because any section must end with its
parent container element. This characteristic is independent of which kind of
container element it is surrounded.
