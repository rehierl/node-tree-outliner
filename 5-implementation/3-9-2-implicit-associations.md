
<!-- ======================================================================= -->
# implicit associations

(related to the implementation of forced subsections)

The focus of this part is on the implementation of:
How to avoid conflicts due to implicit associations,
if close modifiers had to be supported?

<!-- ======================================================================= -->
## example fragment

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
declared `s3` to be independent of `s1`. Under these kind of circumstances,
any such close modifier must be ignored. That is, because these structural
dependencies can not be undefined. Consequently, implicit associations have
precedence over any non-default definition, if both sections have different
parent containers (i.e. `n0` vs. `n2`, see extensions).

Note that `s4` has the same parent container as `s3` (i.e. `n2`). However, that
is not the case between `s4` and `s1`. Because of that, `n4` may close `s3`,
but not `s1`. Consequently, `s4` is like `s3` by structural relationship still
a subsection to `s1`.

Note that `n5` may close `s1` and, just like `n1`,
may technically even close `s0`.

<!-- ======================================================================= -->
## selecting the parent section

In essence, an algorithm is executed on the tree's node sequence. That is, it
enters one node after another and, at some point, enters the next subsequent
sectioning node. At that point, the algorithm's current context contains the
current rooted path of nodes (begins in the node tree's root and ends in the
current sectioning node being entered) and the current path of sections
(begins in the root section and ends in the current section).

If the current sectioning node being entered had no close modifier, then its
declared section would have to become a subsection to the current section.
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
   has to ensure next, that the declared section *is not* a forced
   subsection of the current section.
4. If that test failed (i.e. the declared section *is* a forced
   subsection), then the algorithm can not close the current section.
   Because of that, the current loop must be exited (i.e. break).
5. If instead that test succeeded (i.e. the declared section *is not*
   a forced subsection), then the algorithm needs to close and pop
   the current section. After that, the current section's parent
   section is the new current section.
6. (continue to loop)

Once that loop was exited, the declared section must be added as subsection to
the (new) current section. After that, the declared section is the new current
section.

Note that it is not possible to bypass this loop in order to improve performance
by "skipping some of the ancestor sections". That is, because ...

* (1) one or more open sections can themselves be forced subsections with
  regards to their parent sections (e.g. `s3` in case of entering `n4`). If
  there is even one such forced subsection amongst the open sections, then
  the declared section of the sectioning node being entered is itself a
  forced subsection. Consequently, the declared section is a sibling section
  to the least significant open forced subsection. That is, if the close
  modifier instructs to close the appropriate amount of sections.
* (2) close operations could be used to trigger custom event handlers. Because
  of that, each section must be closed explicitly and in an orderly fashion.

Note that a `bool Section.isForcedSubsection` property (i.e. the property's
section object is, with regards to its parent section, a forced subsection),
set after exiting the loop, can not be used to improve the performance. That
is, because all tests depend on the relationship between the declared section
and the corresponding current section, not on the relationship between the
current section and its parent section.

**TODO**
need a proof-of-concept implementation to see whether that loop truly manages
to properly deal with all possible cases - intermediate parent containers might
require some adjustments? - don't see why, but you never know ...

<!-- ======================================================================= -->
## basic method of detection

The question therefore is: How exactly can an algorithm detect whether or not
the declared subsequent section is a forced subsection of an open section?

As stated in the extensions chapter, an algorithm is free to close a presequent
section if (and only if) it has the same parent container as the subsequent
section. Because of that, multiple options are available, each with its own
advantages and disadvantages:

Note that all options, except for the last one, technically allow to close
type-1 sections from within such a section. That is, if it would not be allowed
to execute these kind of close operations, then additional case dependent tests
are required. Consequently, if it would not be allowed to close type-1 sections,
then no additional case dependent test are required if (and only if) the last
option is used.

Note that the universal section has no existing parent container (i.e. virtual).
This aspect might have to be taken into account, if a close modifier instructs
the algorithm to close all open sections (up to and including the root section).
Whether or not this should even be allowed/possible is an aspect that still
needs to be taken care of.

**Option 1:** parent container references, node identifiers

Keeping a reference of a section's parent container with each section object,
set when creating a such an object, would probably be the obvious first choice.
Which is, because these node references can be tested for reference equality.
That is, the presequent section can be closed, if both references are equal.
Otherwise, the subsequent section is identified to be a forced subsection.

Note that a running algorithm will neither encounter case-1 nor case-3 (see
the extensions chapter). That is, because the corresponding presequent sections
are already closed and will therefore no longer appear within the current path
of sections. Because of that, the remaining relevant cases are case-2 and
case-4.

However, holding a node reference with each section object will obviously
increase the memory footprint of the resulting outline. Hence, these references
can, but should not be used by implementations. That is, unless they have any
additional use besides the outline algorithm itself, there is no need to add
such a permanent property to each section object.

Note that node references are very similar to unique number identifier values.
Because of that, and depending on an implementation's specific environment
(e.g. adjacency lists), node identifiers could be (or even have to be) used
instead of object references.

**Option 2:** sectioning node -> parent container reference

As a section's parent container can be determined from its sectioning node, the
parent container references could be determined on the fly by taking advantage
of the `Section.sectioningNode` properties (i.e. `sectioningNode` in case of a
type-1, and `sectioningNode.parentNode` in case of a type-2 sectioning node).
That is, if the algorithm's environment provides the means to access a node's
parent node (e.g. event driven parsers?).

However, and depending on the environment (e.g. low-level implementations highly
optimized to produce hierarchical listings of section properties on the fly),
the node references of the sectioning nodes are neither required, nor guaranteed
to be valid when the algorithm has to execute the above mentioned tests.

Note that all nodes in the current rooted path of nodes have been entered,
but not yet exited. Therefore, and if an implementation has access to node
references (in contrary to pure node identifiers), the references of those
nodes remain valid for at least until those nodes are exited. This aspect
could however become an issue, if low-level (i.e. pointer-based, no garbage
collection) programming languages or interfaces are used. Those have in
general the option to destroy the referenced nodes once those were exited
(e.g. presequent type-2 sectioning nodes). Therefore, an attempt to retrieve
a reference of a section's parent container via a reference of the section's
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
it knows exactly when it enters the next node (level+1) and when that node is
being exited (level-1).

The tree traversal algorithm can therefore pass the node level of the current
node on to the corresponding event handler. Consequently, the node level of
the current node does not have to be calculated from scratch by counting the
number of its ancestors. In addition to that, and when creating a new section
object while entering its sectioning node, the node level of its parent
container can be determined and stored inside of the new section object.

As mentioned before, such an additional property will increase the memory
footprint of the outline. But, as number values can usually be limited to
a reasonable range of values, those properties would require less memory
as reference properties (e.g. 64-bit in case of references vs. 8- or 16-bit
in case of node level values). Because of that, node level properties could
be considered as an acceptable alternative.

**Option 4-1:** node levels of sectioning nodes
(if it is allowed to close type-1 sections)

Obviously, a test that is solely based upon the references of sectioning
nodes can not work. That is, because each sectioning node declares one
section only. And, because of that, two subsequent sections will always
have different references, which is why testing these for equality will
always evaluate to `false`.

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

* (1) `n1` can technically close `s0` => test: `(level(n1) == level(n0) + 1)`
* (2) `n2` can close `s1` => test: `(level(n2) == level(n1) + 0)`

Obviously, test-1 is different to test-2, which is why case dependent tests are
required. That is, the node level values of sectioning nodes can not be used for
general purpose tests while being unaware of the involved section types.

Note that, the adjustment of these node level values, according to the section
types involved, will essentially be equivalent to option 3 (i.e. using the
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
