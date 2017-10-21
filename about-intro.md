
* [HTML-4, 7.5.5 Headings](https://www.w3.org/TR/html401/struct/global.html#h-7.5.5)

## Introduction

In HTML-4, each heading element is defined to introduce
(i.e. mark the beginning of) a new section.

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

Note - Upper case letters represent passive content
(i.e. nodes have no effect on an outline).

The the consensus to print the table of contents (TOC) for this fragment is:

```
TOC:
====
1. A
```

Even a slight modification of the above fragment reveals, that this TOC can
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

Obviously, node `A` must belong to some section, because that node can not
be ignored. As a result, **heading elements are not the only elements that
introduce new sections**. The simplified TOC therefore ignores the section
that is introduced by the body element.

There are two approaches of how to print a more accurate TOC for the
modified fragment:

```
TOC-1:                          TOC-2:
======                          ======
1. Untitled section             1. Untitled section
2. B                               1.1. B
```

Both TOCs are obviously not semantically equivalent because each of these
corresponds with a different structure. Consequently, only one of these
can accurately represent the fragment's outline, the other one does not.
So which of these is invalid?
