
# HTML-4 heading elements

* [HTML-4, 7.5.5 Headings](https://www.w3.org/TR/html401/struct/global.html#h-7.5.5)

<!-- ####################################################################### -->
## Introduction

In HTML-4, each heading element is defined to introduce (i.e. mark the beginning
of) a new section.

Note - There does not seem to exist an explicit definition which states when a
section ends. The only statement that can be made right away is that,
**by default, any section ends with the body element.**

```
Example:
========
<body>
  <h1>A</h1>
  B
</body>
```

Note - Upper case letters represent passive content;
i.e. these nodes have no effect on a document's outline.

The the consensus to print the table of contents (TOC) for this fragment is:

```
TOC:
====
1. A
```

Even a slight modification of the above fragment reveals that the above TOC can
only represent a commonly accepted simplification:

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
only elements that introduce new sections.** The above TOC therefore ignores
the section that is introduced by the body element.

There are two possible ways to print a TOC for the modified fragment:

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
## Relationship between sections and nodes

*From a node's perspective:*
Any node within a document belongs to some section, regardless if that section
has a title or not. In addition to that, no node can have a direct relationship
with two different sections at the same time. Any node therefore either directly
belongs to some section, or it belongs to a different one. (Multiple nodes may
still belong to the same section.)

*From a section's perspective:*
Any section directly contains no node at all, a single node or more than one, in
theory even infinitely many, nodes.

Note - A section, that does not directly contain any nodes, does not have to be
empty (i.e. a section that only contains subsections is not empty - e.g. the
content of a body element consist of subsections only).

The direct relationship between sections and nodes can therefore be classified
as **a two-way, one-to-many (1:N) relationship**.

```
Example:
========
<body>
  A
  <h1>B</h1>
  C
</body>
```

Node `A` is said to belong to the section introduced by the body element, i.e.
**the body section**.

Node `C` is said to belong to section `B` because the last section introduced
before node `C` is reached is section `B`. There is also no indication that
section `B` ends before node `C` is reached. If that were the case, node `C`
would have to be associated with the body section.

**TODO**
It has yet to be determined if associating a heading element and its inner nodes
(e.g. `h1` and `B`) with the section that the heading element introduces would
even make any sense at all.

<!-- ####################################################################### -->
## Level of heading elements

That any heading element introduces a new section implies that a document can be
broken up into multiple different sections. Without any further definition, all
sections would have to be considered equal and there would have been no reason
to define 6 different heading elements.

HTML-4 therefore also states that each heading element has a level value
associated with it (`h1` is most important, `h6` is least important). As a
consequence, all heading elements can be ordered with regards to their
importance:

```
=> h1 > h2 > h3 > h4 > h5 > h6 - (order of importance)
=> [h1, h2, h3, h4, h5, h6]    - (ordered sequence)
```

The definition of an order for the set of heading elements has no meaning
because this order by itself does not define what the semantics are, if ...

* a subsequent heading is just as (i.e. equally) important.
* a less important heading follows a more important one.
* a more important heading follows a less important one.

Unfortunately, HTML-4 does not explicitly define the semantics associated with
a heading's level value:

<!-- ####################################################################### -->
## HTML-4 example fragment

HTML-4 states that "Visual browsers usually render more important headings in
larger fonts than less important ones.". This does not define any semantics
because a font size merely provides a visual indication.

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
i.e. modified to emphasize the example's relevant parts)

Note - HTML-4 defines `div` elements to "offer a generic mechanism for adding
structure to documents". The word "structure" in this context means that `div`
containers allow to group nodes without introducing new sections (i.e. they allow
to group nodes without changing a document's outline at the same time). As such,
`div` containers are, by definition, passive nodes.

<!-- ======================================================================= -->
### Observations

From the above fragment, the following obersvations can be made:

**(1) Section C begins inside container Y**

Section `C` exists because it is introduced by heading `C`, not by container `Y`.
As a result, section `C` begins inside container `Y`, not with it.

**(2) Container Y belongs to section A**

Consequently, container `Y` must not be associated with section `C` because that
section does not exist when container `Y` is being entered.

**TODO** - when exited is even worse

The very first node that could possibly be associated with section `C` is
heading element `C`.

**(3) Section C ends inside container Y**

It should be obvious, that the intention behind wrapping up heading `C` inside
container `Y`, is to express that section `C` ends inside container `Y` (i.e.
no node past that container can be associated with section `C`).

Note that this intention is most obvious by the values of the `class` attributes
assigned to the `div` containers (i.e. "section" and "subsection").

**TODO** - Because of that, the question that needs to be answered is, if this
implicitly turns div containers from being passive nodes into active nodes ...

**(4) Node D belongs to section C**

There is nothing that introduces a new section in between heading `C` and node
`D`. If that were the case, node `D` would have to be associated with that new
section instead.

There is also nothing that indicates that section `C` ends before node `D`. If
that were the case, node `D` would have to be associated with some other section
introduced before section `C` (e.g. section `A`).

Therefore, node `D` belongs to section `C`.

**(5) Section C ends with container Y**

Observations (3) and (4) together allow to state that section `C` ends with
container `Y` because there is no node following node `D`.

**(6) Node E belongs to section A**

A direct consequence of observation (2) is that no node past container `C` can
be associated with section `C`. Consequently, node `E` must belong to a different
section.

In addition to that, there is no indication that a new section is introduced in
between container `Y` and node `E`. Node `E` must therefore belong to a section
that was introduced before section `C`.

The last section introduced before section `C` is section `A`. Note also that
there is no indication that section `A` ends before node `E` is reached.

Therefore, node `E` belongs to section `A`.

<!-- ####################################################################### -->
### Does section C have to end with container Y?

<!-- ####################################################################### -->
### Could container Y still be associated with section C?

Associating container `Y` with section `C` would mean that section `C` would have
to begin before it is even introduced by heading `C`. Doing so would therefore
mean that container `Y` would gain the characteristic to introduce a new section.
At the same time, heading `C` would loose that characteristic because it is not
intended to introduce yet another section.

The semantics of both of these elements would therefore have to depend on the
context in which they are used (i.e. under certain conditions, the semantics
would have to deviate from the definition of these elements).

As a result, an implementation would always have to first determine the context
of these elements in order to select the appropriate action (i.e. begin a new
section or not). To achieve this, an implementation would always have to do a
look-ahead (i.e. if a `div` container begins, then read ahead until the first
heading element, or until the end of the container is reached).

In theory, that could even be impossible to implement because HTML allows to
place any number of passive nodes in between the beginning of a `div` container
and the first heading element.

**Conclusion: A node can not be associated with a section that still has to be
introduced by some subsequent element.**

Note that redefining the `div` container element to always introduce a new
section would be ill advised, because authors would then have no means to group
elements at block level without changing a document's outline at the same time.

<!-- ####################################################################### -->
## A definition by choice?

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

Could node `E` still be associated with section `C`?

In general, any inactive container element `V` can be injected into a document
to wrap up subsequent child nodes of some parent container element `U` (without
changing the document's outline):

```
Example:                     (injected container)
========                     ====================
<U>                            <U>
  A <B> C </B> D        =>       <V> A <B> C </B> D </V>
</U>                           </U>
```

Such an injection is of course not allowed if container `V` would have to cross
the boundaries of some container `U` (i.e. `V` begins before and reaches into
`U`, or `V` begins inside and ends after `U`):

```
Example (inwards)    (tag layer)        (dom layer)
========             ===========        ===========
-: A                 A                  .
V: B                 <V> B              .
V: <U>        =>     <U>            or  .
V:  C                  C </V>           .
-:  D                  D                .
-: </U>              </U>               .

Example (outwards)   (tag layer)        (dom layer)
========             ===========        ===========
-: <U>               <U>                .
-:   A                 A                .
V:   B         =>      <V> B       or   .
-: </U>              </U>               .
V: C                 D </V>             .
-: D                 D                  .
-:                                      .
-:                                      .
```

On the abstraction layer of tags:

Injecting the start tag of container `V` before the first node and the container's
end tag after the last node would result in an invalid HTML document, because it
would violate HTML's fundamental rule that any inner element must end before its
outer container can.

On the abstraction layer of a DOM tree:

A new node will be created each time a start tag is reached. In addition to that,
and until the end tag of the initial node is reached, a new node will be added as
child node to the initial node each time the start tag of an inner node is reached.
This means that, from the DOM tree's perspective, the start tag of a node
determines where to place a node.



This means that if a
container (as a section's visual representative element) would be injected in
place of the first node associated with it, then all nodes of that section would
have to become child nodes of the injected container. Saving that tree as an HTML
document would therefore result in a document that has a different structure
(i.e. the source document and the saved document are not equivalent).

The answer to the initial question therefore is: No, node `E` must not be
associated with section `C`, because it would mean that the tree of sections
produced by the outline algorithm would be inconsistent with the document's
structure.

**Conclusion**: No section can reach past its parent container.

Note that this conclusion is a mere generalization of: Any section ends with the
body element. That is not because there is nothing that follows the body element,
but because the body element is the topmost ancestor container of any node within
a document.

**Conclusion**: Any section has a parent container.

This conclusion is a mere observation, because any node has a parent container.
Depending on ones point of view, the only exception to that rule is the body
element itself.

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
