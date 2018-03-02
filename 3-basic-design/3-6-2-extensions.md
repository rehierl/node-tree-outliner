
<!-- ======================================================================= -->
# Design - extending the default definitions

The focus of the following considerations is not to define entirely new types
of sectioning nodes, but to evaluate those options which allow to deviate from
the default definition of sectioning nodes. Hence, the first step is to take a
look at those aspects that can be altered.

Note that such options can be used to define modifiers which extend the default
definition of sectioning nodes. Consequently, such modifiers are intended to
alter the definition of sectioning nodes while maintaining consistency with the
default definitions.

<!-- ======================================================================= -->
## available options

> options when entering a sectioning node

When a sectioning node is being entered, an algorithm has in principle knowledge
of all those nodes that it has already visited. Because of that, it knows about
all those sections that are presequent to the current sectioning node (i.e. the
closed/independent and the open presequent sections). In contrary to that, an
algorithm is unaware of any subsequent node. Those might or might not exist
(i.e. there is no guarantee that there is even one such node).

The knowledge of those sections that are already closed is not required by the
default definitions. Because of that, the definition of modifiers with regards
to those closed sections would add additional complexity to an implementation.
That is, because it would then have to remember all those sections that it has
already created as it could not know when that information might be required.

In addition to that, modifiers could only be allowed to use that additional
information to affect the section which is declared by the current sectioning
node. That is, because no more changes are allowed to closed sections. Also,
as those sections are already closed, they are by definition not allowed to
have any effect on subsequent sections (Note that this statement is based upon
the formal perspective of multiple associations per node).

Consequently, and because the intention of this current case is to have an
effect on a declared section when entering its sectioning node, what remains
are the open presequent sections. In addition to that, the only operation that
can be executed on these sections is to close them. However, and as mentioned
before, open sections can not be closed arbitrarily. That is, because any
ancestor section must remain open for as long as any of its subsections are
open.

Obviously, the effect of closing the current and least significant open section
(i.e. the current section) is that the section of the current sectioning node
will not become a subsection of the (to be closed) current section. As such,
the option to close sections allows to arbitrarily select the declared section's
parent section from the current list of open sections.

Note that any other available option (besides closing presequent sections)
is not relevant for the current considerations.

Note that, the same reasoning, with regards to closed presequent and all
subsequent sections, also applies to the following two cases. That is, these
may also only close those sections that are presequent to the corresponding
exit event.

Note that this option could also be used for the definition of an optional
end-marker node (e.g. `<close />`, defined to close type-2 sections). That is,
if the corresponding modifier would be defined to close the relevant sections
before the end-marker node itself has to be associated. That is, such a node
would then belong to the parent section of the most significant section that
it has to close.

> options when exiting a type-1 sectioning node

Closing those sections that are presequent to the exit event of a a type-1
sectioning node would be technically possible.

Note however, that a type-1 sectioning node also represents the parent container
of the section it declares. That is, none of those sections that are declared
inside of a type-1 sectioning node are not allowed to reach past that current
sectioning node. Consequently, those inner sections always have to be closed
first, regardless of any modifier. And, because of that, such a modifier can
only affect those open presequent sections that are presequent to the type-1
sectioning node's enter event.

In contrary to the above case, the corresponding sectioning node, and all of
its inner content already is associated. That is, such a modifier is no longer
in the position to alter the association of the sectioning node (i.e. associate
with a different parent section) or the association of the inner content.
Consequently, such a modifier can only affect subsequent nodes and sections.
That is, this option could be used to mark the end of a branch of the section
hierarchy.

Note that this option could also be used for the definition of an optional
end-marker node. However, that node would then be associated with the current
section. As such, and if more than one sections would have to be closed, it
could be difficult to detect why ancestor sections were closed. That is, because
that node would then be "located" inside of an inner section and thus might not
necessarily be accessible to its ancestor sections  (i.e. a reason as to why
not to associate end-marker nodes with the sections they close).

> options when exiting a type-2 sectioning node

Closing those sections that are presequent to the exit event
of a type-2 sectioning node is not an option.

That is, because it would result in conflicting statements with regards to the
logical location of such a sectioning node and the section's content nodes.
Essentially, the sectioning node, which is associated while it is being entered,
would then belong to a section that is independent to the section with which
the declared section's content nodes will be associated.

Note that type-2 sectioning nodes are defined not to have any inner sectioning
nodes themselves.

**Memory hook**
Modifiers/extensions can only result in closing sections.

<!-- ======================================================================= -->
## benefits of close modifiers

The most relevant option available is to close sections while a subsequent
sectioning node is being entered.

Note that the above considerations related to this option ...

* apply to type-1 and type-2 sectioning nodes alike.
* do not take into account, if it could even be allowed to
  close the relevant outer sections. This option merely states
  that, from a technical perspective, it would be possible.

Assumed that there would be no limitations,
what could be the advantages of such close modifiers?

**TODO**
default definitions are not exactly user-friendly -

**TODO**
the injection of explicit parent containers is tricky -
edit the scope of a presequent section in order to edit
the relationship of a subsequent section -
define means (e.g. rank) that allow to simplify this process -
that is, the rank is a matter of convenience

**TODO**
A parent node is "turned into" a parent container of a type-2 section by an
optional subsequent sectioning node. That is, a parent node can not determine,
while it is being entered, whether it will have to close any inner sections
during its exit event. inconsistency? -
no, because it is a requirement of the subsequent section -
and a paren container does itself not have to be aware that it is one -

<!-- ======================================================================= -->
## HTML's current approach

The two biggest issues with HTML's current approach are (1) to close a section
inside of an associated container, and (2) to continue a section past its
ancestor nodes.

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

Note that in HTML, the first element of heading content (e.g. `<h1>`) inside
of `<section>` elements is reused to define the section's heading. That is,
the first such element does not represent a type-2 sectioning node. (It would
be more appropriate to reuse the `<title>` element instead).

Note that both issues are sufficient to turn any attempt to add dynamic
support into a fruitless effort. That is, because the resulting node tree,
after executing the necessary transformations, is not guaranteed to accurately
represent the initial node tree (i.e. the above `<div>` container would have
to be broken apart).


```
HTML-4:        this design:             table of contents:
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

From the perspective of this design, (1) is due to implicit associations,
and (2) due to the concept of parent containers, a none-issue.

Note that, in contrary to the common practice, the container's inner section
is a subsection to the outer presequent section (i.e. not a sibling section).

Note that the default definitions are rank-less definitions.

<!-- ======================================================================= -->
## implicit associations

```
   n0
========
 n1  n2
----
 n3
```

* `n0` is an inactive parent container (associated with `s0`)
* `n1` is a sectioning node (type-1 or type-2, declares `s1`)
* `n2,n3` are inactive nodes

If, for example, the definition of `n1` would be altered in such a way that
entering `n1` would result in closing section `s0` (but no other ancestor
section in addition to that), then `s1` would be, by the definition of `n1`,
a sibling section to `s0`. That is, no content node of `s1` is a content node
of `s0`. However, because `n0` is still associated with `s0`, any content node
of `s1` remains to be an implicit content node of `s0`.

The conflicting statements therefore are:
(1) `s1` is not a subsection of `s0` (modified definition of `n1`), and
(2) `s1` is a subsection of `s0` (structural relationship via `n0:s0`).

Under these kind of circumstances, `n1` can not be allowed to close `s0`.
In order to avoid such conflicts, any instruction to close `s0` must be
ignored because `s1` is by structural relationship a subsection of `s0`.

Note that these structural dependencies can not be undefined. Because of that,
structural dependencies override any non-default definition. That is, those
always have precedence over any modified/extended definition.

Note that these considerations are independent of where (inside of a node tree)
such a subtree can be found. Such a subtree will always result in the afore
mentioned conflict.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Sections can not be closed arbitrarily.

**CLARIFICATION**
Section `s1`, which is declared by a sectioning node `n1`, is a subsection to
`s0` (i.e. regardless of any non-default definition), if `n1` is a descendant
of a node that is associated with `s0`.

Note that this statement applies whether sectioning node `n1` ...

* is a type-1, or a type-2 sectioning node.
* is associated with the section it declares (i.e. `s1`) or not.

Note HTML's definition of sectioning content elements (an error). And in
combination with "the first element of heading content" (another error).

**CLARIFICATION**
The default definitions of sectioning nodes are consistent with (these kind of)
implicit associations. Therefore, implicit associations have no effect (i.e.
are dormant) for as long as no changes or additions are made to the default
definitions. That is, they will only surface in combination with non-default
definitions.

Note that, by default, any section still ends with its default scope. That is,
because no sectioning node is defined to close a presequent section. Because of
that, the above implicit associations can not trigger these kind of conflicts.

<!-- ======================================================================= -->
## same parent containers

As mentioned before, a section's parent container isn't a parent container
because the definition of the corresponding node has certain characteristics.

Any parent node is a parent container, if it is a type-1 sectioning node, or
if it has type-2 sectioning nodes as child nodes. Consistent dynamic support
could otherwise not be guaranteed (i.e. sections can not be allowed to reach
past their parent containers). In short: Any parent node can become a section's
parent container, regardless of its specific definition.

Because of that, such parent containers exist whether they are manually
injected (explicit), or due to structural circumstances (implicit).

Note that a node can be defined to never be a section's parent container, if
(and only if) the node is not allowed to have type-2 sectioning nodes as child
nodes (e.g. type-2 sectioning nodes). However, a general purpose implementation
is unaware of these kind of additional definitions. That is, in case of input
errors or redefinitions, such an implementation will still treat descendant
sectioning nodes as actual sectioning nodes and thus the corresponding nodes
as parent containers. Because of that, reusing sectioning nodes for purposes
other than to declare new sections must be avoided.

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
`s3`. That is, `s2` can not be a subsection to `s3` and `n2` can no longer
close `s3` (as it is already closed when `n2` is being entered).

Note that, from the perspective of this design, this case is a non-issue. That
is, because sections will be ignored by subsequent operations as soon as they
are closed. Because of that, any such modified definition (with regards to `n2`)
is not understood to be with regards to `n3/s3`, but with regards to some other
open presequent section. Consequently, modified definitions may yield unexpected
results, if this structural aspect is not correctly taken into account.

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
that is a top-level node of `s1`. Consequently, `s3` is by implicit association
a subsection to `s1`. Because of that, and in order to avoid conflicting
statements, any attempt to close `s1` when `n3` is being entered, must be
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

Note that this case can be understood to contain two subsequent subtrees that
have `n1` and `n3` as their root nodes. Because of that, this case is similar
to case 1: `s2` will be closed before `n4` is even entered.

Note that the node levels of the corresponding sectioning nodes don't have
to be identical for as long as both nodes are located within two different
subtrees. The effect will still be covered by case 1: `s2` will be closed
before `n4` is entered.

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

Note that the actual parent section of `s2` can only be one of the remaining
open sections, which all are presequent ancestor sections of `s1`.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Parent containers have significant impact on the use of extended definitions.

Note that the above considerations have precedence over any extended definition.
That is, such non-default definitions must be ignored, if they are in conflict
with structural dependencies. Hence, the use of such definitions is limited.

Note that this can be understood as an indication that, in principle, the
default definitions have precedence over any non-default definition. That
is, such definitions must not be in conflict with the default definitions.

**CLARIFICATION**
In order for non-default definitions to not yield any conflict, or an
unexpected result, the corresponding type-2 sectioning nodes must have
the same parent container.

**Mind hook**
The placement of sectioning nodes is significant.

<!-- ======================================================================= -->

**TODO**
"extended" rather than "modified" definitions -
just a naming related aspect
