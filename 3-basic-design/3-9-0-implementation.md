
<!-- ======================================================================= -->
# How to implement ...

The following content is intended to clarify implementation specific aspects.

<!-- ======================================================================= -->
## top-level nodes

(related to the support of transformations)

associating a node (strict association) with a section is equivalent to
associating a whole subtree of nodes (implicit associations). -

two levels of implicitness -
implicitly with the explicitly associated section (associate a subtree),
and implicitly with the implicitly associated section (one section only)

can an algorithm easily store references to all top-level nodes? -
issue: associate with one section only (not that easy) -
issue: subsequent t2 with equal or higher rank (tricky) -

when a section is being closed, or as an on demand feature? -
is it possible to avoid having to determine them as a post-process
by providing a list of top-level nodes? -
e.g. `Node[] Section.getTopLevelNodes()` -

the first top-level node is easy to determine (entering) -
the last top-level node could be determined when closing a section -
after all, each section does have its own close event -
last child if closed by a parent container -
previous sibling when closed by a t2 sectioning node -

t2 -> t1 transformations must take into account, that
they could be the cause for new first and/or last top-level nodes -
the corresponding node references, if any, need to be updated

<!-- ======================================================================= -->
## test: is node 'n' associated with section 's'?

If node `n` is strictly associated with section `sX` (one reference per node),
and if the question is, whether node `n` is also associated with section `sY`,
then the expression `(sX == sY)` needs to be tested first. If that test fails,
then it needs to be tested whether section `sY` is an ancestor section of `sX`.

```
isAssociatedWith(Node node, Section section) begin
  parentSection = node.parentSection
  
  while(parentSection != null) begin
    if(parentSection == section) return true
    parentSection = parentSection.parentSection
  end
  
  return false
end
```

Consequently, node `n` is not associated with section `sY`,
if (and only if) all of the afore mentioned tests have failed.

Note that an implicit association is not guaranteed to be verified correctly
(i.e. false negatives are possible), if only the ancestor nodes of node `n`
are tested. That is, because type-2 sections can be hidden by that rooted
path of nodes.

<!-- ======================================================================= -->
## parent containers

(related to the implementation of sectioning nodes)

The focus of this part is on the implementation of:
Close one or more inner sections when exiting a parent container.

```
n0
=========
n1 n2 ...
```

* `n0` represents an inactive parent container
* `n0` is associated with section `s0`
* `n1,n2` represent type-2 sectioning nodes
* `n1,n2` declare sections `s1,s2`

By definition, the trace of section sequences is:

```
trace of sequences:     -  node event:
======================  -  ====================
(s0)                    -  just before entering n0
(s0,s1)                 -  just after exiting n1
(s0,s1,s2)              -  just after exiting n2
...                     -  ...
(s0,s1,s2)              -  just before exiting n0
(s0,s1)                 -  while exiting n0
(s0)                    -  just after exiting n0
```

Note that the sequence of sections just before entering the parent container
is identical to the sequence of sections just after exiting said container.
Because of that, an implementation must restore the sequence of sections
when exiting a parent container.

As mentioned before, any parent node can in principle act as the parent
container of one or more sections. The only exception to that rule are the
type-1 sectioning nodes: These always are parent containers. Because of that,
and when exiting any parent node, an implementation must test whether inner
sections need to be closed.

1. Inner sections may have parent containers that are descendants to `n0`.
   The inner sections of these parent containers will be closed before the
   exit event of `n0` is reached (i.e. the same issue, but with regards to
   inner containers).
2. `n0` is the parent container of inner sections, but some subsequent,
   non-default extended definition applies. These sections will be closed
   before the exit event of `n0` is entered.
3. `n0` is the parent container of inner sections, and no non-default rule
   applies. The exit event of `n0` must close these remaining open sections.

In short, the exit event of a given parent container must only close those
sections that remain to be open by the time the parent container is being
exited. All other closed inner sections can and will be ignored (i.e those
are no longer relevant).

Because of that, all relevant sections are part of the current section sequence.
Furthermore, and because all those sections are subsections to the section, with
which the parent container is associated, the relevant sections are located at
the very end of the current section sequence. Consequently, an implementation
must only pop and close the top-most sections from the section stack until the
current section matches the parent container's parent section:

```
onExitParentContainer(Node container) begin
  //- currentSection is a global reference
  while(currentSection !== container.parentSection) begin
    parentSection = currentSection.parentSection
    currentSection.close()
    currentSection = parentSection
  end
end
```

Note that ...

* all nodes are associated while they are being entered. Because of that, a
  parent container's parent section reference is always set when the parent
  container is being exited.
* the root node must be associated with the universal section.
* the remaining open inner sections will be closed in reverse order. That
  is, subsections will be closed before their ancestor sections are closed.
* an implementation does not have to know how many sections need to be closed.
* the close operation of an implementation could have implicit side effects
  (e.g. due to releasing locked resources).

With regards to efficiency, it does not appear to be possible to gain anything
from maintaining a boolean `isParentContainer` flag variable. Therefore, and
apart from gaining some amount of additional clarity, an implementation does
not have to test beforehand (e.g. by the use of an `if-then` construct),
whether the node in question is indeed a parent container. That is, one test
must always be executed either way (i.e. even if the corresponding parent node
is actually not a parent container).

<!-- ======================================================================= -->
## implicit associations

(related to the implementation of forced subsections)

The focus of this part is on the implementation of:
How to avoid conflicts due to implicit associations,
if close modifiers had to be supported?

### example fragment

```
      n0
================
n1 n2         n5
   --------
      n3 n4
```

* `n0` represents a type-1 sectioning node
* `n1, n3-5` represent type-2 sectioning nodes
* `n2` represents an inactive parent node

Note that `s3` is, first and foremost due to its structural relationship, a
subsection of `s1`. That is, even if `s3` would have a close modifier which
defined `s3` to be independent of `s1`. Under these kind of circumstances,
any close modifier must be ignored. That is, because these structural
dependencies can not be undefined. Consequently, implicit associations have
precedence over any non-default definition, if both sections have different
parent containers (i.e. `n0` vs. `n2`, see extensions).

Note that `s4` has the same parent container as `s3` (i.e. `n2`). However, that
is not the case between `s4` and `s1`. Because of that, `n4` may close `s3`,
but not `s1`. Consequently, `s4` is like `s3` by structural relationship still
a subsection to `s1`.

Note that `n5` may close `s1` and, just like `n1`,
may technically even close `s0`.

### selecting the parent section

In essence, an algorithm is executed on the tree's node sequence. That is, it
enters one node after another and, at some point, enters the next subsequent
sectioning node. At that point, the algorithm's current context contains the
current rooted path of nodes (begins in the node tree's root and ends in the
current sectioning node being entered) and the current path of sections
(begins in the root section and ends in the current section).

If the current sectioning node being entered had no close modifier, then its
declared section would have to become the subsection of the current section.
This case obviously represents the default definitions. Because of that, it is
assumed that the current sectioning node holds a close modifier which instructs
the algorithm to close one or more sections.

And because no ancestor section can be closed before any of its subsections are
closed (sections must be closed in an orderly, bottom-up fashion), the section
that has to be closed first always is the current section.

In order to avoid any conflict, the algorithm needs to
execute the following loop:

1. Evaluate the sectioning node's close modifier in order to determine,
   whether there (still) are sections that need to be closed.
2. Exit the loop, if no sections need to be closed (i.e. break).
3. Because sections can not be closed arbitrarily, the algorithm
   has to test next, if the declared section *is not* a forced
   subsection of the current section.
4. If that test failed (i.e. the declared section *is* a forced
   subsection), then the algorithm can not close the current section.
   The current loop must be exited (i.e. break).
5. If that test succeeded (i.e. the declared section *is not*
   a forced subsection), then the algorithm needs to close and pop
   the current section. After that, the current section's parent
   section is the new current section.
6. (continue to loop)

Finally, the declared section can be added as subsection to the (new)
current section. After that, the declared section is the new current section.

Note that it is not possible to bypass this loop in order to improve the
performance by "skipping some of the ancestor section". That is, because ...

* (1) any open section can itself be a forced subsection of its ancestor
  sections (e.g. `s3` in case of entering `n4`). If there is even one such
  ancestor section, then the declared section of the sectioning node being
  entered must become a subsection of the least significant forced subsection.
  That is, if the close modifier instructs to close the appropriate amount
  of sections.
* (2) close operations could be used to trigger custom event handlers.
  Because of that, each section must be closed explicitly and in the
  right bottom-up order.

Note that a `bool Section.isForcedSubsection` property (i.e. the property's
section object is, with regards to its parent section, a forced subsection),
set after executing step 6 can not be used to improve the performance. That
is, because all tests only depend on the declared subsequent section and
the corresponding current section. Consequently, they do not depend on the
relationship between the already open sections. However, that property
could however still prove useful for debugging purposes.

**TODO**
need a proof-of-concept implementation to see whether that loop truly manages
to properly deal with all possible cases - intermediate parent containers might
require some adjustments? - don't see why, but you never know ...

### basic method of detection

The question therefore is: How exactly can an algorithm detect whether or not
the declared subsequent section is a forced subsection of an open section?

As stated in the extensions chapter, an algorithm is free to close a presequent
section if (and only if) it has the same parent container as the subsequent
section. Because of that, multiple options are available, each with its own
advantages and disadvantages:

Note that all options, except for the last one, technically allow to close
type-1 sections. That is, if it would not be allowed to close certain sections,
then additional, case dependent tests would be required.

Note that the universal section has no existing parent container (i.e. virtual).
This aspect might have to be taken into account, if a close modifier instructs
the algorithm to close all open sections (including the root section). Whether
or not this should even be allowed/possible is an aspect that still needs to be
investigated.

**Option 1:** parent container references, node identifiers

Keeping a reference of a section's parent container with each section object,
set when creating a new section object, would probably be the obvious first
choice. Which is, because these node references can be tested for reference
equality. That is, the presequent section can be closed, if both references
are equal. Otherwise, the subsequent section is identified to be a forced
subsection.

Note that a running algorithm will neither encounter case-1 nor case-3 (see
the extensions chapter). That is, because the corresponding presequent sections
are already closed and will therefore no longer appear within the current path
of sections. Because of that, the remaining relevant cases are case-2 and
case-4.

However, holding a node reference with each section object will obviously
increase the memory footprint of the resulting outline. Not to mention the
additional efforts required related to documentation, update requirements,
etc. Hence, these references can, but should not be used by implementations.
That is, unless they have any additional use besides the outline algorithm
itself.

Note that node references are very similar to unique number identifier values.
Because of that, and depending on an implementation's specific environment
(e.g. adjacency lists), node identifiers could be (or even have to be) used
instead of object references.

**Option 2:** sectioning node -> parent container references

As a section's parent container can be determined from its sectioning node, the
parent container references could be retrieved on the fly by taking advantage
of the `Section.sectioningNode` properties (i.e. `sectioningNode` in case of a
type-1, and `sectioningNode.parentNode` in case of a type-2 sectioning node).
That is, if the algorithm's environment provides the means to access a node's
parent node (e.g. event driven parsers?).

However, and depending on the environment (e.g. low-level implementations highly
optimized to produce hierarchical listings of section properties on the fly),
the node references of the sectioning nodes are neither required, nor guaranteed
to be valid when the algorithm has to execute the above mentioned tests.

Note that all nodes in the current rooted path of nodes have been entered,
but not yet exited. Hence, if an implementation has access to node references
(in contrary to pure node identifiers), the references of those nodes remain
valid for at least until those nodes are exited. This aspect could however
become an issue, if low-level (i.e. pointer-based, no garbage collection)
programming languages or interfaces are used. Those have in general the option
to destroy node references once the corresponding nodes have been exited (e.g.
presequent type-2 sectioning nodes). Therefore, an attempt to retrieve a
reference of a section's parent container via a reference of the section's
sectioning node could result in access violation errors.

**Option 3:** node levels of parent containers

A third option is the use of node level values. That is, the current section
can be closed, if the node level of the subsequent section's parent container
is equal to the node level of the current section's parent container. Otherwise,
and because case-1 and case-3 never apply, the subsequent section is a forced
subsection.

Note that, in general, the parent container of an ancestor section *never* is
a descendant of a subsection's parent container. Because of that, the parent
container of a descendant section is *never* closer to the root node than the
parent containers of its ancestor sections. Consequently, the node level of a
subsection's parent container always is greater or equal than the node level
of an ancestor section's parent container.

In cases where an implementation environment does not provide the means to
determine a node's node level, these values have to be determined "manually".
However, the implementation of the tree traversal algorithm does provide the
means to efficiently maintain a "current node level" value. That is, because
it knows exactly when it enters a new node (level+1) and when that node is
being exited (level-1).

The tree traversal algorithm can therefore pass the node level of the current
node on to the corresponding event handler. Consequently, the node level of
the current node does not have to be calculated from scratch by counting the
number of its ancestors. In addition to that, and when creating a new section
object while entering its sectioning node, the node level of its parent
container can be determined and stored inside of the new section object.

**Option 4-1:** node levels of sectioning nodes
(if it is allowed to close type-1 sections)

Obviously, a test that is solely based upon the references of sectioning nodes
can not work. That is, because each sectioning node declares one section only.
Consequently, two subsequent sections will always have different references,
which is why testing these for equality will always evaluate to `false`.

```
      n0
 ------------
 n1        n2
```

* `n0` is a type-1 sectioning node
* `n1,2` are type-2 sectioning nodes

However, one might tend to suspect/hope that the node levels of the sectioning
nodes could be used directly. That is, instead of the node levels of the parent
containers. Unfortunately, that won't work either. Which is, because it does
depend on the types of sectioning nodes involved.

* (1) `n1` could technically close `s0` => test: `(level(n1) == level(n0) + 1)`
* (2) `n2` could close `s1` => test: `(level(n2) == level(n1) + 0)`

Obviously, test-1 is different to test-2, which is why case dependent tests
would be required. That is, these node levels can not be used for general
purpose tests while being unaware of the involved section types.

Note that, the adjustment of these node level values, according to the section
types involved, would essentially be equivalent to option 3 (i.e. using the
node levels of the corresponding parent containers).

* (1) transformed test: `(level(n1) - 1 == level(n0))`
* Note that `level(n0)` is the node level of `n0`'s parent container.
* Note that `(level(n1) - 1)` is the node level of `n1`'s parent container.
* (2) transformed test: `(level(n2) - 0 == level(n1) - 0)`
* (2) equivalent to: `(level(n2) - 1 == level(n1) - 1)`

<!-- ======================================================================= -->

**Option 4-2:** node levels of sectioning nodes
(if it is prohibited to close any type-1 section)

**TODO**
plot twist: what if closing type-1 sections would/could not be allowed?

can these node level values be used as general purpose filters? -
effectively only t2 sections could be closed -
no additional, type dependent tests required? -
node references could not be used

* if tested for equality, then ...
* t1/2 can not close t1 (inner t1/2: different node levels)
* t1/2 can not close t1 (outer t1/2: presequent t1 is already closed)
* t1 can close t2
* t2 can close t2

now that would be really type-independent -
the node level values of parent containers are type-dependent -
at some point, a section's type must be identified in order to
determine the node level of the corresponding parent container -
