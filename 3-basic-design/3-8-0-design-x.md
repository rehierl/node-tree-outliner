
<!-- ####################################################################### -->
<!-- ======================================================================= -->
# Design (9) - type-2 sections

**QUESTION**
Would it be reasonable to allow a subsequent sectioning node to close an open
presequent type-2 section before the end of its default scope is reached?

Note that the following considerations are solely based upon type-2 sectioning
nodes. That is, they do not cover the question whether a type-1 sectioning node
could be allowed to end a type-2 section, nor if a type-2 sectioning could be
allowed to end a type-1 section. The focus of these considerations is whether
a type-2 sectioning node could be allowed to end a presequent type-2 section.

<!-- ======================================================================= -->
## introduction

```
            n0
========================== -> s0
n1 n2 n3 n4 n5 n6 n7 n8 n9
```

* `s0` represents the next outer section (e.g. the universal section)
* all nodes (i.e. `n1-9`) are siblings to each other
* nodes `n1-8` are type-2 sectioning nodes (declare sections `s1-8`)

Note that the default definition of sectioning nodes does not define the
characteristic to close an open presequent section.

In both cases, `n5` needs to be understood to be defined in such a way that it
closes section `s1` before the content nodes of `s5` are entered. That is, `s5`
is defined to be independent of `s1`. Put differently, no content node of `s1`
can be a content node of `s5` (and vice versa). Because of that, none of these
sections can be an ancestor section of the other. Consequently, both sections
are sibling sections with regards to the next outer section `s0`.

Note that if `n1` is itself defined to close the last outer open presequent
section, then section `s0`  represents the last presequent section that remains
to be open. That is, the following considerations need to be understood to be
independent of this outer aspect.

<!-- ======================================================================= -->
## fundamental considerations

> A subsequent type-2 Node `n5` must be a child node of `n1`.

If `n5` is some other descendant of `n1` (i.e. not a child node), then the
parent container of `s5` will be associated with `s1`. That is, because it
will be associated before `n5` is entered and thus before `s1` can even be
closed.

Consequently, all content nodes of `s5` would be implicitly associated with
`s1`: Section `s5` would be a subsection of `s1` by structural relationship.
Because of that, and in order to avoid conflicting statements with regards
to these implicit associations, `n5` could not be allowed to close `s1`.

If that condition is not met, then an implementation can not support these
kind of modified definitions. Under these circumstances, these definitions
must be ignored. Consequently, the use of such definitions is limited.

<!-- ======================================================================= -->

default definitions are rank-less

difference between type-1 and -2 sections
