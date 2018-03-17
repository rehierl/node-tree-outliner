
<!-- ======================================================================= -->
# Design - section hierarchy

**CLARIFICATION**
The default definitions allow to define any section hierarchy.

Note that the "height" of a section hierarchy, if drawn onto a flat surface,
can initially be understood as the section tree's vertical size (aka. outline
height). In addition to that, the "width" of a section hierarchy can loosely be
understood to refer to the tree's overall horizontal size (e.g. the largest
number of sections on any outline level). Therefore, any section hierarchy can
be defined, if both dimensions are unrestricted. Which is, because any section
can be understood to represent its very own section hierarchy.

* A section hierarchy of any height/depth can be defined.

By default, no sectioning node has the characteristic to close a presequent
section. Because of that, a subsequent section always is a subsection to all
open presequent sections. Consequently, the default definitions allow to
arbitrarily increase the height of any section hierarchy.

* A section hierarchy of any width can be defined.

By default, any section ends with its parent container (i.e. its default scope).
Because of that, a subsequent section, whose sectioning node is entered after
the parent container of a presequent section was exited, is independent of
such a presequent section. Consequently, the default definitions allow to
arbitrarily increase the width of any section hierarchy.

<!-- ======================================================================= -->
## type-1 sectioning nodes

```
|---------------- x-axis (width)
|
|               n0
| ==============================
| n1            n5            n9
| -----------   -----------
|    n2    n4      n6 n7
|    -----            -----
|       n3               n8
|
y-axis (height)
```

* nodes `n0-9` are type-1 sectioning nodes
* nodes `n0-9` declare sections `s0-9`

In the above fragment, sectioning node `n1` is associated with section `s0` and
represents the parent container of section `s1`. Because of that, `s1` is a
subsection (i.e. child section) to `s0`. Consequently, any type-1 sectioning
node that is a descendant to another type-1 sectioning node will increase the
height/depth of the section hierarchy.

In addition to that, sectioning node `n5` is the next sibling of `n1`. Section
`s5` is therefore independent to `s1` and all of its subsections. Because of
that, `s5` is a subsection to the parent section of `s1` (i.e. a sibling
section to `s1`). Consequently, any type-1 sectioning node that is independent
to another type-1 section has the potential to increase the width of the overall
section hierarchy.

Because similar statements can be made with regards to all other nodes in the
above fragment, processing it will result in the following section hierarchy:

```
|------- x-axis (height)
|
|  s0 -|- s1 -|- s2 - s3
|      |      |- s4
|      |
|      |- s5 -|- s6
|      |      |- s7 - s8
|      |
|      |- s9
|
y-axis (width)
```

Note that the larger the last index on the x-axis, the higher the section
hierarchy is. This dimension obviously corresponds with the node level/height
(aka. outline height/depth) of a section.

Note that the larger the last index on the y-axis, the wider the section
hierarchy is (There currently is no formal definition that corresponds
with this dimension).

```
s0 -|- s1 -|- s2 - s3
    |      |- s4
    |
    |- s6
    |- s7 - s8
    |
    |- s9
```

Note that the section hierarchy remains essentially the same, if sectioning node
`n5` is replaced by an inactive container node. That is, because `n5` will still
be associated with `s0`. And, because of that, `s6` and `s7` will still be
descendant sections to `s0`.

Note that the inactive container node `n5` does not act as the parent container
of any section. That is, because each type-1 section has its own parent
container (i.e its sectioning node).

**CLARIFICATION**
The definition of type-1 sectioning nodes allows to define a section hierarchy
of any width and height.

<!-- ======================================================================= -->
## type-2 sectioning nodes

Type-2 sections are different from type-1 sections because a type-2 sectioning
node does not act as the parent container of the section it declares. That is,
a type-2 section depends upon an additional node that is presequent to its
sectioning node.

Note that any type-2 sectioning node will always have at least one type-1
sectioning node as its (not necessarily direct) ancestor. That is, because
the root node will always be treated as a type-1 sectioning node, regardless
of the root's specific definition.

```
            n0
==========================
n1 n2 n3 n4 n5 n6 n7 n8 n9
```

* `n0` declares the next outer type-1 section `s0`
* nodes `n1-9` are child nodes to `n0`
* nodes `n1-9` represent type-2 sectioning nodes
* nodes `n1-9` declare sections `s1-9`

Because no sectioning node is defined to close an open presequent section,
and because no section in the above fragment ends before another subsequent
sectioning node is entered, `s1` is a subsection to `s0`, `s2` is a subsection
to `s1`, ..., and finally, `s9` is a subsection to `s8`. Consequently, the
tree of sections that has `s0` as its root section contains a single rtl-path
of sections (i.e. a rooted path that ends in a leaf - "rtl" for "root-to-leaf"):
`(s0,s1,s2,s3,s4,s5,s6,s7,s8,s9)`.

Processing the above fragment will therefore
result in the following section hierarchy:

```
s0 - s1 - s2 - s3 - s4 - s5 - s6 - s7 - s8 - s9
```

Consequently, the default definition of type-2 sectioning nodes alone does not
allow to increase the width of a section hierarchy. That is, these definitions
are on their own insufficient to define any section hierarchy.

Note that, because no section is closed before a subsequent sectioning node
is entered, the next subsequent section will always be a subsection to all
open presequent sections. The height of the section hierarchy therefore
increases with each subsequent type-2 sectioning node.

Note that, `n0` could also be an inactive container node, instead of a type-1
sectioning node. In such a case section `s0` would have to represent the open
presequent section that was used to associate `n0`. Consequently, all rtl-paths
would then have a common prefix of sections (i.e. absolute vs. relative path)
that ends in `s0`.

<!-- ======================================================================= -->
## type-2: parent containers

Because the definition of type-2 sectioning nodes alone is insufficient to
increase the width of a section hierarchy, means to explicitly mark the end
of an open presequent section, or multiples thereof, are required.

**Example 1**

```
            n0
==========================
n1 n2 n3 n4 n5
            --------------
               n6 n7 n8 n9
```

If `n5` is replaced by an inactive container node that holds all nodes which
are subsequent to it (i.e. `n5` is no longer a sectioning node), then that
node will still be associated with `s4`. Consequently, and due to implicit
associations, all nodes descendant to `n5` (i.e. `n6-9`) are automatically
loosely associated with `s4`. And, because of that, sections `s6-9` remain
to be subsections of `s4`.

As a result, the tree of sections will still contain a single rtl-path:
`(s0,s1,s2,s3,s4,s6,s7,s8,s9)` (`s5` does not exist because `n5` is no
longer a sectioning node).

**Example 2**

```
            n0
==========================
n1             n6 n7 n8 n9
--------------
   n2 n3 n4 n5
```

However, if `n1` is replaced by an inactive container node instead, then all
aspects mentioned above apply to its inner nodes and sections (i.e. `n2-5`
and `s2-5`). But, as `n1` now acts as the parent container of sections `s2-5`,
they all end with it. Consequently, those inner sections can no longer have
any effect on any other subsequent section. That is, `s6-9` no longer are
subsections to `s2-5` and, as such, independent to those sections.

As a result, the tree of sections now contains two rtl-paths:
`(s0,s2,s3,s4,s5)` and `(s0,s6,s7,s8,s9)` (`s1` does not exist
because `n1` is no longer a sectioning node).

Processing this fragment will therefore
result in the following section hierarchy:

```
s0 -|- s2 - s3 - s4 - s5
    |- s6 - s7 - s8 - s9
```

**Example 3**

```
              n0
==============================
n1            n5            n9
-----------   -----------
   n2    n4      n6 n7
   -----            -----
      n3               n8
```

* `n1,n2,n5,n7` are inactive container nodes
* `n3,n4,n6,n8,n9` are type-2 sectioning nodes

Note that the injection of explicit inactive container nodes (aka. parent
containers) allows to increase the width of a section hierarchy. Because
of that, type-2 sectioning nodes, in combination with parent containers,
can be used to define any section hierarchy.

As a result, the tree of sections now contains four rtl-paths:
`(s0,s3)`, `(s0,s4)`, `(s0,s6,s8)` and `(s0,s9)`.

Processing this fragment will therefore
result in the following section hierarchy:

```
s0 -|- s3
    |- s4
    |- s6 - s8
    |- s9
```

<!-- ======================================================================= -->
## type-2: derived statements

**CLARIFICATION**
Presequent sections need to be altered in order to change the relationship
of a subsequent section. That is, the actual subsequent section and its
default scope remains essentially unchanged.

In order to move a subsequent section upwards in the section hierarchy (i.e.
increased width), the default scopes of one or more open presequent sections
need to be restricted. That is, those sections need to be closed before the
subsequent section will be entered.

In order to move a subsequent section downwards in the section hierarchy
(i.e. increased height/depth), a subsequent section must be located within
the scope of all of its presequent ancestor sections. That is, the scope of
all presequent ancestor sections must be widened in order to include the
"new" subsequent descendant section.

**CLARIFICATION**
The definition of type-2 sectioning nodes, in combination with parent
containers, allows to define a section hierarchy of any width and height.
