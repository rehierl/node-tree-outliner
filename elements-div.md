
# The div element

* has no special meaning at all
* more appropriate elements must be used if available
* an element of last resort

```html
A
<div>
  B
</div>
C
```

A, B and C represent non-element nodes, element nodes or subtrees of such nodes.
They represent (even empty) subtrees that do not contain any sectioning element.
None of the nodes in those subtrees introduces a new section.

The outline of the above fragment is as follows:

```
Untitled section
```

The nodes in this fragment must be associated (with sections) as follows:

```
s0: A
s0: <div>
s0:   B
s0: </div>
s0: C
```

(!) A `div` element is no sectioning element,
    it must not and it can not be used to introduce a new section.

## What the specs state

### [HTML 3.2](https://www.w3.org/TR/REC-html32#div)

* used to structure documents as a hierarchy of divisions
* a block-like element
* `center` is directly equivalent to `<div algin="center">`

### [HTML 4.01](https://www.w3.org/TR/html401/struct/global.html#h-7.5.4)

* a generic mechanism for adding structure to documents
* defines content to be block-level
* imposes no other presentational idioms on the content
* may be used in conjunction with style sheets
* used to achieve the desired structural and presentational effects
* visual user agents generally place a line break before and after this element

*Notes*

* defined to allow adding structure
* not defined to introduce a new section

### [HTML 5.0](https://www.w3.org/TR/html5/grouping-content.html#the-div-element)

* has no special meaning at all
* represents its children
* can be used to mark up semantics common to a group of consecutive elements
* must be viewed as an element of last resort
* must use more appropriate elements if available
* can be used for stylistic purposes
* can be used to wrap multiple paragraphs within a section -
  to annotate them in a similar way - to set the language (lang attribute) of
  multiple paragraphs at once

### [HTML 5.1](https://www.w3.org/TR/html51/grouping-content.html#the-div-element)

* same as 5.0

### [HTML 5.2](https://www.w3.org/TR/html52/grouping-content.html#the-div-element)

* same as 5.1
