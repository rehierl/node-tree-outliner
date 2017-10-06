
# HTML-4 heading elements

* [HTML-4, 7.5.5 Headings](https://www.w3.org/TR/html401/struct/global.html#h-7.5.5)

<!-- ####################################################################### -->
## Introduction

In HTML-4, each heading element is defined to introduce (i.e. mark the beginning
of) a new section.

Note that there seems to exist no explicit definition which states when an
introduced section ends. The only statement that can be made right away is that,
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

Even a slight modification of the above fragment reveals that the above TOC is
merely a commonly accepted simplification:

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
only elements that introduce new sections.** Note that the above TOC ignores
the section introduced by the body element.

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
## Definitions

**Active/Passive nodes**

A node that has no effect on the outline of a document is said to be passive
with regards to the process of creating an outline for that document.

An active node introduces a new section, ends an existing one, or has both of
these characteristics. Processing an active node will therefore have an effect
on the outline of a document.

Note that, like any heading element, the body element always is an active node
because, in general, any section ends with the body element. Also, any document
always has at least one section that ends with the document's body element.

**Active/Passive content**

A group of nodes that consists of only passive nodes, is said to represent
passive content. Processing all of these nodes will not change the document's
outline in any way.

A group of nodes that contains at least one active node, is said to represent
active content. Processing all nodes of active content will eventually change
the document's outline.

**Heading X introduces section X**

Assume that any heading element can be identified by the heading's inner nodes,
or some other unique characteristic (e.g. the heading's `id`).

```
Example:
========
<body>
  <h1>A</h1>
  B
</body>
```

(In this document, upper case letters inside HTML fragments always represent
passive content.)

Heading `A` is therefore said to introduce section `A`.

The intention behind this definition is to identify a section by the heading
element that introduced it. Note that each heading element always introduces a
single section (i.e. never more than one).

A reference of the form "section `A`" therefore refers to the section introduced
by the corresponding heading element.

**Heading X of section Y**

If a section `A` is introduced by heading element `A`, then that heading element
is also said to be the heading of that section.

**Node X (is located inside | belongs to | is associated with) section Y**

Node `B` is said to be located inside section `A` because there is nothing that
introduces a new section in between heading `A` and node `B`. There is also
nothing that indicates that section `A` ends before node `B` is reached.

If a node is located inside a section, then it is also said to belong to, or to
be associated with, that section. In such a case, the node and its section are
both said to have a direct relationship.

Note that this definition is based upon the direct relationship between a node
and its section (i.e. no subsections in between).

**Section X (contains | is associated with) node Y**

Section `A` contains node `B` because node `B` is located inside section `A`.

If a node is located inside a section, then that section is said to contain, or
to be associated with, that node.

Note the direct relationship between the node and its section.

**Parent container X of section Y**

Except for the body element, any node within a document always has a parent
element. A node's parent element is said to be the node's parent container
element because it contains the node as one of its inner child nodes.

A heading element is the parent container of all its inner child nodes. The inner
nodes of a heading element define the heading for the section that the heading
element introduces.

The parent container of a section introduced by a heading element is the parent
element of that heading. In general, the parent element of element `X` is said
to be the parent container of section `Y` if element `X` introduces section `Y`
as a subsequent section (i.e. not inside of it).

The parent container of the section introduced by the body element is the body
element. In general, element `X` is said to be the parent container of section
`Y` if element `X` introduces section `Y` as an inner section.

A container element is said to contain section as an inner section if that
container element is the section`s parent container.

Note that the element which introduced a section and the section's parent
container element are not necessarily identical (i.e. these can be different
elements).

Note that, as this definition is based upon an element's characteristic to
introduce a new section, it is independent of where exactly a section ends. The
only statement that can be made is that a section always begins inside its
parent container.

**Section X (is located inside | belongs to | is associated with) container Y**

A section is said to be located inside of its parent container.

In addition to that, a section can also be said to be belong to, or to be
associated with its parent container element.

Note that a section's belongs-to-node (outwards) and contains-node (inwards)
associations have different direction!

<!-- ####################################################################### -->
## Relationship between sections and nodes

From a node's perspective: Any node within a document always belongs to some
section, regardless if that section has a title or not. In addition to that, no
node can have a direct relationship with two different sections at the same time.
Any node therefore either directly belongs to some section, or it belongs to a
different one. (Multiple nodes may still belong to the same section.)

From a section's perspective: Any section always directly contains no node at
all, a single node or more than one, in theory even infinitely many, nodes.

Note that a section, that does not directly contain any nodes, does not have to
be empty (i.e. a section that only contains subsections is not empty - e.g. the
content of a body element consist of subsections only).

The direct relationship between sections and nodes can therefore be classified
as **a two-way, one-to-many (1:N) relationship**.

<!-- ####################################################################### -->
## Level of heading elements

The definition that a heading element introduces a new section implies that a
document can be broken apart into different sections. Without any further
definition, all sections would have to be considered equal and there would have
been no reason to define 6 different heading elements.

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

Unfortunately, HTML-4 does not explicitly define the intended semantics.

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
i.e. modified to emphasize the example's relevant parts -
Note that nodes A, B, C, D and E represent passive content)

Note that HTML-4 defines `div` elements to "offer a generic mechanism for adding
structure to documents". The word "structure" in this context means that `div`
containers allow to group nodes without introducing new sections (i.e. they allow
to group nodes without changing a document's outline at the same time). As such,
`div` containers are, by definition, passive nodes.

**(1) Section C begins inside container Y**

Section `C` exists because it is introduced by heading `C`, not by container `Y`.
As a result, section `C` begins inside container `Y`, not with it.

**(2) Container Y belongs to section A**

Consequently, container `Y` can not be associated with section `C` because that
section does not exist when container `Y` is being entered.

**TODO** - when exited

The very first node that could possibly be associated with section `C` is
heading element `C`. (Note that it has yet to be determined if associating a
heading element with the section it introduces would even make any sense ...)

**(3) Section C ends inside container Y**

It should be obvious, that the intention behind wrapping up heading `C` inside
container `Y`, is to express that section `C` ends inside container `Y` (i.e.
no node past that container can be associated with section `C`).

This intention is most obvious by the values of the `class` attributes assigned
to the `div` containers (i.e. `section` and `subsection`).

**(4) Node D belongs to section C**

There is nothing that introduces a new section in between heading `C` and node
`D`. If that were the case, node `D` would have to be associated with that new
section instead.

There is also nothing that indicates that section `C` ends before node `D`. If
that were the case, node `D` would have to be associated with some other section
introduced before section `C` (e.g. section `A`).

Therefore, node `D` belongs to section `C`.

**(5) Section C ends with container Y**

Observations (3) and (4) together allow to state that section `C` not just ends
somewhere inside container `Y`. As there is no more node following node `D`,
that still belongs to container `Y`, section `C` also ends with said container.

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
