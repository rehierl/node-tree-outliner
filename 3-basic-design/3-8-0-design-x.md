
<!-- ======================================================================= -->
# Design (9) - type-2 sections

**QUESTION**
Would it be reasonable to allow a subsequent type-2 sectioning node to close an 
open presequent type-2 section before the end of its default scope is reached?

Note that the following considerations are solely based upon type-2 sectioning
nodes. That is, they do not cover the question whether a type-1 sectioning node
should be allowed to end a type-2 section, nor if an inner type-2 sectioning
node should be allowed to end a type-1 section.

<!-- ======================================================================= -->
## introduction

```
            n0
========================== -> s0
n1 n2 n3 n4 n5 n6 n7 n8 n9
```

* `n0` declares the next outer type-1 section `s0`
* all nodes (i.e. `n1-9`) are siblings to each other
* all other descendant nodes will be ignored
* nodes `n1-9` all represent type-2 sectioning nodes
* nodes `n1-9` declare sections `s1-9`
* obviously, `s9` will always be empty

Note that the default definition of sectioning nodes does not define the
characteristic to close any open presequent section. Because of that, `s1`
is a subsection to `s0`, `s2` a subsection to `s1`, ..., and finally, `s9`
a subsection to `s8`. Consequently, the tree of sections that has its root
in `s0` contains a single rtl-path (i.e. a rooted path that ends in a leaf,
i.e. "rtl" for "root-to-leaf") of sections: `(s0,s1,s2,s3,s4,s5,s6,s7,s8,s9)`.

Obviously, the default definition of type-2 sectioning nodes alone is
insufficient to manually define a proper section hierarchy. In order to
support any tree of sections, means to mark the end of an open presequent
section, or multiples thereof, are required.

<!-- ======================================================================= -->
## parent containers

```
            n0
==========================
n1 n2 n3 n4 n5
            --------------
               n6 n7 n8 n9
```

If `n5` is turned into an inactive container node to hold the nodes that are
subsequent to it (i.e. no longer a sectioning node), then that node still has
to be associated with `s4`. Consequently, and due to implicit associations, 
all nodes descendant to `n5` (i.e. `n6-9`) are automatically loosely associated
with `s4`. And, because of that, sections `s6-9` still are subsections to `s4`.

Note that the tree of sections still contains a single rtl-path:
`(s0,s1,s2,s3,s4,s6,s7,s8,s9)` (`s5` does not exist because `n5` no
longer is a sectioning node).

```
            n0
==========================
n1             n6 n7 n8 n9
--------------
   n2 n3 n4 n5
```

However, if `n1` is turned into an inactive container node instead, then all
aspects mentioned above apply to the corresponding inner nodes and sections
(i.e. `n2-5` and `s2-5`). But, as `n1` now acts as the parent container of
sections `s2-5`, they all end with it. Consequently, those inner sections
can no longer have any effect on any other subsequent sectioning node (i.e.
`n6-9`). Because of that, `s6-9` no longer are subsections to `s2-5` and,
as such, independent of those sections.

Note that the tree of sections now contains two rtl-paths:
`(s0,s2,s3,s4,s5)` and `(s0,s6,s7,s8,s9)` (`s1` does not exist
because `n1` is no longer a sectioning node).

```
           n0
===========================
n1                 n7
-----------------  --------
   n2 n3       n6     n8 n9
      --------
         n4 n5
```

* inactive container nodes: `n1, n3, n7`
* type-2 sectioning nodes: `n2, n4, n5, n6, n8, n9`

Consequently, inactive container nodes (aka. parent containers) can be used to
manually define any tree of sections. However, this method does not strictly
answer the initial question. That is, because the default scopes of the above
sections are reduced by placing explicit parent containers. Because of that,
any section in the above tree still ends with its default scope.

Note that the tree of sections now contains three rtl-paths:
`(s0,s2,s4,s5)`, `(s0,s2,s6)` and `(s0,s8,s9)` (there are only
three leaf sections: `s5`, `s6` and `s9`).

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Basically, the default definitions (type-2 sectioning nodes, parent containers
and implicit associations) already provide the means to manually define any
hierarchy of sections.

That is, because the parent containers not just define when sections have
to end, but, due to their associations, also to which sections all of their
inner nodes and sections belong. Which is, because all formal associations
of a parent container carry over to all of its contents.

**CLARIFICATION**
In order to shift a subsequent section upwards in the section hierarchy, the
default scopes of one or more open presequent sections need to be reduced.
That is, they need to be closed before the subsequent section will be entered.

Note that the targeted actual section (and its default scope) remains unchanged.
In short: Presequent sections are changed in order to edit a subsequent section.

<!-- ======================================================================= -->

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
