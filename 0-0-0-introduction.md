
<!-- ======================================================================= -->
# Introduction

In HTML-4, each heading element is defined to introduce
(i.e. mark the beginning of) a new section.

In general:

The DOM tree is a tree data structure defined in terms of nodes and edges.
That is, HTML is bound by the rules of discrete mathematics (graph theory)!

Think in terms of graphs and tuples.

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
* `(p,c) in R in NxN` states that node `p` is in direct relationship with 
  node `c` (i.e. parent node `p` contains child node `c`).
* `(c,p) in R' in NxN` states that node `c` is in direct relationship with
  node `p` (i.e. child node `c` belongs to parent container node `p`).
* `(p,c) in R <=> (c,p) in R'`

<!-- ======================================================================= -->
## The NxS Relation

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

* The last section introduced before node `C` is section `B`. No other section
  is introduced before node `C`. If that would be the case, node `C` would have
  to belong to this section instead.
* There is no indication that section `B` ends before node `C`. If that would be
  the case, node `C` would have to belong to a different, pre-declared section
  instead (e.g. the body section).

Node `A` belongs to the body section and the body section contains node `A`.

* Any node always belongs to some pre-declared section.
* Heading elements are not the only elements that introduce new sections.
* The body element must introduce a section (i.e. the **body section**).

**Question** -
Does a heading element and its inner nodes (e.g. `h1` and `B`) belong to
(1) the section that it introduces, or (2) to some pre-existing section?

**Question** -
Elements introduce new sections, but where do they end?

* The only statement that can be made right away is that,
  **by default, any section ends with the body element.**
* Can a section end before a new one is introduced?
* What is the scope of a section?

### Nodes <-> Sections

* `S` the set of sections, `s in S` and `n in N`.
* `(n,s) in R in NxS` states that node `n` is in direct relationship with
  section `s` (i.e. node `n` belongs to section `s`).
* `(s,n) in R' in SxN` states that section `s` is in direct relationship with
  node `n` (i.e. section `s` contains node `n`).
* `(n,s) in R <=> (s,n) in R'`

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

The the consensus to display the table of contents (TOC) for this fragment is:

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

The section introduced by the body element is itself not empty (node `A` belongs
to the body section). As a result, a TOC can no longer ignore this section.

There are two approaches to print a more accurate TOC for this fragment:

```
TOC-1:                          TOC-2:
======                          ======
1. Untitled section             1. Untitled section
2. B                               1.1. B
```

Both TOCs are not equivalent because each of these corresponds with a different
structure. Consequently, only one can accurately represent the fragment's
outline, the other one does not. So which of these is invalid?

**Question**:
What kind of relationship do sections have with each other?

### Sections <-> Sections

**Question**:
Do relations `R` and `R'` exist such that ...

* `S` is the set of sections, `s1` and `s2` in `S`.
* Does `R` exist such that `(s1,s2) in R in SxS` (?)
* Does `R'` exist such that `(s1,s2) in R <=> (s2,s1) in R'` (?)
