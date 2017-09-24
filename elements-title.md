
# The title element

* when displayed, stripped of any inner markup - child text content
* is not considered part of the flow of text
* required exactly once per document -
  defines the document's title or name
* must be context-rich - must stand alone when used out of context

## What the specs state

### [HTML 3.2](https://www.w3.org/TR/REC-html32#title)

* is always needed (exactly once - required) in a document's `head`
* provides an advisory title, to be displayed in a window's caption, etc.
* content model is PCDATA - markup is not permitted in its content (PCDATA)

### [HTML 3.2, dtd](https://www.w3.org/TR/REC-html32#dtd)

* is not considered part of the flow of text
* should be displayed (e.g.) as the page header or window title

### [HTML 4.01](https://www.w3.org/TR/html401/struct/global.html#h-7.4.2)

* is not considered part of the flow of text
* should be displayed (e.g.) as the page header
* required exactly once per document in the `head` section
* used to identify the contents of a document
* should be a context-rich title -
  e.g. "Introduction to ... " instead of "Introduction"
* may contain character entities, but no markup

### [HTML 5.0](https://www.w3.org/TR/html5/document-metadata.html#the-title-element)

* represents the document's title or name
* should be descriptive, even if used out of context
* often different from its first heading -
  which does not have to stand alone when taken out of context
* there must be no more than one element per document
* content equals concatenated text nodes - ignoring any non-text child nodes

### [HTML 5.1](https://www.w3.org/TR/html51/document-metadata.html#the-title-element)

* same as 5.0
* should be used when referring to a document in a user interface

### [HTML 5.2](https://www.w3.org/TR/html52/document-metadata.html#the-title-element)

* same as 5.1
* definition of [child text content](https://www.w3.org/TR/html52/infrastructure.html#child-text-content)
