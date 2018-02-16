
<!-- ======================================================================= -->
# Design (8) - fundamental considerations

At any given point in time, one or more sections count as being open. This set
of open sections will be referred to as the current set of open sections (`cs`
for "current-set").

* `cs := { s0, s1, s2, ... }` and `(cs subset-of S)`
* `S` contains all declared/known sections

If the node sequence of the tree and the sectioning nodes of all open sections
are taken into account, then that set of sections can be understood to define
the current ordered list of open sections (`cl` for "current-list").

* `cl := [ s0, s1, s2, ... ]`
* `(si subsection-of si-k)` for `si in cl` and any `k in [1,i)`
* `(si declared-by ni)` for any `si in cs`
* `(ni subsequent-to ni-k)` for any `k in [1,i)`

**CLARIFICATION**
The current set of open sections will be referred to as "the set of (open)
sections" and the current ordered list of sections as "the list of (open)
sections" or "the sequence of (open) sections".

Note that this list does by itself not represent an existing list object. It
merely represents an ordered listing of sections that, at a given point in
time, still count as being open. That is, this list can be understood as the
result of a lookup operation.

Note that this lookup operation is completely based upon those nodes that have
already been visited (i.e. presequent nodes). That is, an implementation could
maintain such a listing while it is traversing the node tree. However, the
corresponding list object must, at all times, accurately represent the list
of sections.

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
* other descendant nodes will/can be ignored
* nodes `n1-9` represent type-2 sectioning nodes
* nodes `n1-9` declare sections `s1-9`
* obviously, section `s9` will always be empty

If, for example, an implementation would enter node `n5`,
then the list of sections will be the sequence `(s0,s1,s2,s3,s4)`.

When creating/opening section `s5`, that list will change into the sequence
`(s0,s1,s2,s3,s4,s5)`. Which is, because no open presequent section will be
closed (i.e. `s5` is a subsection to `s4`).

**case 2:** `(s0,s1,s2,s3,s4,s6) => -{s6} => (s0,s1,s2,s3,s4)`

```
            n0
==========================
n1 n2 n3 n4 n5    n7 n8 n9
            -----
               n6
```

* `n5` is an inactive parent node
* `n6` is a child node of `n5`

If, for example, an implementation would exit node `n6` (i.e. after opening
`s6`), then that list of sections is equivalent to `(s0,s1,s2,s3,s4,s6)`
(`s5` does not exist because `n5` is no longer a sectioning node).

The next node event that will have to be processed is the exit event of `n5`.
And because `n5` acts as the parent container of `s6`, `s6` has to be closed
during `n5`'s exit event. Consequently, the list of sections will no longer
contain `s6`: `(s0,s1,s2,s3,s4)`.

**case 3:** `(s0,s1,s2,s3,s4,s6,s7) => -{s6,s7} => (s0,s1,s2,s3,s4)`

```
            n0
==========================
n1 n2 n3 n4 n5       n8 n9
            --------
               n6 n7
```

* `n5` is an inactive parent node
* `n6, n7` are both child nodes of `n6`

In contrary to the previous case, `n5` now has two inner sections (i.e. `s6`
and `s7`). Consequently, when exiting `n7` after opening `s7`, the list of
sections is `(s0,s1,s2,s3,s4,s6,s7)` (`s5` does not exist because `n5` is
no longer a sectioning node).

As before, the exit event of `n5` has to close all remaining open inner
sections. Consequently, and after `n5`'s exit event, the list of sections
will be `(s0,s1,s2,s3,s4)`.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The list of sections will be extended by a new section, if the next node event
results in opening a new section. However, that new section will always appear
at the end of the list (i.e. not an arbitrary position).

That is, because the new section will be a subsection to all sections in the
previous listing (formal perspective).

Note that any sectioning node can only declare a single new section. That is,
no node event will extend the list of sections by more than one section.

**CLARIFICATION**
The list of sections will be reduced by one or more sections, if the next
node event results in closing the corresponding sections. Note that all of
these sections will always be removed from the end of the list (i.e. not
from an arbitrary position).

That is, because no subsection can remain open if its parent section has to
be closed. Note that this is a mere consequence of "the parent container of
a subsection never is an ancestor of its parent section's parent container".

**CLARIFICATION**
If multiple sections need to be closed during the same node event, then those
sections need to be closed in reverse order. That is, if `s6` was opened before
`s7`, then `s7` needs to be closed before `s6` is closed.

That is, because `s7` is a subsection to `s6` and because no subsection can
remain open if its parent section has to be closed. Put differently, any other
close order would be in conflict with "a parent section is open for as long as
its subsections are open".

Note that it might not seem that relevant in which order sections are closed.
That is, if they need to be closed during the same node event. However, the
order of close events can also be relevant, if those operations are used to
trigger event handler routines.

Note that an implementation might initially not be aware of how many inner
sections need to be closed when exiting a given parent container. In addition
to that, an implementation might even not have to be aware of the exact number
(e.g. repeat to close the last subsection until a certain condition is met).

**CLARIFICATION**
The behavior of the list of open sections is consistent with the
operations of a first-in-first-out data structure (aka. stack).

1) `push()` a new section onto the stack
2) `pop()` the last subsection from the stack
3) `get()` the last subsection from the stack

**CLARIFICATION**
The list of open sections can also be
referred to as the "stack of (open) sections.

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

```
list of sections:       -  phase of processing:
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

Note that it does not really matter, if `n0` is a type-1 sectioning node, or
an inactive parent container. If `n0` would be such a container node, then `s0`
would represent the section that was used to associate `n0`. Consequently, `s0`
would not have to be created when entering and closed when exiting `n0`. Other
than that, all sequences of sections would begin with some common prefix, which
would end with `s0`.

```
                        |- s6 - s7
s0 - s1 - s2 - s3 - s4 -|
                        |- s8 - s9
```
