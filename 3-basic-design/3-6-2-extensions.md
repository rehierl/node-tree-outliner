
<!-- ======================================================================= -->
# Design - extending the default definitions

The focus of the following considerations is not to define new types of nodes,
but to investigate those options which allow to deviate from the default
definitions. Hence, the first step is to take a look at those aspects which
can be altered. These options, if any, then allow to extend the definition of
sectioning nodes by certain modifiers.

Note that such modifiers are intended to alter the definition of sectioning
nodes while being consistent with their default definitions. That is, it must
be possible to transform any tree, which is defined based upon those extended
definitions, into a tree that is solely based upon default definitions (and
vice versa, i.e. extended description equivalent-to strict/default description).

<!-- ======================================================================= -->
## available options

> options when entering a sectioning node

When a sectioning node is being entered, an algorithm has in principle knowledge
of all those nodes that it has already visited. Because of that, it knows about
all those sections that are presequent to the current sectioning node (i.e. the
closed and the open presequent sections). In contrary to that, an algorithm is
unaware of any subsequent node. Those might, or might not exist (i.e. there is
no guarantee that there are subsequent nodes/sections).

As the closed presequent sections were closed even before the current subsequent
sectioning node was entered, the declared subsequent section is by default
independent to these sections. Hence, and with regards to closed sections, all
that modifiers could do would be to define the subsequent section to be a
subsection to them. But, as the `subsection-of` relationship is formally based
upon multiple associations per node, any attempt to define a subsequent section
to be a subsection to closed presequent sections would represent an attempt to
alter closed sections and consequently be in conflict with the definition a
section's "closed" state.

Note that, because of the current path of open sections, an algorithm is by
default even unaware of all closed presequent sections.

What remains therefore are the open presequent sections. But, because any
subsequent section is by default a subsection to all open presequent sections,
all that a modifier could do would be to close these sections and thus define
the subsequent section to be independent to them. As such, the option to close
open presequent sections allows to select a different parent section for section
declared by the current sectioning node.

Note however that, as mentioned before, open sections can not be closed
arbitrarily. That is, because any ancestor section must remain open for as long
as any of its subsections are open (i.e. close in an orderly/bottom-up fashion).

Note that any other available option, besides closing presequent sections,
is not relevant for the current considerations. That is, with regards to
the definition of modifiers which define other section properties which are
not relevant to the section hierarchy (e.g. a title).

Note this option (i.e. close open sections) could also be used for the
definition of end-marker nodes (e.g. `<close />`, defined to close type-2
sections). That is, if the corresponding modifiers would be defined to close
the relevant sections before the end-marker node itself is associated. And,
because of that, such a node would then belong to the parent section of the
most significant section which needs to be closed.

Note that the same reasoning, with regards to closed presequent and all
subsequent sections, also applies to the other two cases mentioned below.
That is, these may also only close those sections that are presequent to
the corresponding exit event.

> options when exiting a type-1 sectioning node

Closing those sections that are presequent to the exit event of a type-1
sectioning node is technically possible.

Note however, that a type-1 sectioning node also represents the parent container
of the section it declares. That is, none of those sections that are declared
inside of a type-1 sectioning node are allowed to reach past such a sectioning
node. Consequently, those inner sections always have to be closed first,
regardless of any modifier. And, because of that, such a modifier can only
affect those open sections that are presequent to the type-1 sectioning node's
enter event.

However, and in contrary to the above case, the corresponding sectioning node,
and all of its inner content nodes are already associated. That is, such a
modifier can no longer change the association of the sectioning node (i.e.
associate with a different parent section) or the association of its inner
content nodes. Consequently, such a modifier can only affect subsequent nodes
and sections.

This option could therefore only be used to mark the end of a branch of the
section hierarchy (i.e. end-marker nodes). However, such nodes would then be
associated with the current section. As such, and if more than one sections
would have to be closed, it could be difficult to detect why ancestor sections
were closed. That is, because that node would then be "located" inside of an
inner section and thus might not necessarily be accessible to its ancestor
sections (i.e. a reason as to why not to associate end-marker nodes with the
sections they close).

Note that this option has the same problematic as parent containers (i.e.
presequent nodes must be edited in order to change the relationship of
subsequent sections). Consequently, and depending on the specific notation
of such modifiers, authors could have difficulties to notice the reasons
behind the relationship between two subsequent sections.

> options when exiting a type-2 sectioning node

Closing those sections that are presequent to the exit event
of a type-2 sectioning node is not an option.

That is, because it would result in conflicting statements with regards to the
logical location of such a sectioning node and the section's content nodes.
Essentially, the sectioning node, which is associated while it is being entered,
would then belong to a section that is independent to sections with which the
content nodes of the declared section will be associated.

Note that type-2 sectioning nodes are defined not to have any inner sectioning
nodes themselves. Consequently, such an option could, by definition, only close
those sections that are presequent to the sectioning node's enter event.

<!-- ======================================================================= -->
## benefits of close modifiers

The most relevant option available is to close sections while a subsequent
sectioning node is being entered.

Note that the above considerations related to this option ...

* apply to type-1 and type-2 sectioning nodes alike. Yes, a type-1 sectioning
  node may technically close open presequent type-1 or type-2 sections.
* do not take into account, if it could even be allowed to close presequent
  sections in a given context. This option merely states that, from a technical
  perspective, it would be possible.

As stated before, a subsequent sectioning node must be within the scope of a
presequent section, if the declared section is supposed to become one of its
subsections. Likewise, if the declared section is not supposed to become a
subsection, then the scope of the presequent section must end before the
subsequent sectioning node can be entered.

Consequently, and in order to change the relationship of a subsequent section,
the scope of one or more presequent sections must be altered. Because of that,
users always need to be aware that the definition of a section's relationship
depends on presequent nodes. As such, the default definitions lack clarity when
defining a section hierarchy. That is, because the information which defines a
section's parent section is not strictly bound to the corresponding sectioning
node.

In principle, close modifiers allow to close one or more sections when a
subsequent sectioning node is entered. Because of that, they provide the means
to bind the definition of a section's relationship to its sectioning node. As
such, they allow to explicitly define the relationship of a declared section
and can therefore be used to define a more obvious section hierarchy.

<!-- ======================================================================= -->
## conclusion

Modifiers/extensions are based upon closing sections. Hence, each modifier can
be loosely understood to instruct the outline algorithm to close one or more
sections. And because they bind the definition of a section's relationship to
its sectioning node, they can be used to clearly express the section hierarchy.

That is, (1) such modifiers are possible, and (2) they improve the overall
design by making it more convenient to express a specific section hierarchy.
Because of that, extending the default definitions with close modifiers is
in general reasonable.

Note however, that the above considerations did not take into account, whether
a section can be closed in a given context. As it turns out (see below),
sections can not be closed arbitrarily. The usefulness of such modifiers
therefore has its limits.

<!-- ======================================================================= -->
## HTML's current approach

The two biggest issues with HTML's current approach are (1) sections can be
closed inside of an associated container, and (2) sections may contain nodes
that are siblings to their ancestor nodes.

```
HTML-4:        common practice:         table of contents:
=======        ================         ==================
<h1>A</h1>     <section> <h1>A</h1>     1. A
B              B                        2. D
<div>          <div>
  C              C </section>
  <h1>D</h1>     <section> <h1>D</h1>
  E              E
</div>         </div>
F              F </section>
```

Note that in HTML-5, the first element of heading content (e.g. `<h1>`) inside
of `<section>` elements is reused to define the section's heading. That is,
the first such element does not represent a type-2 sectioning node. (It would
be more appropriate to redefine the `<title>` element).

Note that the rank of a heading content element is essentially a close modifier.
As such, rank values instruct an outline algorithm to close sections. Because
of that, rank values are a mere matter of convenience.

Note that both issues are sufficient to render any attempt to add dynamic
support into a fruitless effort. That is, because the resulting node tree,
after executing the necessary transformations, is not guaranteed to accurately
represent the tree's initial contents (i.e. the `<div>` container would
basically break apart).


```
HTML-4:        this approach:           table of contents:
=======        ====================     ==================
<h1>A</h1>     <section> <h1>A</h1>     1. A
B              B                        1.1. D
<div>          <div>
  C              C
  <h1>D</h1>     <section> <h1>D</h1>
  E              E </section>
</div>         </div>
F              F </section>
```

From the perspective of this approach, issue (1) is due to implicit
associations, and issue (2) due to the concept of parent containers,
a non-issue.

Note that, in contrary to HTML's common practice, the container's inner section
is a subsection to the presequent outer section (i.e. not a sibling section).

Note that the default definitions have no rank (i.e. rank-less definitions).

<!-- ======================================================================= -->
## implicit associations

```
   n0
========
 n1  n2
----
 n3
```

* `n0` is an inactive parent node (associated with `s0`)
* `n1` is a sectioning node (type-1 or type-2, declares `s1`)
* `n2, n3` are inactive nodes

If, for example, the definition of `n1` would be altered in such a way that
entering `n1` would result in closing section `s0` (but no other ancestor
section in addition to that), then `s1` would be, by the definition of `n1`,
a sibling section to `s0`. That is, no content node of `s1` is a content node
of `s0`. However, because `n0` is still associated with `s0`, any content node
of `s1` still remains to be (by implicit association) a content node of `s0`.

The conflicting statements therefore are:
(1) `s1` is not a subsection of `s0` (modified definition of `n1`), and
(2) `s1` is a subsection of `s0` (structural relationship via `n0:s0`).

In order to avoid such conflicts, any instruction to close `s0` must be ignored
because `s1` is by structural relationship a subsection of `s0`. Under these
kind of circumstances, `n1` can therefore not be allowed to close `s0`.

Note that these structural dependencies can not be undefined. Because of that,
structural relationships override any modification. That is, those dependencies
always have precedence over any close modifier.

Note that these considerations are independent of where (inside of a node tree)
such a subtree can be found. Such a subtree will always result in the afore
mentioned conflict.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Sections can not be closed arbitrarily.

**CLARIFICATION**
Section `s1`, which is declared by some sectioning node `n1`, is a forced
(or structural) subsection of `s0` (i.e. regardless of any close modifier),
if `n1` is a descendant of a node that is associated with `s0`.

Note that this statement applies whether sectioning node `n1` ...

* is a type-1, or a type-2 sectioning node.
* is associated with the section it declares (i.e. `s1`) or not.

Note HTML's definition of sectioning content elements (an error).

**CLARIFICATION**
The default definitions of sectioning nodes are consistent with implicit
associations. Therefore, implicit associations have no effect (i.e. are
dormant) for as long as no changes or additions are made to the default
definitions. That is, implicit associations will only surface in combination
with close modifiers.

Note that, by default, any section still ends with its default scope. That is,
because no sectioning node is defined to close a presequent section. Because of
that, the above implicit associations can not trigger these kind of conflicts.

<!-- ======================================================================= -->
## parent containers

Any parent node is a parent container, if it is a type-1 sectioning node, or
if it has type-2 sectioning nodes as child nodes. That is, because sections
must not be allowed to reach past their parent containers. Consistent dynamic
support could otherwise not be guaranteed.

Any parent node can therefore become a section's parent container, regardless
of its specific definition. Because of that, such parent containers exist
whether they are manually injected (explicit), or due to structural conditions
(implicit).

Note that a node can be defined to never be a section's parent container, if
(and only if) the node is not allowed to have type-2 sectioning nodes as child
nodes (e.g. the type-2 sectioning nodes themselves). However, an implementation
is in general unaware of these kind of additional definitions. That is, in
case of input errors or redefinitions, such an implementation will still treat
descendant sectioning nodes as actual sectioning nodes and the corresponding
nodes as parent containers. Because of that, reusing sectioning nodes for
purposes other than to declare new sections must be avoided.

**case 1: (node level 1 >> node level 2)**

```
      n0
 ------------
 n1        n2
----
 n3
```

* `n1` is an inactive parent node
* `n2, n3` are type-2 sectioning nodes

If a presequent sectioning node `n3` has a higher node level than the next
subsequent sectioning node `n2`, then the default scope of `s3` ends before
`n2` is entered. That is, `s3` and `s2` are, by structural relationship,
independent from each other. Consequently, `n2` can not have any effect on
`s3`. That is, `s2` can not be a subsection to `s3` and `n2` can no longer
close `s3` (as it is already closed when `n2` is being entered).

Note that, from the perspective of an algorithm, this case is a non-issue.
That is, because sections will be ignored by subsequent operations as soon
as they are closed. Because of that, any modifier (`n2`) is *not* understood
to be with regards to `n3/s3`, but with regards to some other open presequent
section. Consequently, modifiers may yield unexpected results, if this
structural aspect is not taken into account.

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

* `n2` is an inactive parent node
* `n1, n3` are type-2 sectioning nodes

If, in contrary to that, the next subsequent sectioning node `n3` has a higher
node level than a presequent sectioning node `n1`, then `n3` has an ancestor
that is a top-level node of `s1`. Consequently, `s3` is by implicit association
a subsection to `s1`. Because of that, and in order to avoid conflicting
statements, any instruction to close `s1` when `n3` is being entered, must be
ignored. That is, `s3` can not be independent of `s1` (e.g. a sibling section
to it).

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

Note that this case can be understood to contain two independent subtrees that
have `n1` and `n3` as their root nodes. Because of that, this case is similar
to case 1: `s2` will be closed before `n4` is even entered.

Note that the node levels of the corresponding sectioning nodes don't have
to be equal for as long as both nodes are located within two different subtrees.
The effect will still be covered by case 1: `s2` will be closed before `n4` is
entered.

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

Note that the parent section of `s2` can only be one of the remaining open
sections, which all are ancestor sections of `s1`.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Parent containers have significant impact on the use of close modifiers.

Note that the above considerations have precedence over any extended definition.
That is, such non-default definitions must be ignored, if they are in conflict
with structural dependencies. Hence, the use of such definitions is limited.

Note that this can be understood as an indication that, in principle, the
default definitions have precedence over any non-default definition. That
is, such modifications must not be in conflict with the default definitions.

**CLARIFICATION**
In order for non-default definitions to not yield any conflict, or an
unexpected result, type-2 sectioning nodes must have the same parent container.

**Mind hook**
The placement of sectioning nodes is significant.
