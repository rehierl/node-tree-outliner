
<!-- ======================================================================= -->
# Introduction

In HTML-4, each heading element is defined to introduce
(i.e. mark the beginning of) a new section.

In general: The DOM tree represents a tree data structure defined in terms of
nodes and edges. HTML elements may therefore be referred to as "nodes of the
underlying tree", or simply as "nodes" rather than "elements".

Think in terms of trees and sequences.

<!-- ======================================================================= -->
## The NxN Relation

```
Example:
========
<body>
  A
</body>
```

Node `A` belongs to the body element and the body element contains node `A`.

### Nodes <-> Nodes

* `N` is the set of nodes, `p` and `c` in `N`.
* `(p,c) in R subset-of NxN` states that node `p` is in direct relationship
  with  node `c` (i.e. parent node `p` contains child node `c`).
* `(c,p) in R' subset-of NxN` states that node `c` is in direct relationship
  with node `p` (i.e. child node `c` belongs to parent container node `p`).
* `(p,c) in R <=> (c,p) in R'`

<!-- ======================================================================= -->
## The SxN Relation

```
Example:
========
<body>
  A
  <h1>B</h1>
  C
</body>
```

Node `C` belongs to section `B` and section `B` contains node `C`.

* The last section introduced before node `C` is reached, is section `B`.
  No other section is introduced in between heading `B` and node `C`.
* There is no indication that section `B` ends before node `C` is reached.
  If that would be the case, node `C` would have to belong to a different
  section instead (e.g. the body section).
* Section `B` is therefore the parent section of node `C`.

Node `A` belongs to the body section and the body section contains node `A`.

* Any node must always belongs to some section.
* Heading elements can not be the only nodes that introduce new sections.
* The body element must introduce a section (i.e. the **body section**).

**Question** -
Does a heading and its inner nodes (e.g. heading `h1` and node `B`) belong to
(1) the section that a heading introduces, or (2) to some other pre-declared
section?

**Question** -
Nodes introduce new sections, but where exactly do they end?

* The only statement that can be made right away is that,
  **by default, any section ends with the body element.**
* Can a section end before a new one is introduced?
* What is the scope of a section?

### Sections <-> Nodes

* `S` the set of sections, `(s in S)` and `(n in N)`.
* `(s,n) in R subset-of SxN` states that section `s` is in direct relationship
  with node `n` (i.e. section `s` contains node `n`).
* `(n,s) in R' subset-of NxS` states that node `n` is in direct relationship
  with section `s` (i.e. node `n` belongs to section `s`).
* `(s,n) in R <=> (n,s) in R'`

<!-- ======================================================================= -->
## The SxS Relation

```
Example:
========
<body>
  <h1>A</h1>
  B
</body>
```

The common consensus to display the table of contents (TOC) listing for this
fragment is:

```
TOC:
====
1. A
```

Even a slight modification of the above fragment however reveals, that this
listing can only represent some commonly accepted simplification:

```
Example:
========
<body>
  A
  <h1>B</h1>
  C
</body>
```

The section introduced by the body element is not exactly empty because node
`A` belongs to the body section. As a result, a TOC listing can actually not
ignore the body section.

From the perspective of HTML-4, there are two approaches to produce more
accurate TOC listings for this fragment:

```
TOC-1:                          TOC-2:
======                          ======
1. Untitled section             1. Untitled section
2. B                               1.1. B
```

Both TOCs are not equivalent, because each of these corresponds with a
different structure. Consequently, only one can accurately represent the
fragment's outline, the other one does not. So which of these is invalid?

Note that HTML-5 defines heading `B` to be reused to specify the heading of the
body section. However, the reuse of heading elements is misleading because it
ignores the placement of a reused heading (e.g. as a child of the body element
and after node `A`).

**Question** -
What kind of relationship do sections have with each other?

### Sections <-> Sections

**Question** -
Do relations `R` and `R'` exist such that ...

* `S` is the set of sections, `s1` and `s2` in `S`.
* Does `R` exist such that `(s1,s2) in R subset-of SxS` (?)
* Does `R'` exist such that `(s1,s2) in R <=> (s2,s1) in R'` (?)
