
<!-- ======================================================================= -->
# Multiple associations (s)

What effect does it have,
if multiple different nodes are associated with the same section `s`?

```
r x ... x (x):s x (x+1):s x ... x L
                x ... x (y):s x ... x L
                      x ... (z):s x ... x L
```

If some node `x` is strictly associated with section `s`, then any descendant
of `x` is already loosely related to `s`. As a result, descendant nodes of `x`
do not have to be strictly associated with the same section, if the distinction
between a "strict" and a "loose" relationship is not relevant.

Memory hook:
Associating a single node is equivalent to associating a whole subtree of nodes
that begins with the associated node.

With that in mind, and in this context, any rooted path can be reduced to a path
that ends with a strictly associated node, because the remainder of a path, that
passes through such a node, will not change the path's characteristics any
further.

```
r x ... x (x:s)
```

Consequently, a path that is not supposed to fall into the same category must
branch off from some common path before the first associated node is reached.
That is, a second path may branch off beginning with the parent of an associated
node and up until the root of the node tree.

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
## Sectioning node

```
... x n x c1:s x ...
        x c2:s x ...
```

If no other node in the whole tree is strictly associated with section `s`, then
node `n` is the section's sectioning node because any node descendant to it
is related to that section.

```
... x n x c1   x ...
        x c2:s x ...
        x c3:s x ...
        x c4   x ...
```

However, node `n` can not be a sectioning node, if it has any child nodes (e.g.
`c3`) that are not associated with section `s`.

