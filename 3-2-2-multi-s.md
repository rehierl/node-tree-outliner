
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

