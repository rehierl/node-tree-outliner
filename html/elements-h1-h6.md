
# Heading elements - What the specs state

<!-- ======================================================================= -->
## [HTML 3.2](https://www.w3.org/TR/REC-html32#headings)

* there are six levels of headers
* h1 is most important, h6 is least important
* used for document headings
* headings have a level associated with them which reflects the heading
  element's importance
* in general, more important headings are rendered in a larger font

*Notes*

* does not clarify what "document headings" means
* does define an order (importance, levels) of headings - `h1 > ... > h6`

<!-- ======================================================================= -->
## [HTML 4.01](https://www.w3.org/TR/html401/struct/global.html#h-7.5.5)

* briefly describes the topic of the section it introduces
* may be used to construct a table of contents for a document
* six levels of headings - h1 the most important, h6 the least important
* in general, more important headings are rendered in larger font

*Notes*

* a heading introduces a section
* does not state that the heading element itself is an element of that section
* can be read to state that the section begins just after its heading element
* does itself not state where the section of a heading ends

Use `div` elements to associate a heading with a section:

```html
<DIV class="section" id="forest-elephants" >
  <H1>Forest elephants</H1>
  <P>In this section, we discuss the lesser known forest elephants.
     ...this section continues...

  <DIV class="subsection" id="forest-habitat" >
    <H2>Habitat</H2>
    <P>Forest elephants do not live in trees but among them.
       ...this subsection continues...
  </DIV>
</DIV>
```

* shows how to use the `div` element to associate a heading with the document
  section that follows it
* allows to define a style (background, font, ...) for the section

*Notes*

* the above fragment can only mean that the section associated with a heading
  is supposed/intended to end with its surrounding `div` container
* the following question is still remains unanswered - where exactly does `h1`'s
  section end? - with the beginning of `h2`'s, or with the end of `h1`'s
  surrounding div container? - put differently, could one add additional content
  to `h1`'s section after `h2`'s section has ended? - that must be possible!
* note the "section" and "subsection" style sheet classes -
  these imply that there is a hierarchy of sections
* note that the heading elements, not the `div` elements, are defined to
  introduce a new section - this example does not change the definition of
  a `div` element
* "with the document section that follows it" - to which element does "it"
  refer? - "it" can only refer to the heading element - you would have to
  rephrase that sentence if "it" would refer to the `div` element - that
  section does not follow the div element, it is located inside of it

Note-1

* HTML does itself not cause section numbers to be generated from headings.

*Notes*

* implies that this is seen as a style sheet issue
* heading elements do not have a number associated with them
* they need to be generated from the document's structure

Note-2

* Some people consider skipping heading levels to be bad practice.

*Notes*

* the issue here is - the association of a subsection with a parent section
* the generation of section numbers is a mere result of that issue

<!-- ======================================================================= -->
## HTML 5.0

[HTML 5.0, heading content](https://www.w3.org/TR/html5/dom.html#heading-content-0)

* heading content defines the header of a section
* whether a section is explicitly marked up using sectioning content elements,
  or implied by the heading content itself

[HTML 5.0, heading elements](https://www.w3.org/TR/html5/sections.html#the-h1,-h2,-h3,-h4,-h5,-and-h6-elements)

* heading elements represent headings for their sections
* semantics and meaning defined in "headings and sections"
* have a rank - given by the number in their name - h1 has highest rank, h6 has
  lowest rank - two elements with the same name have equal rank
* must not be used to mark up subheadings, etc. - unless intended to be the
  heading for a new section or subsection - use markup patterns instead

*Notes*

* "for their sections" - have (or can be associated with) a section
* this definition does not state that a heading element introduces a new section
  (unfortunately, "headings and sections" still does - implied sections)

[HTML 5.0, sectioning content](https://www.w3.org/TR/html5/dom.html#sectioning-content-0)

* sectioning content is content that defines the scope of headings and footers
  `=> article, aside, nav, section`
* each element potentially has a heading *and* an outline
* see "headings and sections" for further details

[HTML 5.0, headings and sections](https://www.w3.org/TR/html5/sections.html#headings-and-sections)

* (1) the first element of heading content represents the heading for that section
* a heading's rank is used to determine where to put the implied section of a
  subsequent heading
* (2) subsequent headings of equal or higher rank start new implied sections
* (3) headings of lower rank start implied subsections that are part of the
  previous one
* subsequent headings represent the heading of their implied section
* certain elements are said to be *sectioning roots* - can have their own
  outlines, but do not contribute to the outlines of their ancestors
  (`=> blockquote, body, fieldset, figure, td`)
* sectioning content elements are always considered subsections of their nearest
  ancestor sectioning root or sectioning content
* explicitly wrap sections in elements of sectioning content -
  do not rely on the implicit sections generated by having multiple headings in
  one element of sectioning content

*Notes*

* subsequent headings of equal or higher rank start new implied *sections* -
  it does not state *sub-sections*! - i.e. a sibling to the explicit section
* (At first) the first heading represents the heading for that explicit section -
  regardless of the first heading's rank! - (Then) subsequent headings of equal
  or higher rank start new implied sections - here, the first heading's rank
  will be relevant, if the subsequent heading is the 2nd heading, etc. -
  that does not add up!
* (Then, outside view) sectioning content elements are subsections of their
  nearest ancestor sectioning element - essentially states to ignore any
  implied section

[HTML 5.0, creating an outline](https://www.w3.org/TR/html5/sections.html#outlines)

* outline, a list of one or more potentially nested sections
* a section is a container that corresponds to some nodes in the original tree
* each section can have a heading and further nested sub-sections
* sections in the outline don't necessarily correspond with `section`
  elements - they are merely conceptual sections.
* interactive table of contents should jump the user to the relevant sectioning
  content element
* outline depth - of a heading content element associated with a section is the
  number of sections that are ancestors of that section in the outermost outline
  that this section finds itself in plus 1 - the outline depth of a heading
  content element, not associated with a section, is 1

*Notes*

* an outline is a list of sections - i.e. not a single root section
* a section is a container of some nodes - more precisely and more importantly
  a container of consecutive nodes
* jump the user to the relevant section - issue if it begins with a non-element
  text node
* outline depth - why set the value of unassociated headings to 1 - and not 0?

[HTML 5.0, algorithm](https://www.w3.org/TR/html5/sections.html#outlines)

* see [HTML 5.0 algorithm](./algorithm-5.0.md)
