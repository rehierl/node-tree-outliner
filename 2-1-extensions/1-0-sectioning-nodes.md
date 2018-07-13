
<!-- ======================================================================= -->
# Design - extensions (sectioning nodes)

The only case that can be used to extend the definitions of sectioning nodes
is case 1: Close presequent sections before executing any operation that is
associated with the node's enter event.

Note that the considerations of that case apply to type-1 and type-2 sectioning
nodes alike. That is, a type-1 sectioning node could technically close type-1
and type-2 sections.

**TODO**
a heading that has a rank may/can act as an end-marker node -
that is, a rank value adds an additional role to a heading element -
could that be used to proof that no t1 section can be closed?

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
support into a fruitless effort. That is because transformations would end
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
## derived statements

```
   n0
========
 n1  n2
----
 n3
```

* `n0` is an inactive parent node (associated with `s0`)
* `n1` is a type-1 or type-2 sectioning node
* `n1`'s close modifier instructs to close `s0`

**CLARIFICATION**
Section `s1`, which is declared by some sectioning node `n1`, is a "forced
subsection" (or "structural subsection") of `s0` (i.e. regardless of any close
modifier), if `n1` is a descendant of a node that is associated with `s0`.

Note that this statement applies whether sectioning node `n1` ...

* is a type-1, or a type-2 sectioning node.
* is associated with the section it declares (i.e. `s1`) or not.

Note HTML's definition of sectioning content elements (a design error):
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

**Mind hook**
The placement of sectioning nodes is significant.
