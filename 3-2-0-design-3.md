
<!-- ======================================================================= -->
# Multiple associations

As mentioned before, associating a single node with a section also loosely
associates any descendant of that node with the same section. In addition to
that, any node loosely belongs to any section with which any of its ancestors
is associated.

The questions that now need to be answered next are:

* What happens, if other nodes are associated with the same section?
* What are the consequences with regards to a section's last node?

**TODO**
strict/explicit vs. loose/implicit

<!-- ======================================================================= -->
## multiple associations (1)

```
r x ... x (n):s x (x):s x ... x L
                x ... x (y):s x ... x L
                      x ... (z):s x ... x L
```

If some node `n` is strictly associated with section `s`, then any descendant
of `n` is already loosely related to `s`. Consequently, descendants of node `n`
do not have to be strictly associated with section `s`, if the distinction
between a "strict" and a "loose" relationship is not relevant. That is, if a
loose association can be seen to be equal to a strict association.

Because of that, any rooted path in this context can be reduced to a path which
ends with a strictly associated node. That is, because the remainder of a path,
that passes through such a node, will not change the path's characteristics any
further.

```
r x ... x (x:s)
```

Consequently, a path that is not supposed to fall into the same category must
branch off from some common prefix before the first associated node is reached.
That is, a second path may branch off beginning with the parent of an associated
node and up until the root of the node tree.

<!-- ======================================================================= -->
## example fragment

`A:s <C:s> D:s E </C:s> F`

In this fragment, node `A` can be understood to represent the first node of
section `s`. The next node, that must be strictly associated with section `s`
is node `C`.

Unlike with descendant nodes, an association does not carry over to any
subsequent sibling. That is, because no semantically consistent path can be
defined which connects a node with its next sibling.

Consequently, the very same loose associations mentioned before also apply to
any descendant of node `C`. Node `E` therefore also belongs to section `s`,
whether that node is strictly associated with it or not.

<!-- ======================================================================= -->
## derived statements

**Memory hook**
Strictly associating a single node is equivalent to associating a whole subtree
of nodes whose root is the strictly associated node.

**CLARIFICATION**
Node `n` must be strictly associated with section `s`, if `n` is in relationship
with `s`, and if `n` does not already have a loose relationship with it.

Node `n` would otherwise remain unrelated to section `s`.

**DEFINITION**
Node `n` is said to be a top-level node of a section, if `n` must be strictly
associated with it.

**CLARIFICATION**
Any section is defined by its top-level nodes.

That is, because any other associated node can be derived from the section's
top-level nodes.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
No descendant of a strictly or loosely associated node can be excluded from any
of its ancestor's sections.

Any attempt to define a descendant to be unrelated to any one of its ancestor's
sections is going to be in conflict with the afore mentioned loose associations.

**CLARIFICATION**
It is not possible to clearly identify the relationship between the first node
and the last node of a section.

That is, because any associated node can have any number of descendant nodes.
It is therefore not possible, from a definition's point of view, to clearly
identify a section's last node without forcing a certain structure upon the
nodes of a section.

**CLARIFICATION**
A non-empty section can always be seen to end with its last top-level node.

With that in mind, a section can also be seen to end inside of an associated
container, because the last subsequent descendant of that container (e.g. node
`E`) will then become the section's last node. However, this perspective could
be misleading, because a section can only end with the very last subsequent
descendant (i.e. not some randomly selected one).

**CLARIFICATION**
The last node of any non-empty section will always be a leaf
(either by strict, or by loose association).

That is, because the last descendant entered will always be a leaf.
After all, it would not be the last descendant, if it were a parent.

Put differently, the last node of a section will never be a parent node.

No such clarification can be derived for the first node of a section. That
is, because the first node of a section is specified by a sectioning node's
definition. In addition to that, such a definition is in general independent
of a tree's structure.

<!-- ======================================================================= -->
## multiple associations (2)

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
