
<!-- ======================================================================= -->
# Design (9) - type-2 sections

**QUESTION**
Would it be reasonable to allow a subsequent type-2 sectioning node to close an 
open presequent type-2 section before the end of its default scope is reached?

Note that the following considerations focus on type-2 sectioning nodes only.
That is, they do not cover the question whether a type-1 sectioning node should
be allowed to close a type-2 section, nor if an inner type-2 sectioning node
should be allowed to close a type-1 section.

<!-- ======================================================================= -->
## introduction

```
            n0
==========================
n1 n2 n3 n4 n5 n6 n7 n8 n9
```

* `n0` declares the next outer type-1 section `s0`
* all nodes (i.e. `n1-9`) are siblings to each other
* all other descendant nodes will be ignored
* nodes `n1-9` all represent type-2 sectioning nodes
* nodes `n1-9` declare sections `s1-9`
* obviously, `s9` will always be empty

Note that any type-2 sectioning node will have at least one type-1 sectioning
node as its ancestor. That is, because the root node always acts as a type-1
sectioning node.

Note that the default definition of sectioning nodes does not define the
characteristic to close any open presequent section. Because of that, `s1` is
a subsection to `s0`, `s2` is a subsection to `s1`, ..., and finally, `s9` is
a subsection to `s8`. Consequently, the tree of sections that has `s0` as its
root section contains a single rtl-path of sections (i.e. a rooted path that
ends in a leaf - "rtl" for "root-to-leaf"): `(s0,s1,s2,s3,s4,s5,s6,s7,s8,s9)`.

Obviously, the default definition of type-2 sectioning nodes alone is
insufficient to manually define a proper section hierarchy. That is, because
no section is closed before a subsequent sectioning node is entered. As a
result, the next subsequent section will always be a subsection to all
presequent sections. Because of that, and in order to support any tree of
sections, means to explicitly mark the end of an open presequent section,
or multiples thereof, are required.

<!-- ======================================================================= -->
## explicit parent containers

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
as such, independent to those sections.

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

* `n1, n3, n7` are inactive container nodes
* `n2, n4, n5, n6, n8, n9` are type-2 sectioning nodes

Consequently, inactive container nodes (aka. parent containers)
can be used to manually define any tree of sections.

Note that the tree of sections now contains three rtl-paths:
`(s0,s2,s4,s5)`, `(s0,s2,s6)` and `(s0,s8,s9)` (there are only
three leaf sections: `s5`, `s6` and `s9`).

Note that, `n0` could also be some inactive common parent container, instead of
a type-1 sectioning node. In such a case `s0` would then have to represent the
section that `n0` is associated with. Consequently, all rtl-paths would have
some common prefix of sections (i.e. absolute vs. relative paths/sequences).

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The default definitions (type-2 sectioning nodes, parent containers and implicit
associations) provide the means to manually define any hierarchy of sections.

That is, because the parent containers not only define when sections have to
end, but also, due to implicit associations, to which sections all of their
inner nodes and sections belong. Which is, because all formal associations
of a parent container carry over to all of its contents.

**CLARIFICATION**
Presequent sections need to be altered in order to change the relationship of a
subsequent section. That is, the actual subsequent section and its default scope
remains unchanged.

In order to shift a subsequent section upwards in the section hierarchy, the
default scopes of one or more open presequent sections need to be reduced.
That is, they need to be closed before the subsequent section will be entered.

In order to shift a subsequent section downwards in the section hierarchy, a
subsequent section must be located within the scope of all of its presequent
ancestor sections. That is, the scope of all presequent ancestor sections must
be widened in order to include the subsequent descendant section.

<!-- ======================================================================= -->
## preliminary summary

The injection of explicit parent containers does not answer the initial
question. That is, because only the default scopes of the above sections are
changed. As a result, any section in the above node trees still ends with its
default scope and not any sooner. Note that the focus of the initial question
is on the latter aspect.



<!-- ======================================================================= -->

> A subsequent type-2 Node `n5` must be a child node of `n1`.

meaning - parent containers have precedence over any user-defined rank value -
that is, because they are presequent to this user-provided information

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
