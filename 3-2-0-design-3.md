
<!-- ======================================================================= -->
# Multiple associations

As mentioned before, associating a single node with a section also loosely
associates any descendant of that node. In addition to that, any node loosely
belongs to any section with which any of its ancestors is associated.

The questions, that now need to be answered next, are:

* What happens, if other nodes are associated with the same section?
* What are the consequences with regards to a section's last node?

<!-- ======================================================================= -->
## multiple associations (1)

```
r x ... x (n):s x (x):s x ... x L
                x ... x (y):s x ... x L
                      x ... (z):s x ... x L
```

If some node `n` is strictly associated with section `s`, then any descendant
of `n` is already loosely related to `s`.

Consequently, descendants of node `n` do not have to be strictly associated with
section `s`, if the distinction between a "strict" and a "loose" relationship is
not relevant. That is, if a loose association can be seen to be equal to a strict
association.

From this point on, all associations (strict/explicit or loose/implicit) are
considered to be semantically equivalent. Because of that, this perspective
is a necessity.

Because of that, any rooted path in this context can be reduced to a path which
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
sibling. That is, because no semantically consistent path can be defined on top
of the underlying relation, which connects a node with its next sibling.

The loose associations mentioned above also apply to any descendant of node `C`.
Node `E` therefore also belongs to section `s`, whether that node is strictly
associated with it or not.

<!-- ======================================================================= -->
## derived statements

**Memory hook**
Strictly associating a single node is equivalent to associating a whole
subtree of nodes. The root of that subtree is the strictly associated node.

Because of that, a section does not change, if a descendant of a strictly
associated node is itself strictly associated. The strict association merely
transforms the descendant's implicit relationship with that section into an
explicit relationship.

**CLARIFICATION**
Node `n` must be strictly associated with section `s`, if `n` is intended to
be in relationship with `s`, and if `n` is not already have a loosely related
to it (`n` would otherwise remain unrelated to `s`).

In the end, the algorithm's resulting structure of sections must reflect the
relationship of any node with its sections by establishing connections between
the tree's sections and all of its nodes.

**DEFINITION**
Node `n` will be referred to as a section's top-level node, if
`n` must be strictly associated with it.

**CLARIFICATION**
Any section is defined by a sequence of nodes which only contains the
section's top-level nodes (in the order of the tree's node sequence).
Any other node, which is related to that section, can be derived from
such a node sequence.

**DEFINITION**
The sequence of strictly subsequent nodes, which contains all the nodes of a
section, will be referred to as the section's complete node sequence (`cs`).
The sequence of nodes, which only contains all the top-level nodes of a
section, will be referred to as the section's reduced (`rs`), or as the
section's characteristic node sequence.

* A complete sequence is a sequence of strictly subsequent nodes.
* A reduced sequence is not necessarily strictly subsequent.
* The reduced sequence can only be strictly subsequent, if all the
  top-level nodes are leaf nodes. In that case, the reduced sequence
  is even identical to the complete sequence.
* The reduced sequence will always be a sequence of subsequent nodes.
* If a sequence is created by removing one or more nodes from
  a reduced sequence, then that sequence is insufficient to
  determine the section's complete sequence.
* The reduced sequence represents the shortest sequence possible
  that still allows to determine the complete sequence.
* A non-empty section has exactly one complete
  and exactly one reduced sequence.
* The first node of a reduced sequence is identical to the section's
  first node. The last node of a reduced sequence is not necessarily
  identical to the section's last node.

**TODO**
a section's reduced sequence allows transformations -
how to determine the top-level nodes of a section

**TODO**
complete and reduced sequences are unique to their section -
no other section has the exact same sequences -
depends on the definitions of sectioning nodes

<!-- ======================================================================= -->
## multiple associations (2)

The definition of a section's reduced node sequence allows to clarify
the general characteristics of a section independent of any particular
sectioning node:

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

Recall that, in between a section's open and closed states, any subsequent node
must be associated with said section. Because of that, a section is a sequence
of strictly subsequent nodes (i.e. no gaps in between any two adjacent nodes).

Once the very first node of a section is strictly associated (e.g. `n1`), any
of its descendants are implicitly associated with the same section. If the
section did not end with that node, then the next node that must be strictly
associated is the first node's next sibling (e.g. `n2`). The next node after
that then is the next sibling of that node. Consequently, and for as long as
a section does not end, an algorithm must at least strictly associate all the
subsequent siblings of the section's first node.

The next node entered, after the first node's last subsequent sibling was
associated, is the next sibling of the first node's parent node (e.g. `n3`).
Similar as before, any subsequent sibling of that node must be strictly
associated until the parent's last subsequent sibling is associated (e.g. `n4`).

Consequently, and unless a section must be closed, an algorithm must continue
with the next sibling of first node's next ancestor (e.g. `n5`).

By now it should be obvious, that this process must be continued until the last
sibling of the first node's top-most ancestor was associated. And because the
root node has no sibling, the last relevant ancestor of the first node is one
of the root's child nodes. To be more clear, ancestors are skipped if they have
no next sibling. The actual last relevant ancestor therefore is the top-most
ancestor for which a next sibling exists.

**CLARIFICATION**
The reduced sequence of a section is a sequence of top-level nodes that all are
subsequent siblings to a section's first node, or to any of its ancestors.

In addition to that, the reduced sequence is ordered such that it begins with
the siblings of the first node, followed by the siblings of its parent. After
these, the sequence contains the siblings of the first node's ancestors until
it ends with the siblings of the last relevant ancestor.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
No descendant of an associated node can be excluded from the sections of its
ancestors. Descendants are implicitly associated by the tree's structure.

Any attempt to define a descendant to be unrelated to the sections of its
ancestors is going to be in conflict with the afore mentioned implicit loose
associations.

**CLARIFICATION**
Unlike with a section's first node, it is in general not possible
to clearly identify a section's last node. Obviously, the same also
applies to the relationship between a section's first and last node.

That is, because any associated node can have any number of descendant nodes.
It is therefore not possible, from a definition's point of view, to clearly
identify a section's last node without forcing a certain structure upon the
nodes of a section.

**CLARIFICATION**
A non-empty section can always be seen to end with its last top-level node.
If this top-level node has any descendants, then the section's last node is
the last subsequent descendant of this top-level node.

With that in mind, a section can also be seen to end inside of an associated
container, if the last subsequent descendant of that container (e.g. node `E`)
is the section's last node. However, this perspective could be misleading,
because a section can only end with the very last subsequent descendant
(i.e. not some randomly selected descendant).

**CLARIFICATION**
The last node of a non-empty section will always be a leaf (either by strict,
or by loose association). Put differently, the last node of a section will
never be a parent node.

That is, because the last descendant entered will always be a leaf. After all,
a section's last node would not be the section's last node, if it were a parent
(Note also, that all nodes must be associated while they are being entered).

No such clarification can be derived for the first node of a section. That is,
because the first node of a section depends on the definition of the section's
sectioning node. In addition to that, such a definition must in general be
independent of the tree's structure.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The end of a section can either be defined in terms of the last node that is
allowed to be associated with a section, or in terms of the first node
that is not allowed to be associated. In the latter case, any node, beginning
with a section's first node, is seen to be related to a section until the first
node is entered that is not intended to be associated with a given section.

Because of that, the search for a section's very last node may skip the

**CLARIFICATION**
If an associated node has subsequent siblings, then these siblings must be
strictly associated next. That is, unless rules exist that the section has
to end with a presequent sibling.

Consequently, the search for a section's very last node may skip the descendants
of any associated node. Because 

<!-- ======================================================================= -->

```
r x ... x n1 x ... x n2:s
        x n3 x ... x n4:s
--- (includes)
<n1>
  <n2:s> ... </n2:s>
</n1>
<n3>
  <n4:s> ... </n4:s>
</n3>
```

<!-- ======================================================================= -->

```
r x ... x n2:s
        x n4:s
--- (includes)
<n2:s> ... </n2:s>
<n4:s> ... </n4:s>
```

<!-- ======================================================================= -->

```
r x ... x n2:s
        x n3 x ... x n4:s
--- (includes)
<n2:s> ... </n2:s>
<n3>
  <n4:s> ... </n4:s>
</n3>
```

<!-- ======================================================================= -->

```
r x ... x n1 x ... x n2:s
        x n4:s
--- (includes)
<n1>
  <n2:s> ... </n2:s>
</n1>
<n4:s> ... </n4:s>
```

<!-- ======================================================================= -->
## Sectioning nodes

```
... x n x c1:s x ...
        x c2:s x ...
```

If no other node in the whole tree is strictly associated with section `s`,
then node `n` is a type-1 sectioning node, because any node descendant to it
is related to that section.

```
... x n x c1   x ...
        x c2:s x ...
        x c3:s x ...
        x c4   x ...
```

However, node `n` can not be a type-1 sectioning node, if it has any child nodes
(e.g. `c1`) that are not associated with section `s`.
