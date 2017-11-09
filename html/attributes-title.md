
# The title attribute

* offers advisory information about an element
* frequently displayed as tooltip
* user agents tend to not expose this attribute
* if an element has no title attribute, the title attribute of an ancestor
  element must be used - i.e. must overrides

## What the specs state

### [HTML 3.2, attr](https://www.w3.org/TR/REC-html32)

* has no section dedicated to the attribute itself
* defined alongside of multiple elements
* link element - an advisory title for the linked resource
* anchor element - an advisory title for the linked resource

### [HTML 4.01](https://www.w3.org/TR/html401/struct/global.html#h-7.4.3)

* offers advisory information about the element for which it is set
* may be used to annotate any number of elements
* an element must support this attribute
* frequently displayed as a "tool tip"
* also used for speech synthesis
* link element - designate an external style sheet

### [HTML 5.0](https://www.w3.org/TR/html5/dom.html#the-title-attribute)

* represents advisory information for an element
* such as would be appropriate for a tooltip
* on a link - the title, or a description of the target resource
* on an image - image credit, or a description of the image
* on a paragraph - a footnote or commentary on the text
* on a citation - further information about the source
* on interactive content - a label for, or instructions for use of the element
* relying on the title attribute is discouraged -
  many user agents do not expose this attribute
* if omitted, the title attribute of an ancestor is what counts -
  overrides the title attribute of an ancestor -
  i.e. must be overridden (e.g. empty string)
* line break characters (i.e. 0xA, LF) can be used for line breaks -
  (issue - unintended line break if a title gets too long -
  escaping, i.e. "\n", seems unsupported)
* some elements (link, abbr, input) define additional semantics -
  in case of these elements, the title attribute of any ancestor is ignored

### [HTML 5.1](https://www.w3.org/TR/html51/dom.html#the-title-attribute)

* same as 5.0

### [HTML 5.2](https://www.w3.org/TR/html52/dom.html#the-title-attribute)

* same as 5.1
