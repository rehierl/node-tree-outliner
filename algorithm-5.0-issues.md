
# Issues of HTML 5.0's outline algorithm

* A closer look at some of the "bigger" issues the outline algorithm has.
* Heading titles (e.g. A.1.1) refer to the corresponding step in the algorithm.
* Compare with [HTML 5.0 algorithm](./algorithm-5.0.md)

## Definitions

**DEF-1** - The first element of heading content in an element of sectioning
content represents the heading for that section.

**DEF-2** - Sectioning content elements are always considered subsections of their
nearest ancestor sectioning root, or their nearest ancestor element of sectioning
content, whichever is hearest, regardless of what implied sections other headings
may have created.

*conceptual problem* - DEF-2 associates an implicit characteristic to sectioning
content elements: They may even end preceeding outer sections.

## A.1.1 - No. 1

According to this step, entering a sectioning content element always ends the
current section (implied heading). In contrary to that, the first element of
heading content within a section is defined to represent a section's heading (DEF-1):

```
<body>
  A
  <section>
    <h1>B</h1>
  </section>
  C
  <h1>D</h1>
  E
</body>
```

The outlines according to the ...

```
(... algorithm (1))           (... definition (2))
1.   Untitled section         1.   heading:D
1.1.   heading:B              1.1.   heading:B
2.   heading:D
```

Unfortunately, outline (1) does not correspond with the specificiation because
`heading:D` is used to create an implied section, instead of using it as the
first section's heading.

This issue needs to be seen in combination with B.3, B.4 and DEF-2:

The `lastSection` of the outer outline, to which the sectioning element's inner
sections will be added (B.3), is closed (A.1.1, implied heading) when the
sectioning element is entered.

When the sectioning element is exited, `currentSection` will be set to reference
that closed outer section (B.3). This means that the algorithm will continue to
associate nodes with and add further subsections to it. But, at that time, it
already has an implied heading associated with it. This implied heading marks
that section as done.



Conceptual problem:

This definition implicitly defines that any implied section, which is a subsection
of one of the top-level sections of an outline, must end if a section element is
entered.

This issue actually indicates, that a sectioning content element
should not end any outer section. A sectioning content element needs to be
considered a subsection of the current section, not a subsection of the nearest
outer sectioning content or sectioning root element.

This is the actual reason
why 


. A sectioning content element
should not end any outer section, it should merely continue/extend such a section.

## A.1.1 - No. 2

"4.3.10 Headings and sections" states: Sectioning content elements are always
considered subsections of their nearest ancestor sectioning root or their
nearest ancestor element of sectioning content ...

## A.5

Sectioning content elements will always be associated with their first inner
section, sectioning root elements with the last active outer section (C.3).

As a result, the meaning of the `Node.parentSection` property depends on the
property`s parent node. A clear definition of this property is therefore not
possible.

In general, a `parent` property always refers to a superordinate entity, not a
subordinate one.
