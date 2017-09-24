
# The heading elements (h1-6)

```html
A
<h1>B</h1>
C
```

A, B and C represent non-element nodes, element nodes or subtrees of such nodes.
They represent (even empty) subtrees that do not contain any sectioning element.
None of the nodes in those subtrees introduces a new section.

The outline of the above fragment is as follows:

```
Untitled section
  B
```

The nodes in this fragment must be associated (with sections) as follows:

```
s0: A
s0: <h1>
s0:   B
s0: </h1>
s1: C
```
