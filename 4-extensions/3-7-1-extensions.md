
<!-- ======================================================================= -->
# Design - extending the default definitions

The focus of the following considerations is to evaluate options which allow to
extend the default definitions by defining additional nodes and/or attributes.
The definition of these nodes and attributes will be referred to as "extended
definitions", or simply as "extensions (to the default definitions)".

> extended description => default description

The first step is to take a look at those aspects which can be altered while
maintaining consistency with the default definitions. That is, because it
must be possible to transform the description of a tree, which uses extended
definitions, into a semantically equivalent description, which does not use
any such definition. In short, for each extended description, there must
exist an equivalent default description.

As such, the definition of extensions is not intended to add new features to
the default definitions. Those extensions will be a mere matter of convenience.

<!-- ======================================================================= -->
## available options

Obviously, extensions can only have an effect on an algorithm's current
context. In addition to that, and because the creation of new sections is
already covered by the definition of sectioning nodes, such extensions can
only instruct an implementation to close presequent sections.

Note that already closed presequent sections are no longer relevant. That is,
because sections can not be reopened, and because of that, no further nodes
and/or subsections can be associated with sections that are already closed.
Likewise, subsequent nodes and sections are not relevant. Which is, because
those are not even guaranteed to exist. Consequently, extensions can only
represent instructions to close presequent sections.

Note that such attributes, which instruct an implementation to close sections,
will be referred to as "(close) modifiers". In addition to that, any node can
be understood to always have a default (close) modifier associated with it
(e.g. `<div close="0">`). Consequently, the term "close modifier" will be
used rather than the terms "extended definition" or "extensions".

> overview of available options

```
              | an (inactive/sectioning) node's |
              | enter event   | exit event      |
--------------------------------------------------
when entering | (1/1)         | (0/0)           |
when exiting  | (0/0)         | (1/0)           |
```

* `1` - this case represents a viable option
* `0` - this case is ill advised or triggers a conflict
* `1/0` - this case represents a viable option with regards to inactive
  nodes (`1`), but not with regards to sectioning nodes (`0`).

> case 1 - when entering a node's enter event - (1)

Obviously, presequent sections can be closed before the corresponding node
is itself associated. Because of that, the current node (and its descendants)
will belong to the parent section of the most significant section of those
sections which are going to be closed.

This option could therefore be used in order to define end-marker nodes
(e.g. `<close />`). Note that the effect of such a definition would be to:
(1) first close the current section, and then (2) associate the node (and
potentially also its descendants) with the current section's parent section.

> case 2 - when entering a sectioning node's enter event - (1)

Closing a presequent section before associating the sectioning node that is
being entered, is a viable option. That is, because it will not result in
conflicting statements with regards to the logical location of a section:
(1) the sectioning node will be associated with one of the current section's
ancestor sections, and (2) the section's content nodes will be associated with
the declared section, which will then be a subsection to the sectioning node's
parent section. That is, the declared section will be strongly connected with
its sectioning node.

> case 3 - when exiting a node's enter event - (0)

This case means that the node is associated before presequent sections will be
closed. Because of that, this case will result in conflicting statements: (1)
the node's descendants do not belong to the closed sections, and (2) the node's
descendants, due to the implicit associations that result from the association
of the current node, belong to the closed section.

> case 4 - when exiting a sectioning node's enter event - (0)

In addition to the issue mentioned in case 3, this case will also result in
conflicting statements with regards to the logical location of a section.
Regardless of what type of section is declared, the conflicting statements then
are: (1) the section is, due to the association of the sectioning node, located
inside of the to-be-closed sections, and (2) the section is, because of the
association of its content nodes (after closing those sections), not located
inside of those sections. That is, the declared section is not a subsection of
the section with which its sectioning node is associated. And, because of that,
the declared section is not strongly connected with its sectioning node.

Note that, with regards to type-1 sectioning nodes, the presequent sections
obviously need to be closed before the sectioning node's section is opened.
Otherwise, that section would have to be closed first, as it will become the
new current section once it is opened.

> case 5 - when entering a node's exit event - (0)

As mentioned before, any node is a parent container, if the corresponding node 
has type-2 sectioning nodes as its child nodes. Because of that, those sections
which are declared by child type-2 sectioning nodes must always be closed first.
That is, whether a close modifier is associated with the current node or not.
And, because of that, case 5 is not applicable.

> case 6 - when entering a sectioning node's exit event - (0)

As before, case 6 is not applicable because inner sections must
always be closed first, regardless of any potential close modifier.

Note that a type-1 sectioning node is by definition the parent container
of the section it declares. That is, if it is not allowed to close a type-1
section before the end of its default scope is reached, then this node event
will always have to close at least the declared type-1 section.

Note that a type-2 sectioning node never acts as the parent container of the
section it declares. In addition to that, a type-2 sectioning node is defined
to not contain any sectioning node as one of its descendant nodes. Consequently,
a type-2 sectioning node will never act as the parent container of any section.

> case 7 - when exiting a node's exit event - (1)

Due to case 5, and by the time a node's exit event will be exited, all inner
sections can be considered to be closed already. Consequently, the application
of a close modifier according to this case can only be with regards to sections
that are still open by the time the corresponding node was entered.

In addition to that, all descendants of that node have already been associated.
Consequently, the close modifier of such a node can also no longer change these
associations. However, such a modifier can still change the relationship of
those nodes and sections that are subsequent to the node's exit event.

This option could therefore only be used to mark the end of a branch of the
section tree (i.e. end-marker nodes). As such, the effect of such a definition
would be to: (1) first associate the node (and its descendants) with the current
section, and then (2) close one or more presequent sections.

Because of that, and if more than one section would have to be closed, it
could turn out to be difficult to detect why sections had to be closed. That
is, because such a node would then be "located" deep inside of an inner section
and will therefore not necessarily be accessible to its ancestor sections (i.e.
a reason as to why not to associate end-marker nodes with the sections they
close).

> case 8.1 - when exiting a type-1 sectioning node's exit event - (0)

Because all nodes have already been associated, closing those sections that
are presequent to the type-1 sectioning node's enter event (while the node
is being exited) *can not result* in conflicting statements with regards to
the location of the declared section.

However, this option has the same problematic as parent containers (i.e.
presequent nodes must be edited in order to change the relationship of
subsequent sections). That is, the relationship of a subsequent section
with other sections depends on a node that is presequent to the subsequent
section's sectioning node. Consequently, and depending on the specific
notation of such modifiers, authors could have difficulties to understand
the reasons behind the relationship between two sections. As such, this
case is, although technically possible, ill advised.

> case 8.2 - when exiting a type-2 sectioning node's exit event - (0)

Because the content nodes of a type-2 section have not been associated yet
(i.e. in contrary to the sectioning node itself and its descendant nodes),
closing those sections that are presequent to the type-2 sectioning node's
enter event (while the node is being exited) *will result* in conflicting
statements with regards to the location of the declared section: (1) the
sectioning node and its descendants belong to the closed section, and (2)
the declared section's content nodes do not belong to the closed sections.

<!-- ======================================================================= -->
## benefits of close modifiers

The most relevant option available, with regards to sectioning nodes, is case 1:
Close sections while the enter event of a sectioning node is being entered.

Note that the above considerations of that case ...

* apply to type-1 and type-2 sectioning nodes alike. That is, a type-1
  sectioning node can technically close open type-1 and type-2 sections.
* do not take into account, if it should even be allowed to close sections
  in a given context. This case merely states that, from a technical
  perspective, it would be possible and could be allowed.

As stated before, a subsequent sectioning node must be within the scope of a
presequent section, if the section it declares is supposed to become one of its
subsections. That is, because sections must be strongly connected. Likewise,
if the declared section is not supposed to become a subsection, then the scope
of the presequent section must end before the subsequent sectioning node can be
entered.

Consequently, and in order to change the relationship of a subsequent section,
the scope of one or more presequent sections must be altered. Because of that,
users always need to be aware that the definition of a section's relationship
depends on presequent nodes. As such, the default definitions lack clarity when
defining a section hierarchy. That is, because the information which defines a
section's parent section is not strictly bound to the corresponding sectioning
node itself.

In principle, close modifiers provide the means to bind the definition of
a section's relationship to its sectioning node. As such, they allow to
explicitly define the relationship of a declared section and can therefore
be used to express a more obvious section hierarchy.

<!-- ======================================================================= -->
## conclusion

Modifiers/extensions are based upon closing sections. Hence, each modifier can
be loosely understood to instruct the outline algorithm to close one or more
sections. And because they bind the definition of a section's relationship to
its sectioning node, they can be used to clearly express the section hierarchy.

That is, (1) such modifiers are possible, and (2) they improve the overall
design by making it more convenient to express a specific section hierarchy.
Because of that, extending the default definitions by close modifiers is in
general reasonable.

Note however, that the above considerations do not take into account, if
a section can be closed in a given context. As it turns out (see below),
sections can not be closed arbitrarily. The usefulness of close modifiers
therefore has its limits.

<!-- ======================================================================= -->
## HTML's current approach

The biggest issues with HTML's current approach are (1) sections can be closed
inside of an associated container, and (2) sections may contain nodes that are
siblings to their ancestor nodes.

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
be more appropriate to reuse the `<title>` element instead).

Note that the rank of a heading content element is essentially a close modifier.
Because of that, rank values are more or less a mere matter of convenience.
That is, if HTML had a rank-less heading element (i.e. the `<h>` element).

Note that both issues are sufficient to render any attempt to add dynamic
support into a fruitless effort. That is, because transformations would end
up tearing the above `<div>` container apart. Consequently, the result of such
operations is not guaranteed to be semantically equivalent to the initial node
tree.


```
HTML-4:          this approach:             table of contents:
=======          ====================       ==================
<h1>A</h1>       <section> <h1>A</h1>       1. A
B                B                          1.1. D
<div>            <div>
  C                C
  <h1>D</h1>       <section> <h1>D</h1>
  E                E </section>
</div>           </div>
F                F </section>
```

From the perspective of this approach, (1) is due to implicit associations,
and (2) due to the concept of parent containers, a non-issue.

Note that, in contrary to HTML's common practice, the container's inner
section is a subsection to the presequent outer section. That is, section
`D` is a subsection (i.e. not a sibling section) to section `A`.

Note that the default definitions of this approach are rank-less definitions.
Thus far, rank values are undefined.

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
of `s0`. However, and because `n0` is still associated with `s0`, any content
node of `s1` remains to be (by implicit association) a content node of `s0`.

The conflicting statements therefore are:
(1) `s1` is not a subsection of `s0` (by definition of `n1`), and
(2) `s1` is a subsection of `s0` (by structural relationship via `n0:s0`).

In order to avoid such conflicts, any instruction to close `s0` must be ignored.
That is, because `s1` is by structural relationship a subsection of `s0`. Under
these kind of circumstances, `n1` can not be allowed to close `s0`.

Note that these structural dependencies can not be undefined. Because of that,
structural relationships override any extended definition. That is, those
dependencies always have precedence over any close modifier.

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

Note HTML's definition of sectioning content elements (an error):
These are defined to close any section except for the next ancestor section of
a sectioning content or a sectioning root element, regardless of intermediate,
inactive ancestor nodes. Because of that, HTML's definition ignores structural
dependencies.

**CLARIFICATION**
The default definitions of sectioning nodes are consistent with implicit
associations. Therefore, implicit associations have no effect (i.e. are
dormant) for as long as no additions are made to the default definitions.
That is, implicit associations will only surface in combination with close
modifiers.

Note that, by default, any section still ends with its default scope. That is,
because no sectioning node is defined to close a presequent section. Because of
that, the above implicit associations do not trigger these kind of conflicts.

<!-- ======================================================================= -->
## parent containers

Any parent node is a parent container, if it is a type-1 sectioning node, or
if it has type-2 sectioning nodes as child nodes. That is, because sections
must not be allowed to reach past their parent containers. Consistent dynamic
support could otherwise not be guaranteed.

Any parent node can therefore become a section's parent container, regardless
of its specific definition. Because of that, such parent containers exist
whether they are manually injected (explicit), or due to structural dependencies
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

Note that `s3` is a forced subsection of `s1`.

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

Note that the node levels of the corresponding sectioning nodes don't have to
be equal for as long as both nodes are located within two different subtrees.
The effect will still be covered by case 1 (i.e. `s2` is closed when `n4` is
entered).

**case 4: (same parent container)**

```
      n0
 ------------
 n1        n2
```

* `n1, n2` are type-2 sectioning nodes

However, `n2` is in principle free to close the open presequent section `s1`, if
(and only if) both type-2 sectioning nodes have the same parent node (i.e. the
same parent container).

Note that the parent section of `s2`, if `n2` is defined to close `s1`, can only
be one of the remaining open sections, which all are ancestor sections of `s1`.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Parent containers have significant impact on the use of close modifiers.

Note that the above considerations have precedence over any extended definition.
That is, such non-default definitions must be ignored, if they are in conflict
with structural dependencies. Hence, the use of extended definitions is limited.

Note that this can be understood to indicate that, in principle, the default
definitions have precedence over any non-default definition. That is, such
definitions must be made with regards to the default definitions. Consequently,
they can not be in conflict with those default definitions.

**Mind hook**
The placement of sectioning nodes is significant.
