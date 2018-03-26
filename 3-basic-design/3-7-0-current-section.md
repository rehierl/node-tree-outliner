
<!-- ======================================================================= -->
# Design - current section

At any given point in time during the traversal of the node tree, one or more
sections always count as being open. This set of open sections will be referred
to as the current set of open sections (`cs` for "current-set").

* `cs := { s0, s1, s2, ... }` and `(cs subset-of S)`
* `S` is the set of all declared/known sections

If the node sequence of the tree and the sectioning nodes of all open sections
are taken into account, then that set of sections can be understood to define
the current ordered list of open sections (`cl` for "current-list").

* `cl := [ s0, s1, s2, ... ]`
* `(si subsection-of si-k)` for `si in cl` and any `k in [1,i)`
* `(si declared-by ni)` for any `si in cl`
* `(ni subsequent-to ni-k)` for any `k in [1,i)`

**CLARIFICATION**
The current set of open sections will be referred to as "the (current) set of
(open) sections" and the current ordered list of sections as "the (current)
list of (open) sections", or "the (current) sequence of (open) sections".

Note that this list does by itself not represent an existing list object. It
merely represents an ordered listing of sections that, at a given point in
time, still count as being open. That is, this list can be understood as the
result of a lookup operation.

Note that this lookup operation is completely based upon those nodes that have
already been visited (i.e. presequent nodes). That is, an implementation could
maintain such a listing while it is traversing the node tree. However, that
list object must represent the list of sections as is.

<!-- ======================================================================= -->
## list operations

**case 1:** `(s0,s1,s2,s3,s4) => +{s5} => (s0,s1,s2,s3,s4,s5)`

```
            n0
==========================
n1 n2 n3 n4 n5 n6 n7 n8 n9
```

* `n0` declares the next outer type-1 section `s0`
* nodes `n1-9` are all child nodes to `n0`
* other descendant nodes can and will be ignored
* nodes `n1-9` represent type-2 sectioning nodes
* nodes `n1-9` declare sections `s1-9`
* obviously, section `s9` will always be empty

If an implementation begins to enter `n5`, then that list of sections will be
`(s0,s1,s2,s3,s4)`. And because no open presequent section will be closed (i.e.
`s5` is a subsection to `s4`), that list will change into `(s0,s1,s2,s3,s4,s5)`
once section `s5` is open.

**case 2:** `(s0,s1,s2,s3,s4,s6) => -{s6} => (s0,s1,s2,s3,s4)`

```
            n0
==========================
n1 n2 n3 n4 n5    n7 n8 n9
            -----
               n6
```

* `n5` is an inactive parent node
* `n6` is a child node to `n5`

If an implementation exits `n6` (i.e. after opening `s6`), then that list of
sections will be `(s0,s1,s2,s3,s4,s6)` (`s5` does not exist because `n5` is no
longer a sectioning node). After that, the node event which will have to be
executed next is going to be the exit event of `n5`. And because `n5` acts as
the parent container of `s6`, `s6` will have to be closed during that event.
Consequently, the list of sections will no longer contain `s6`, which is why
that list will change into `(s0,s1,s2,s3,s4)`.

**case 3:** `(s0,s1,s2,s3,s4,s6,s7) => -{s6,s7} => (s0,s1,s2,s3,s4)`

```
            n0
==========================
n1 n2 n3 n4 n5       n8 n9
            --------
               n6 n7
```

* `n5` is an inactive parent node
* `n6, n7` are both child nodes of `n5`

In contrary to the previous case, `n5` now has two inner sections (i.e. `s6`
and `s7`). Because of that, and when exiting `n7` after opening `s7`, the list
of sections will be `(s0,s1,s2,s3,s4,s6,s7)` (`s5` does not exist because `n5`
is no longer a sectioning node). Similar as before, the exit event of `n5` has
to close all remaining open inner sections. Consequently, and after `n5`'s exit
event, that list will change into `(s0,s1,s2,s3,s4)`.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The list of sections will be extended by a new section,
if the next node event results in opening a new section.

Note that the new section will always appear at the end of that list (i.e.
not at some arbitrary position). That is, because the new section will be
a subsection to all sections which were part of the list just before opening
the corresponding section (formal perspective).

Note that any sectioning node can only declare a single new section. That
is, no node event will extend the list of sections by more than one section.

**CLARIFICATION**
The list of sections will be reduced by one or more sections,
if the next node event results in closing those sections.

Note that all of these sections will always be removed from the end of the
list (i.e. not from an arbitrary position). That is, because any subsection
must be closed before any of its ancestor sections can be closed. Which is,
because no parent container of an ancestor section is a descendant to the
parent container of any of its subsections.

**CLARIFICATION**
The above cases therefore are independent of which types of sectioning nodes
are encountered. That is, if a section is declared, then that section will be
added to the end of the list of sections. If one or more sections are closed,
then these sections will be removed from the end of that list.

**CLARIFICATION**
If multiple sections need to be closed during the same node event, then those
sections need to be closed in reverse order. That is, if `s6` was opened before
`s7`, then `s7` needs to be closed before `s6` can be closed.

That is, because `s7` is a subsection to `s6` and because no subsection can
remain open if its parent section has to be closed. Put differently, any other
close order would be in conflict with "a parent section is open for as long as
any of its subsections are open".

Note that it might not seem to be relevant in which order sections are closed.
After all, they need to be closed during the same node event. However, the
close order will be relevant, if those operations are used to trigger event
handler routines.

Note that an implementation might initially not be aware of how many inner
sections need to be closed when exiting a given parent container. In addition
to that, an implementation might even not have to be aware of the exact number
(e.g. repeat to close the last, least significant subsection until some
condition holds).

**CLARIFICATION**
The behavior of the list of sections is consistent with the
operations of a first-in-first-out data structure (aka. stack).

1) `push()` a new subsection onto the stack
2) `pop()` the last subsection from the stack
3) `get()` the last subsection from the stack

**CLARIFICATION**
The list of sections can also be
referred to as "the stack of (open) sections.

<!-- ======================================================================= -->
## trace of section sequences

```
            n0
==========================
n1 n2 n3 n4 n5       n8 n9
            --------
               n6 n7
```

* `n5` is an inactive parent node
* `n6, n7` are both child nodes of `n6`

Printing the list of sections at certain points in time, while the above
fragment is being processed, could result in the following trace of section
sequences:

```
trace of sequences:     -  node event:
======================  -  ====================
()                      -  before entering n0
(s0)                    -  after entering n0
(s0,s1)                 -  after exiting n1
...                     -  ...
(s0,s1,s2,s3,s4)        -  after exiting n4
(s0,s1,s2,s3,s4,s6)     -  after exiting n6
(s0,s1,s2,s3,s4,s6,s7)  -  after exiting n7
(s0,s1,s2,s3,s4,s6)     -  while exiting n5
(s0,s1,s2,s3,s4)        -  after exiting n5
(s0,s1,s2,s3,s4,s8)     -  after exiting n8
(s0,s1,s2,s3,s4,s8,s9)  -  after exiting n9
(s0,s1,s2,s3,s4,s8)     -  while exiting n0
(s0,s1,s2,s3,s4)        -  while exiting n0
...                     -  ...
(s0,s1)                 -  while exiting n0
(s0)                    -  while exiting n0
()                      -  after exiting n0
```

Note that the root section `s0` is always located at the beginning of
any sequence. That is, because any other section is a subsection to it.

As mentioned before, and in contrary to the formal perspective, each node
will be associated with one section only (practical perspective). However,
this single association must, based on implicit associations, represent all
formal associations. And, because of that, each node must be associated with
the closest open presequent section in that list. Consequently, the parent
section of any node always is located at the very end of the current sequence.

Note that, if `n0` is a type-1 sectioning node, or an inactive parent container,
then `s0` would represent the section that was used to associate `n0`. Because
of that, `s0` would not have to be created when entering, and closed when
exiting `n0`. In addition to that, all section sequences would begin with some
common prefix, which would always end in `s0`. Replacing node `n0` with an
associated inactive parent container will therefore not result in significant
changes to the above trace of sequences.

**DEFINITION**
The last/top-most section in the list/stack of open sections will be referred
to as the "current section". The "current section" therefore is the current,
least significant open section.

A reference to this section, provided by the global `Section currentSection`
variable, will be used to associate each node. This `currentSection` variable
must be used to set the `Node.parentSection` property of the subsequent node
that will be entered next.

Note that an explicit reference variable is optional, if an implementation
chooses to maintain an explicit stack of open sections. That is, because the
corresponding reference can always be retrieved from that stack via a call
to `stack.get()`.

<!-- ======================================================================= -->
## list of sections vs. tree of sections

Processing the above fragment according to the default definitions
will result in the following section tree:

```
s0 - s1 - s2 - s3 - s4 -|- s6 - s7
                        |- s8 - s9
```

If the above trace of section sequences is compared to that tree,
the following observations can be made:

A section sequence represents a path in the section tree, that connects the
root section with the current section. That is, the section sequence is just
another rooted path of nodes.

Note that the overall trace of sequences has itself no particular order. That
is, because any sequence may appear multiple times at different positions. In
order to get a specific order, one would have to exclude those repetitions,
which would require a clear definition of when to log a list of sections
(e.g. based on the enter/open events).

**CLARIFICATION**
The list of sections can also be
referred to as "the (current) path of (open) sections".

**CLARIFICATION**
An implementation does not have to maintain an explicit list of sections
because it is always implicitly available via the `currentSection` variable.

Beginning with a reference to the current section, one would just have to
traverse upwards, using the `Section.parentSection` properties, until the
root section is reached. Note however that this traversal will visit those
sections in reversed/bottom-up order.
