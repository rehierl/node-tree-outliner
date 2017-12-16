
<!-- ======================================================================= -->
# Design (3)

Associating a single node with a section also loosely associates any descendant
of that node (downwards). In addition to that, any node loosely belongs to any
section with which any of its ancestors is associated (upwards).

That is, because a semantically consistent path can be defined which connects a
section with any of the associated node's descendants.

Note that these loose associations are established automatically by the
structure of a tree. Because of that, these associations can not be undefined
and they can not be ignored (i.e. they must be taken into account).

Note that, if the above statement would not be true, then there would
consequently be no definition for the term "descendant". That is, because the
definition of "descendant" is also based upon the construction of a semantically
consistent path. In addition to that, the term "descendant" is used to define
the term "ancestor".

**NEXT OPEN QUESTIONS**
(1) What happens, if other nodes are associated with the same section?
(2) What are the consequences with regards to a section's last node?

<!-- ======================================================================= -->
## multiple associations

```
r x ... x (n):s x (x):s x ... x L
                x ... x (y):s x ... x L
                      x ... (z):s x ... x L
```

If some node `n` is strictly associated with section `s`, then any descendant
of `n` is already loosely related to `s`.

Consequently, descendants of node `n` do not have to be strictly associated with
section `s`, if the distinction between a "strict" and a "loose" relationship is
not relevant. That is, if a loose association can be seen to be equal to a
strict association.

**CLARIFICATION**
From this point on, all associations (strict/explicit or loose/implicit) are
considered to be semantically equivalent. Because of that, this equality is
itself a necessity/requirement.

Consequently, any rooted path in this context can be reduced to a path which
ends with a strictly associated node. That is, because the remainder of a path,
that passes through such a node, will not change the path's characteristics any
further.

```
r x ... x (x:s)
```

A path that is not supposed to fall into the same category must therfore branch
off from an ancestor of the first associated node. That is, a second path may
branch off beginning with the parent of an associated node and up until the
first node's top-most relevant ancestor.

<!-- ======================================================================= -->
## example fragment

`A:s <C:s> D:s E </C:s> F`

In this fragment, node `A` can be understood to represent the first node of
section `s`.

The next node, that must be strictly associated with section `s` is node `C`.
Unlike with descendant nodes, an association does not carry over to a subsequent
sibling. That is, because, based upon the underlying relation, no semantically
consistent path can be defined which connects a node with its next sibling
(i.e. a node does not contain its siblings).

The loose associations mentioned above also apply to any descendant of node `C`.
Node `E` therefore also belongs to section `s`, whether that node is strictly
associated with it or not. Consequently, section `s` can not end with node `D`
and, because of that, inside of node `C`.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
No descendant of an associated node can be excluded from the sections of its
ancestors. Descendants are implicitly associated with these by the structure
of the node tree.

Any attempt to define a descendant to be unrelated to the sections of its
ancestors is going to be in conflict with the afore mentioned implicit
associations.

**CLARIFICATION**
A section can not end inside of an associated container.

If a given section would be defined to end inside of an associated container,
then that container would have subsequent descendant nodes, which are then
defined to be unrelated to that section. Consequently, such an attempt is going
to produce a conflict, because any descendant of an associated container loosely
belongs to all of the container's sections.

**Memory hook**
Strictly associating a single node is equivalent to associating a whole subtree
of nodes. The root of that subtree is the strictly associated node.

Because of that, a section does not change, if a descendant of a strictly
associated node is itself strictly associated. The strict association merely
transforms the descendant's implicit relationship with that section into an
explicit relationship.

<!-- ======================================================================= -->
## reduced sequence (1)

**CLARIFICATION**
Node `n` must be strictly associated with section `s`, if `n` is intended
to be in relationship with `s`, and if `n` is not already loosely related
to it (`n` would otherwise remain unrelated to `s`).

After all, an algorithm must reflect the relationship of any node with the
node's sections by establishing connections between the sections of a tree
and all of its nodes.

**DEFINITION**
Node `n` will be referred to as a section's top-level node,
if `n` must be strictly associated with it.

**CLARIFICATION**
A section can be defined by a sequence of nodes which only contains the
top-level nodes of a section, in the order of the tree's node sequence.
Any other node, which is related to that section, can be derived from the
section's sequence of top-level nodes.

In order to create the node sequence of a section, all the node sequences
of the section's top-level nodes would have to be concatenated into a single
sequence of nodes.

**DEFINITION**
The sequence of strictly subsequent nodes, which contains all the nodes of
a section, will be referred to as the section's complete node sequence.

**DEFINITION**
The sequence of nodes, which only contains all the top-level nodes of a
section, will be referred to as the section's reduced, or as the section's
characteristic node sequence.

* A complete sequence is a sequence of strictly subsequent nodes.
* A reduced sequence is not necessarily strictly subsequent.
* The reduced sequence can only be strictly subsequent, if all the
  top-level nodes are leaf nodes. In that case, the reduced sequence
  is also identical to the complete sequence.
* The reduced sequence will always be a sequence of subsequent nodes.
* If a sequence is created by removing one or more nodes from a
  reduced sequence, then that sequence is insufficient to determine
  the section's complete sequence.
* The reduced sequence represents the shortest sequence possible
  that still allows to determine the complete sequence.
* A non-empty section has exactly one complete
  and exactly one reduced sequence.
* The first node of a reduced sequence is identical to the first
  node. That is, because the first node always is a top-level node.
* The last node of a reduced sequence is not necessarily identical
  to the last node of a section. That is, because the last node can
  be a descendant of the last top-level node.

<!-- ======================================================================= -->
## reduced sequence (2)

The definition of a section's reduced sequence allows to describe the general
characteristics of a section independent of any particular sectioning node:

```
r x ak x ... x a2 x a1 x n1:s
                       x n2:s
                  x n3:s
                  x n4:s
             x n5:s
       x ... x
  x nl:s

//- this section's reduced sequence:
rs := [n1, n2, n3, n4, n5, ..., nl]
```

In between a section's open and close events, any subsequent node must be
associated with a section. Because of that, a section is a sequence of strictly
subsequent nodes (i.e. no gaps in between any two adjacent nodes).

Once the very first node of a section is strictly associated (e.g. `n1`), any
of its descendants are implicitly associated with the same section. If the
section did not end with this first node, then the next node that must be
strictly associated is the first node's next sibling (e.g. `n2`). The next node
after that is the next sibling of that node. Consequently, and for as long as
a section does not end, an algorithm must at least strictly associate all the
subsequent siblings of the section's first node.

The next node entered, after the first node's last subsequent sibling was
associated, is the next sibling of the first node's parent node (e.g. `n3`).
Similar to before, any subsequent sibling of that node must be strictly
associated until the parent's last subsequent sibling is associated (e.g. `n4`).

Consequently, and unless a section must be closed, an algorithm must continue
with the next sibling of first node's next upper ancestor (e.g. `n5`).

By now it should be obvious, that this process continues until the last sibling
of the first node's top-most ancestor was associated. And because the root node
has no sibling, the last relevant ancestor of the first node is one of the
root's child nodes.

To be more clear, ancestors are skipped if they have no next sibling. The
actual last relevant ancestor therefore is the top-most ancestor for which
a next sibling exists.

**CLARIFICATION**
The reduced sequence of a section is a sequence of top-level nodes that, except
for the first node itself, are siblings to the first node, or siblings to any of
the first node's ancestors.

In addition to that, the reduced sequence begins with the section's first node,
followed by its siblings, which are then followed by the siblings of the first
node's parent. After that, the sequence continues with the siblings of the first
node's next upper ancestor until it finally ends with the siblings of the last
relevant ancestor.

**Memory hook**
The reduced sequence of a section, or even a section itself, could simply be
referred to as "a sequence of siblings".

<!-- ======================================================================= -->
## associate nodes while entering

As mentioned before, associating any nodes while they are being exited is in
principle in conflict with the node order of a tree. In addition to that, the
event that is used to associate nodes has a significant effect on the detection
of a section's first and last nodes.

Recall that the first node of a section is, by definition, identical to its
first top-level node. In contrary to that, the last node of a section is not
necessarily identical to its last top-level node.

```
<n1><n2> <n3/> <n4/> </n2></n1>
```

Assumed, that node `n1` would be defined as a section's first node. Which
effects would it have, if nodes were associated while they are being entered?
(e.g. Is the first node of a section going to be associated first)? Which
effects would it have, if `n1` would be defined as a section's last top-level
node (e.g. Is the last node of a section going to be associated last)?

```
                         | entering | exiting
-------------------------|----------|--------
first (/top-level) node  |   1/1    |   0/0
-------------------------|----------|--------
last (/top-level) node   |   1/0    |   0/1
```

(A) first associated node + while entering:
(1) Guaranteed to be the section's first node and
(2) guaranteed to be the section's first top-level node
(=> `1/1`).

(C) first associated node + while exiting:
(1) Not necessarily the section's first node and
(2) not necessarily the section's first top-level node
(=> `0/0`).

(B) last associated node + while entering:
(1) Guaranteed to be the section's last node, but
(2) not necessarily the section's last top-level node
(=> `1/0`).

(D) last associated node + while exiting:
(1) Not necessarily the section's last node, but
(2) guaranteed to be the section's last top-level node
(=> `0/1`).

Associating nodes while exiting them neither guarantees that a section's first
node will be associated first, nor that a section's last node will be associated
last. Put differently, and with that order of association, a section's first and
last nodes can not be consistently determined. The nodes associated first and
last can turn out to be false positives. However, the last node associated is
guaranteed to be the section's last top-level node.

In contrary to that, associating nodes while entering them guarantees that a
section's first node will be associated first and that a section's last node
will be associated last.

**CLARIFICATION**
All nodes must be associated while they are being entered.

<!-- ======================================================================= -->
## reduced sequence (3)

```
r x ak x ... x a2 x a1 x n1:s
                       x n2:s
                  x n3:s
                  x n4:s
             x n5:s
       x ... x
  x nl:s

//- this section's reduced sequence:
rs := [n1, n2, n3, n4, n5, ..., nl]
```

In order to allow dynamic support, it is necessary to provide an algorithm with
the means to efficiently traverse the top-level nodes of a section.

Associating nodes while they are being exited therefore adds additional efforts
to the traversal of a section: One would always first have to detect the first
or the last top-level node.

In contrary to that, and because the first node of a section is guaranteed to
be a top-level node, if all the nodes of a section are associated while they are
being entered, that first step is a none-issue, if an algorithm can start with
a section's first node.

### beginning with a section's last node

### beginning with a section's first node

If an algorithm would have to begin with a section's last node.

**CLARIFICATION**
The first node of a sequence is critical to the traversal of a section.
