
<!-- ======================================================================= -->
# Design (8) - type-2 sections

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
* nodes `n1-9` are siblings to each other
* other descendant nodes will be ignored
* nodes `n1-9` represent type-2 sectioning nodes
* nodes `n1-9` declare sections `s1-9`
* obviously, section `s9` will always be empty

Note that any type-2 sectioning node will have at least one type-1 sectioning
node as its (not necessarily immediate/direct) ancestor. That is, because the
root node always acts as a type-1 sectioning node.

Note that the default definition of sectioning nodes does not define the
characteristic to close any open presequent section. Because of that, `s1` is
a subsection to `s0`, `s2` is a subsection to `s1`, ..., and finally, `s9` is
a subsection to `s8`. Consequently, the tree of sections that has `s0` as its
root section contains a single rtl-path of sections (i.e. a rooted path that
ends in a leaf - "rtl" for "root-to-leaf"): `(s0,s1,s2,s3,s4,s5,s6,s7,s8,s9)`.

Obviously, the default definition of type-2 sectioning nodes alone is not
sufficient to manually define a proper section hierarchy. That is, because
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
subsequent to it (i.e. no longer a sectioning node), then that node will still
be associated with `s4`. Consequently, and due to implicit associations, all
nodes descendant to `n5` (i.e. `n6-9`) are automatically loosely associated
with `s4`. And, because of that, sections `s6-9` still are subsections to `s4`.

As a result, the tree of sections still contains a single rtl-path:
`(s0,s1,s2,s3,s4,s6,s7,s8,s9)` (`s5` does not exist because `n5` is
no longer a sectioning node).

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

As a result, the tree of sections now contains two rtl-paths:
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

Consequently, inactive container nodes (aka. parent containers) can be used to
manually alter the default scopes of the involved sections and therefore allow
to define any tree of sections.

As a result, the tree of sections now contains three rtl-paths:
`(s0,s2,s4,s5)`, `(s0,s2,s6)` and `(s0,s8,s9)` (there are only
three leaf sections: `s5`, `s6` and `s9`).

Note that, `n0` could also be an inactive container node, instead of a type-1
sectioning node. In such a case `s0` would then represent the section that was
used to associate `n0`. Consequently, all rtl-paths would then have a common
prefix of sections (i.e. absolute vs. relative paths/sequences).

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Presequent sections need to be altered in order to change the relationship of
a subsequent section. That is, the actual subsequent section and its default
scope remains essentially unchanged.

In order to shift a subsequent section upwards in the section hierarchy, the
default scopes of one or more open presequent sections need to be restricted.
That is, they need to be closed before the subsequent section will be entered.

In order to shift a subsequent section downwards in the section hierarchy, a
subsequent section must be located within the scope of all of its presequent
ancestor sections. That is, the scope of all presequent ancestor sections must
be widened in order to include the "new" subsequent descendant section.

**CLARIFICATION**
The default definitions (type-2 sectioning nodes, parent containers and
implicit associations) provide the means to manually define any hierarchy
of sections.

That is, because the parent containers not only define when sections end, but
also, due to implicit associations, to which sections all of their inner nodes
and sections belong. Which is, because all formal associations of a parent
container carry over to all of its contents.

**CLARIFICATION**
The injection of explicit parent containers does however not answer the initial
question. That is, because only the default scope of an affected section is
changed. As a result, any section in the above fragments still ends with its
default scope and not any sooner.

Note that the focus of the initial question is on the latter aspect. That is,
to close a presequent section before the end of its default scope is reached.

<!-- ======================================================================= -->
## implicit parent containers

As mentioned before, a section's parent container isn't a parent container
because the definition of the corresponding node has certain characteristics.

Any parent node is a parent container, if a section was declared inside of it.
If that would not be the case, then consistent dynamic support (see the
requirements) could not be guaranteed. In short: Any parent node can become
a section's parent container, regardless of its specific definition.

Because of that, such parent containers exist whether they are manually
injected (explicit), or due to some structural requirement (implicit).

Recall that the node level of a node is defined as "1 + the number of edges in
between the node and the tree's root". That is, the root node has a node level
of 1, its child nodes a node level of 2, and their children a node level of 3.
In short: The higher the node level, the deeper within the hierarchy a node is
located.

**case 1: (node level 1 >> node level 2)**

```
      n0
 ------------
 n1        n2
----
 n3
```

* `n1` is an inactive container node
* `n2, n3` are type-2 sectioning nodes

If a presequent sectioning node `n3` has a higher node level than the next
subsequent sectioning node `n2`, then the default scope of `s3` ends before
`n2` is entered. That is, `s3` and `s2` are, by structural relationship,
independent from each other. Consequently, `n2` can not have any effect on
`s3`. That is, `s2` can not be a subsection to `s3` and `n2` can not close
`s3` (as it is already closed when `n2` is being entered).

Note that, from the perspective of this design, this case is a non-issue. That
is, because sections will be ignored as soon as they are closed. Because of
that, any such modified definition (with regards to `n2`) is not understood to
be with regards to `n3/s3`, but with regards to some other open presequent
section. Consequently, modified definitions may yield unexpected results, if
the above structural dependency is not correctly taken into account.

However, certain conditions may still yield a seemingly identical result. If
that is the case, the reasons for those matching results differ none the less.

**case 2: (node level 1 << node level 2)**

```
      n0
 ------------
 n1        n2
          ----
           n3
```

* `n2` is an inactive container node
* `n1, n3` are type-2 sectioning nodes

If, in contrary to that, the next subsequent sectioning node `n3` has a higher
node level than a presequent sectioning node `n1`, then `n3` has an ancestor
that is a top-level node of `s1`. Consequently, `s3` is by structural
relationship a subsection to `s1`. Because of that, and in order to avoid
conflicting statements, any attempt to close `s1` when `n3` is being entered,
must be ignored. That is, `s3` can not be independent of `s1` (e.g. a sibling
section to it).

**case 3: (node level 1 == node level 2)**

```
      n0
 ------------
 n1        n3
----      ----
 n2        n4
```

* `n1, n3` are inactive container nodes
* `n2, n4` are type-2 sectioning nodes

Note that this case can be understood to contain two subsequent subtrees that
have `n1` and `n3` as their root nodes. Because of that, this case is similar
to case 1: `s2` will be closed before `n4` is entered.

Note that the node levels of the corresponding sectioning nodes may even differ
for as long as both nodes are located within two different subtrees. The effect
will still be covered by case 1: `s2` will be closed before `n4` is entered.

**case 4: (same parent container)**

```
      n0
 ------------
 n1        n2
```

* `n1, n2` are type-2 sectioning nodes

However, `n2` is in principle free to close the open presequent section `s1`,
if (and only if) both type-2 sectioning nodes have the same parent node (i.e.
the same parent container).

Note that the parent section of `s2` can then only be one of the remaining open
sections, which all are presequent to `s1` (i.e. ancestor sections of `s1`).

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
In order for modified definitions to not yield any conflict or an unexpected
result, the corresponding type-2 sectioning nodes must have the same parent
container.

Note that the above considerations have precedence over any modified definition.
That is, those definitions must be ignored, if they are in conflict with the
corresponding structural considerations. Hence, the use of such definitions is
always limited.

Note that this can be understood as an indication that, in principle, the
default definitions always have precedence over any modified definition. That
is, those definitions must not be in conflict with the default definitions.

```
            n0
==========================
n1 n2 n3 n4 n5 n6 n7 n8 n9
```

<!-- ======================================================================= -->

**TODO**
extended rather than modified definitions -
just a naming related aspect

**TODO**
default definitions are rank-less

**TODO**
difference between type-1 and -2 sections -
type-1 is always rank-less?
