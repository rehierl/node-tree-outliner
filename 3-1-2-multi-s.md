
<!-- ======================================================================= -->
# Multiple associations

As mentioned before, associating a single node with a given section also loosely
associates any descendant of that node with the same section. In addition to
that, any node loosely belongs to any section with which any of its ancestors
is associated.

The questions that need to be answered next therefore are:

* What happens, if other nodes are associated with the same section?
* What are the consequences with regards to a section's last node?
* Do rules exist that can be used to describe beyond which node a
  section must not reach in order to not violate the fundamental
  aspects with regards to the definition of a section?

<!-- ======================================================================= -->
## associations (1)

```
r x ... x (x):s x (x+1):s x ... x L
                x ... x (y):s x ... x L
                      x ... (z):s x ... x L
```

If some node `x` is strictly associated with section `s`, then any descendant
of `x` is already loosely related to `s`. As a result, descendant nodes of `x`
do not have to be strictly associated with the same section, if the distinction
between a "strict" and a "loose" relationship is not relevant.

**Memory hook**
Explicitly associating a single node is equivalent to associating a whole
subtree of nodes whose root is the strictly associated node.

Consequently, any rooted path can, in this context, be reduced to a path that
ends with a strictly associated node, because the remainder of a path, that
passes through such a node, will not change the path's characteristics any
further.

```
r x ... x (x:s)
```

Consequently, a path that is not supposed to fall into the same category must
branch off from some common prefix before the first associated node is reached.
That is, a second path may branch off beginning with the parent of an associated
node and up until the root of the node tree.

<!-- ======================================================================= -->
## clarifications

`A:s <C:s> D:s E </C:s> F`

Here, node `A` can be assumed to represent the first node of section `s`. The
next node that is subsequent to node `A`, which must be strictly associated with
section `s`, is node `C`. That is, unless section `s` must end with node `A`.

Because of that, the very same loose associations also apply to any descendant
of node `C`. Node `E` therefore also belongs to section `s`, whether that node
is strictly associated with it or not.

**CLARIFICATION**
No descendant of an associated node can be excluded from a parent node's
section. Any attempt to define a descendant to be unrelated to an ancestor's
section is in conflict with the tree of nodes.

**CLARIFICATION**
A section can be seen to end with an associated container. That is, if a
section is not intended to be associated with any subsequent node which is
not a descendant of the associated container.

With that in mind, a section can also be seen to end inside of an associated
container, because the last subsequent descendant of that container (e.g. node
`E`) will then become the section's last node. However, this perspective could
be misleading because a section can not end with some arbitrary descendant.

**CLARIFICATION**
The last node of any non-empty section will always be a leaf node. Either by
strict, or by implicit/loose association. Put differently, no last node will
ever be a parent node. In contrary to that, the very first node of a section
will either be a parent or a leaf.

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
