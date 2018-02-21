
<!-- ======================================================================= -->
# Design (8) - current section

At any given point in time, one or more sections always count as being open.
This set of open sections will be referred to as the current set of open
sections (`cs` for "current-set").

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
result of an implicit lookup operation.

Note that this lookup operation is completely based upon those nodes that have
already been visited (i.e. presequent nodes). That is, an implementation could
maintain such a listing while it is traversing the node tree. However, that list
object must accurately represent the list of sections.

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

If an implementation would begin to enter `n5`, then
the list of sections will be the sequence `(s0,s1,s2,s3,s4)`.

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
* `n6` is a child node to `n5`

If an implementation would exit `n6` (i.e. after opening `s6`), then that
list of sections would be equivalent to the sequence `(s0,s1,s2,s3,s4,s6)`
(`s5` does not exist because `n5` is no longer a sectioning node).

The next node event that will have to be processed is the exit event of `n5`.
And because `n5` acts as the parent container of `s6`, `s6` has to be closed
during that event. Consequently, the list of sections will no longer contain
`s6`, which is why the sequence will change into `(s0,s1,s2,s3,s4)`.

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
and `s7`). Consequently, when exiting `n7` after opening `s7`, the list of
sections is `(s0,s1,s2,s3,s4,s6,s7)` (`s5` does not exist because `n5` is
no longer a sectioning node).

Similar as before, the exit event of `n5` has to close all remaining open
inner sections. Consequently, and after `n5`'s exit event, the list of
sections will be `(s0,s1,s2,s3,s4)`.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The list of sections will be extended by a new section,
if the next node event results in opening a new section.

Note that the new section will always appear at the end of the list (i.e.
not at some arbitrary position). That is, because the new section will be
a subsection to all sections in the previous listing (formal perspective).

Note that any sectioning node can only declare a single new section. That is,
no node event will extend the list of sections by more than one section.

**CLARIFICATION**
The list of sections will be reduced by one or more sections,
if the next node event results in closing these sections.

Note that all of these sections will always be removed from the end of the
list (i.e. not from an arbitrary position). That is, because no subsection
can remain open if its parent section has to be closed.

**CLARIFICATION**
If multiple sections need to be closed during the same node event, then those
sections need to be closed in reverse order. That is, if `s6` was opened before
`s7`, then `s7` needs to be closed before `s6` can be closed.

That is, because `s7` is a subsection to `s6` and because no subsection can
remain open if its parent section has to be closed. Put differently, any other
close order would be in conflict with "a parent section is open for as long as
its subsections are open".

Note that it might not seem to be relevant in which order sections are closed.
After all, they need to be closed during the same node event. However, the
close order can be relevant, if those operations are used to trigger event
handler routines.

Note that an implementation might initially not be aware of how many inner
sections need to be closed when exiting a given parent container. In addition
to that, an implementation might even not have to be aware of the exact number
(e.g. repeat to close the last subsection until some condition is met).

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

Logging the list of sections at certain points in time, while the
above fragment is being processed, could result in the following
trace of lists/sequences:

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
the list. That is, because any other section is a subsection to it.

As mentioned before, and in contrary to the formal perspective, each node
will be associated with one section only (practical perspective). However,
this single association does, based on implicit associations, represent all
formal associations (i.e. both perspectives are equivalent). And, because
of that, each node must be associated with the closest presequent section
that still counts as being open (i.e. the node's parent section).

Note that the parent section of any node always is located at the end of
the list. That is, when being entered, a node will be associated with the
last/top-most section of that list/stack.

Note that it does not really matter, if `n0` is a type-1 sectioning node, or
an inactive parent container. If `n0` would be such a container node, then
`s0` would represent the section that was used to associate `n0`. Consequently,
`s0` would not have to be created when entering, and closed when exiting `n0`.
In addition to that, all sequences of sections would begin with some common
prefix, which always ends with `s0`.

**CLARIFICATION**
The last/top-most section in the list/stack of open sections will be referred
to as the "current section". A reference to this section, provided by the
global `Section currentSection` variable, will be used to associate each node.

Note that an explicit reference variable is optional, if an implementation
chooses to maintain an explicit stack of open sections. That is, because the
corresponding reference can always be retrieved from that stack via a call
to `stack.get()`.

<!-- ======================================================================= -->
## compared with the tree of sections

Processing the above fragment will, according to the default
definitions, result in the following tree of sections:

```
s0 - s1 - s2 - s3 - s4 -|- s6 - s7
                        |- s8 - s9
```

If the above trace of section sequences is compared to that tree, then
the following observation can be made right away:

A section sequence represents a path in the tree of sections, which connects
the root section with the current section (i.e. just another rooted path of
nodes/sections).

Note that the overall trace of lists has itself no particular order. That
is, because any sequence may appear multiple times at different positions.
In order to get a specific order, one would have to exclude those repetitions,
which would require a clear definition of when to print a list of sections
(e.g. based on the enter/open events).

**CLARIFICATION**
The list of sections can also be
referred to as "the (current) path of (open) sections.

**CLARIFICATION**
An implementation does not have to maintain an explicit list of sections
because it is always implicitly available via the `currentSection` variable.

Beginning with a reference to the current section, one would just have to
traverse upwards, using the `Section.parentSection` references, until the
root section is reached. However, this traversal will visit those sections
in reversed/bottom-up order.

**CLARIFICATION**
The node order of the section tree is defined by the node order of the node
tree. In addition to that, the section tree will be created in the order in
which its sections will be entered during the traversal of the section tree.

That is, because due to the node order of the node tree, all parent sections
will be entered/created/opened before any subsection is entered. In addition
to that, the sectioning nodes of sibling sections are entered according to the
node order of the node tree (i.e. in the sequence in which they appear in the
node sequence, which is based upon the node order of the node tree).

Note that not any tree data structure is suited to represent the tree of
sections. That is, because an AVL tree, for example, will repeatedly trigger
balancing operations, if entries are added in an orderly fashion (e.g. in
ascending order). Consequently, a list-based data structure would be more
appropriate.

<!-- ======================================================================= -->
## outline depth/height

**CLARIFICATION**
The outline depth of a section is "1 + the number of its ancestor sections"
(not counting the universal section). That is, starting with an outline depth
value of 1, the higher the value is, the deeper within the section hierarchy
a section is located.

That is, the root section has an outline depth of 1, its child sections an
outline depth of 2, and their child sections an outline depth of 3.

In other words, the outline depth of a section is the length (in terms of the
number of sections involved) of the rooted path of sections that ends in the
corresponding section. Note the edge case of a rooted path of length 1 (e.g.
root section).

Note that the node level of a node is defined as "1 + the number of edges in
between the node and the tree's root" (In short: "1 + the number of ancestors
that a node has").

Note that the term "outline depth" is, in the context of a section tree,
synonymous to "node level".

**CLARIFICATION**
The outline depth of a node is the outline depth of its unique parent section
("unique" due to multiple associations).

Note that the outline depth of the root node is 0. That is, because the root
node is associated with the universal section, which the above definition does
not count. Consequently, the outline depth of an unassociated node is 0.

**CLARIFICATION**
The outline height of a section tree is the outline height of its root section.
The outline height of a section is the the distance to its furthest descendant
(i.e. a leaf section). That is, the most amount of jumps/edges between that
leaf and the corresponding section.

That is, the height of a leaf section is 0. The height of a section which only
has a single child section is 1. The height of a section that only has such a
subtree (i.e. a child section that itself only has one child section) is 2.

Note that, similar as above and in the context of a section tree, the term
"outline height of a section" is synonymous to the "height of a node".

Note that a node can not have an "outline height". That is, because a node
does in general not have any descendant sections (Although declared sections
could be seen to be descendant to their sectioning nodes; i.e. "descendant"
with regards to "subordinate").

<!-- ======================================================================= -->
## height map

```
            n0
==========================
n1 n2                n8 n9
   -----------------
      n3 n4       n7
         --------
            n5 n6
```

* `n0` is a type-1 sectioning node
* `n2,n4` are inactive parent containers
* `n1,n3,n5-6,n7,n8-9` are type-2 sectioning nodes
* `s6,s7,s9` are empty sections

Processing this fragment will, according to the default
definitions, result in the following tree of sections:

```
s0 - s1 -|- s3 -|- s5 - s6
         |      |- s7
         |
         |- s8 - s9
```

The associations of the tree's nodes with these sections are as follows:

```
y-axis
  ^
4 |                   ==            - s5
3 |             ===========    ==   - s3, s8
2 |       =======================   - s1
1 |    ==========================   - s0
  --------------------------------> x-axis
    n0 n1 n2 n3 n4 n5 n6 n7 n8 n9
```

Note that the x-axis represents the corresponding node (e.g. via its index
within the node sequence) and the y-axis the outline depth of that node.

As such, the outline depth can be understood to shift a node into the next
dimension by associating a height value with it. That is, the outline depth
allows to turn a one-dimensional (short: 1-dim) listing (i.e. the node
sequence) into a 2-dim graph, which can be referred to as the tree's 2-dim
height map.

Similar to that, and if the nodes of a node tree are drawn onto a flat
2-dim surface, the outline depth can be used to shift the nodes into the
3rd dimension. What results can be seen to represent the 3-dim height map
of the corresponding node tree.

Another way to display the outline depth, and thus allow to visualize the
associations, could be to indent the textual definition of the node tree
by the display of a border:

```
outline depth      node tree
 1 2 3 4
================   ================
                   <n0>
 |                   <n1/>
 | |                 <n2>
 | |                   <n3/>
 | | |                 <n4>
 | | |                   <n5/>
 | | | |                 <n6/>
 | | |                 </n4>
 | | |                 <n7/>
 | |                 </n2>
 | |                 <n8/>
 | | |               <n9/>
                   </n0>
```

**Memory hook**
The outline depth is similar to stacking wood planks:
The greater the value, the smaller the length.
