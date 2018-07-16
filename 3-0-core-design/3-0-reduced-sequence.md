
<!-- ======================================================================= -->
# Design - reduced node sequence

Associating a single node with a section loosely associates any descendant
of that node (downwards). In addition to that, any node loosely belongs to
any section with which any of its ancestors is associated (upwards). That
is, because a semantically consistent path can be defined which connects a
section with any of its loosely related nodes.

Note that these loose associations will be established automatically by the
structure of the node tree. Because of that, these associations can not be
undefined and they can not be ignored (i.e. they must be taken into account).

Note that, if the above statement would not be true, then there would
consequently be no definition for the term "descendant". That is because the
definition of "descendant" is also based upon the definition of semantically
consistent paths. In addition to that, the term "descendant" is used to define
the term "ancestor".

<!-- ======================================================================= -->
## multiple associations

```
r x ... x (n):s x (x):s x ... x L
                x ... x (y):s x ... x L
                      x ... (z):s x ... x L
```

If some node `n` is strictly associated with section `s`, then any descendant
of `n` is also (loosely) related to `s`.

Consequently, descendants of node `n` do not have to be strictly associated with
section `s`, if the distinction between a "strict" and a "loose" relationship is
not significant. That is, if a loose association is understood to be equivalent
to a strict association.

**CLARIFICATION**
All associations (strict/explicit or loose/implicit) are considered to
be semantically equivalent. From this forward, that equivalence is a
necessity/requirement.

Consequently, any rooted path in this context can be reduced to a path which
ends in a strictly associated node. That is because the remainder of a path,
that passes through such a node, will not change the path's characteristics
(in terms of associations with the given section) any further.

```
r x ... x (x:s)
```

A path that is not supposed to fall into the same category must therefore branch
off from an ancestor of the first strictly associated node. That is, a second
path may branch off beginning with the parent of that node and up until the
first node's top-most relevant ancestor (i.e. the algorithm's root node).

<!-- ======================================================================= -->
## example

`A:s <C:s> D:s E </C:s> F`

Here, node `A` can be understood to represent the first node of section `s`.

The next node, that must be strictly associated with section `s` is node `C`.
That is because unlike with descendant nodes, an association does not carry
over to subsequent siblings. Which is, because based upon the `parent-of`
relation of a tree, no semantically consistent path can be defined that
connects a node with its next sibling.

The loose associations mentioned above also apply to any descendant of node `C`.
Node `E` therefore also belongs to section `s`, whether that node is strictly
associated with it or not. Consequently, section `s` can not end with node `D`
and, because of that, section `s` does not end inside of node `C`.

However, section `s` can intuitively be understood to end with node `C`.
That is because node `F` is unrelated to section `s`.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
No descendant can be excluded from those sections with which its ancestors are
associated. Descendants are implicitly associated with these by the structure
of the node tree.

Any attempt to define a descendant to be unrelated to the sections of its
ancestors is going to be in conflict with the afore mentioned implicit
associations.

**CLARIFICATION**
A section can not end inside of an associated container node.

If a given section would be defined to end inside of an associated container,
then that container could have one or more subsequent descendant nodes, which
are then defined to be unrelated to that section. Consequently, such an attempt
is going to be in conflict with the afore mentioned implicit associations.

**Memory hook**
Strictly associating a single node is equivalent to associating a whole subtree
of nodes. With the root of that subtree being the strictly associated node.

Because of that, a section does not change, if a descendant of an strictly
associated node is itself strictly associated. The strict association merely
transforms the descendant's implicit relationship with that section into an
explicit relationship.

<!-- ======================================================================= -->
## reduced sequence

**CLARIFICATION**
Node `n` must be strictly associated with section `s`, if `n` is intended to
be in relationship with `s`, and if `n` is not already loosely related to it.
That is because `n` would otherwise remain unrelated with regards to `s`.

After all, an algorithm must reflect the relationship of any node with its
sections by establishing strict or loose connections between the sections
of a tree and all of its nodes.

**DEFINITION**
Node `n` will be referred to as a section's top-level node,
if `n` must be strictly associated with it.

Note that no ancestor of a top-level node is strictly or loosely associated
with the corresponding section. If that would not be the case, then that
top-level node would not be one of the section's top-level nodes as it would
already be loosely associated with it.

Note that "top" in the "top-level" term is a reference to "an upper-most
node" and that "level" is with regards to the node's "node level".

Note that a section's first content node always is a top-level node. That is,
because a section's first node never is already loosely associated. In order
to be loosely associated, a node must have a strictly associated presequent
ancestor. Put differently, a section's first node would then not be the first
node of its section.

Note that any node can be a top-level node to multiple sections. That is,
because a node can be subsequent to multiple open presequent sections. Again,
the formal approach requires to associate all nodes with one or more sections.

**CLARIFICATION**
A section can be defined as a sequence of nodes which only contains its
top-level nodes, in the order of the tree's node sequence. As such, a
non-empty section always has a first and a last top-level node.

Any other node, loosely related to that section, can be derived from such a
sequence of top-level nodes. In order to create the node sequence of a section,
all the node sequences of those subtrees, which are defined by the top-level
nodes of a section, would have to be concatenated into a single node sequence.

**DEFINITION**
The sequence of strictly subsequent nodes, which contains all the nodes of
a section, will be referred to as the section's "complete node sequence".

**DEFINITION**
The sequence of nodes, which only contains all the top-level nodes of a
section, will be referred to as the section's "reduced node sequence", or
as the section's "characteristic node sequence".

* A complete sequence is a sequence of strictly subsequent nodes.
* A reduced sequence is not necessarily strictly subsequent.
* The reduced sequence can only be strictly subsequent, if all the
  top-level nodes are leaf nodes. In that case, the reduced sequence
  is even identical to the complete sequence.
* However, the reduced sequence still is a sequence of subsequent nodes.
* If a sequence is created by removing one or more nodes from a reduced
  sequence, then that sequence is insufficient to determine the complete
  sequence of the corresponding section.
* The reduced sequence represents the shortest sequence possible,
  which still allows to determine a section's complete sequence.
* A non-empty section always has exactly one complete
  and exactly one reduced sequence.
* The first node of a reduced sequence is identical to the first
  node. That is because the first node always is a top-level node.
* The last node of a reduced sequence is not necessarily identical
  to the last node of a section. That is because a section's last
  node can be a descendant of its last top-level node.

**CLARIFICATION**
No two non-empty sections within a node tree have identical complete
or even reduced node sequences. These are unique to a section.

That is because no two such sections have identical first nodes and therefore
also different first top-level nodes. Consequently, it does not matter what
other nodes those sections have.

Note however, that a section's complete node sequence may still overlap (i.e.
completely include and/or reach out of) the complete node sequence of another
section. That is, the definitions so far do not include this aspect.

(see also "sectioning nodes")

<!-- ======================================================================= -->
## reduced sequence

The definition of a section's reduced sequence allows to describe the general
pattern of a section. Note that the following description is independent of
any particular sectioning node. That is because the relevant nodes of a
section are its content nodes and because no sectioning node is a content
node of the section it declares.

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
associated with a section. Because of that, a section is a sequence of
strictly subsequent nodes (i.e. no gaps in between two adjacent nodes).

Once the very first node of a section is strictly associated (e.g. `n1`), any
of its descendants are implicitly associated with the same section. The next
node that must be strictly associated therefore is the first node's next
sibling (e.g. `n2`). The next node after that is the next sibling of that node.
Consequently, an algorithm must at first (and at least) strictly associate all
the subsequent siblings of the section's first node.

The next node entered, after the first node's last subsequent sibling was
associated, is the next sibling of the first node's parent node (e.g. `n3`).
Similar to before, any subsequent sibling of that node must be strictly
associated until the parent's last subsequent sibling was associated (e.g.
`n4`).

After that, an algorithm must continue with the next sibling of first node's
next upper ancestor (e.g. `n5`). This process will obviously continue upwards
until the last sibling of the first node's top-most ancestor was associated.
And because the root node has no sibling, the last relevant ancestor of the
first node is one of the root's child nodes.

To be more clear: Ancestors will be skipped, if they have no next sibling.
The last relevant ancestor therefore is the top-most ancestor that has a
next sibling.

**CLARIFICATION**
A reduced sequence is a sequence of top-level nodes that, except for the
first node itself, are siblings to the first node, or siblings to any of
the first node's ancestors.

In addition to that, the reduced sequence begins with the section's first node,
which is then followed by its siblings. These siblings are then followed by the
siblings of the first node's parent. After that, the sequence continues with the
siblings of the first node's next upper ancestor until it finally ends with the
siblings of the last relevant ancestor.

**CLARIFICATION**
A reduced sequence contains subsequences of subsequent siblings. All the nodes
of a particular subsequence have the same parent. In addition to that, the
parent of a subsequent subsequence is an ancestor of the parent of a presequent
subsequence.

Note that a next sibling is not necessarily strictly subsequent to its previous
sibling. That is because the previous sibling could have child nodes. Hence,
"subsequences of subsequent siblings" and not "of strictly subsequent siblings".

**Memory hook**
A reduced sequence, and therefore even a section, can loosely be described as
"a sequence of siblings".

Note that, in an ordered tree of nodes, the context of a node has vaguely
similar characteristics. That is, if the ancestors of a node are ignored and
if the nodes are ordered according to the distance they have with regards to
the current node.

<!-- ======================================================================= -->
## associate nodes while entering

**CLARIFICATION**
An implementation can easily store a reference to the node that was
associated first and a reference to the node that was associated last:

```
Section.associate(Node node) begin
  //- reference to the first node
  if(this.firstNode === null) begin
    this.firstNode = node
  end

  //- reference to the last node
  //- i.e. override the current last node
  this.lastNode = node
end
```

Note that this code fragment is independent of which type of sectioning
node was used to create and initialize the corresponding section object.

**CLARIFICATION**
All nodes must be associated while they are being entered.

As mentioned before, associating any nodes while they are being exited is in
principle in conflict with the node order of the tree. In addition to that,
the event that is used to associate nodes has a significant impact on the
detection of a section's first and last nodes:

```
<n1> <n2> <n3> </n1>
```

Assumed, that node `n1` would be defined to be a section's first node. Which
effects would it have, if nodes were associated while they are being entered?
(e.g. Is the first node of a section going to be associated first)? What can
be said, if `n1` would be a section's last top-level node (e.g. Is the last
node of a section going to be associated last)?

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
last. Put differently, and with that order of association in mind, a section's
first and last nodes can not be consistently detected. The nodes associated
first and last can turn out to be false positives. However, the last node
associated is guaranteed to be the section's last top-level node.

In contrary to that, associating nodes while entering them guarantees that a
section's first node will be associated first and that a section's last node
will be associated last. In addition to that, the first node associated is
also guaranteed to be the section's first top-level node. However, the last
node associated is *not*  guaranteed to be the section's last top-level node.

<!-- ======================================================================= -->
## reduced sequence

Not all the nodes of a section are relevant to support transformations (dynamic
support needs to be able to execute transformations). That is because only
the top-level nodes of a section are needed to group the contents of a section.
Each subsequence in a section's reduced sequence of nodes can be grouped by
placing its nodes inside of a container. Because of that, a section can be
transformed into a sequence of such container nodes.

Note that, without any restriction in scope, and because the ancestors of a
section's first node do not belong to the same section, a section can not be
grouped into a single container. It is therefore still not possible to
transform a type-2 section into a semantically equivalent type-1 section.

```
r x ak x ... x a2 x a1 x n1:s
                  x n2:s
                  x n3:s
                  x n4:s
             x n5:s
```

The basic approach to determine all the top-level nodes of a section is
to start with a node that is associated with a given section. This initial
node then allows to determine the first top-level node (e.g. `n3`). That is,
because the initial node is a descendant of that first top-level node, which
(by definition) is the top-most ancestor that belongs to the same section.

Next, an algorithm would have to detect all those siblings that are subsequent
to `n3` (e.g. `n4`, `n5`). This process is straight forward, as one would only
have to traverse from one sibling to another and, if there is no next sibling,
continue with the next upper relevant ancestor (e.g. `a2`).

After that, an algorithm would have to detect all those siblings that are
presequent to `n3` (e.g. `n2`, `n1`). With regards to the siblings of `n3`,
that belong to the same section, this step is at first also straight forward.
However, things are no longer straight forward, if the previous sibling does
not belong to the same section: (1) If there is no previous sibling, then the
last previous sibling's parent could be a type-1 sectioning node. (2) If the
previous sibling does not belong to the same section, it could be a type-2
sectioning node, or (3) the algorithm needs to continue with the last child
of an unassociated sibling.

Obviously, this approach requires the ability to reliably determine if a node
is related to a given section, regardless whether that node strictly belongs to
one of the section's subsections or not (hint: associate with one section only).

<!-- ======================================================================= -->
## conclusions

(1) Only the top-level nodes of a section are needed to support transformations.
It is not required to have knowledge of all the nodes of a section. If needed,
this information can be regained by traversing the top-level nodes.

(2) It is preferable, if an algorithm could start directly with a top-level
node. That is because the search for the initial top-level node would then be
a non-issue. Each section object should therefore hold one or more references
to a section's top-level nodes.

(3) It is almost straight forward to traverse the top-level nodes of a section
away from a section's first top-level node in the direction of a section's last
top-level node. Because of that, it is preferable to begin with a section's
first (top-level) node (hint: associate all nodes while entering).

**CLARIFICATION**
A section object does not have to store any reference to any of the section's
nodes. That is because a section's first node always is a top-level node, and
because the first node of a section can be determined from the section's type.

Note that, in order to allow sections to not store any node references at all,
the definition of a sectioning node must allow to easily and unambiguously
determine the first node of a section (hint: a strict type-2 definition).

However, in order to avoid having to distinguish between the different types
of sections, a section object should at least hold a reference to a section's
first (top-level) node.

**CLARIFICATION**
The first node of a section is critical to efficient transformations.
