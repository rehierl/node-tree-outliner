
<!-- ======================================================================= -->
# Multiple sections (s,t)

What effects does it have,
if some node `nx` is associated with section `s` and
if some descendant node `ny` is associated with section `t`?

```
< root <                path-of-nodes                 > leaf >
> parent-of >                                     < child-of <
> contains >                                    < belongs-to <

          s                  t                 (down) contains
          x                  x
... x N x nx x N x ... x N x ny x N x ...      (up) belongs-to
                 x ... x N x nz x ...
```



This merely reflects that any descendant of `n2` belongs to section `s1` and
section `s2` at the same time. However, the same does not apply to any
descendant of `n1` that is also descendant of `n2`.
