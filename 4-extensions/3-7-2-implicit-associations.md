
<!-- ======================================================================= -->
# Design - implicit associations

```
   n0
========
 n1  n2
```

* `n0` is an inactive parent node (associated with `s0`)
* `n1` is a node that has a close modifier associate with it
* `n1`'s close modifier instructs to close `s0`

Due to `n1`'s close modifier, `n2` would no longer be located inside of section
`s0`. However, and because `n0` is still associated with `s0`, `n2` would still
be implicitly associated with `s0` (i.e. located inside of `s0`).

Note that, if `n1`'s close modifier would have to be applied when entering the
node's enter event, then the conflicting statements would also apply to `n1`.

In order to avoid such conflicts, any instruction to close `s0` must be ignored.
That is, because `n2` belongs by structural relationship to `s0`. Consequently,
and under these kind of circumstances, `n1` can not be allowed to close `s0`.

Note that these structural dependencies can not be undefined. Because of that,
structural relationships override any extension. That is, such dependencies
always have precedence over any close modifier.

Note that these considerations are independent of where (inside of a node tree)
such a subtree can be found. Such a subtree will always result in the afore
mentioned conflict.

**CLARIFICATION**
Sections can not be closed arbitrarily.

<!-- ======================================================================= -->
## parent containers

Any parent node is a parent container, if it is a type-1 sectioning node, or
if it has type-2 sectioning nodes as child nodes. That is, because sections
must not be allowed to reach past their parent containers. Consistent dynamic
support could otherwise not be guaranteed.

Any parent node can therefore become a section's parent container, regardless
of its specific definition. Because of that, such parent containers exist
whether they are manually injected (explicit), or due to structural dependencies
(implicit).

Note that a node can be defined to never be a section's parent container, if
(and only if) the node is not allowed to have type-2 sectioning nodes as child
nodes (e.g. the type-2 sectioning nodes themselves). However, an implementation
is in general unaware of these kind of additional definitions. That is, in
case of input errors or redefinitions, such an implementation will still treat
descendant sectioning nodes as actual sectioning nodes and the corresponding
nodes as parent containers. Because of that, reusing sectioning nodes for
purposes other than to declare new sections should be avoided.

**case 1: (node level 1 >> node level 2)**

```
      n0
 ------------
 n1        n2
----
 n3
```

* `n1` is an inactive parent node
* `n2, n3` are type-2 sectioning nodes

If a presequent sectioning node `n3` has a higher node level than the next
subsequent sectioning node `n2`, then the default scope of `s3` ends before
`n2` is entered. That is, `s3` and `s2` are, by structural relationship,
independent from each other. Consequently, `n2` can not have any effect on
`s3`. That is, `s2` can not be a subsection to `s3` and `n2` can no longer
close `s3` (as it is already closed when `n2` is being entered).

Note that, from the perspective of an algorithm, this case is a non-issue.
That is, because sections will be ignored by subsequent operations as soon
as they are closed. Because of that, any modifier (`n2`) is *not* understood
to be with regards to `n3/s3`, but with regards to some other open presequent
section. Consequently, modifiers may yield unexpected results, if this
structural aspect is not taken into account.

However, certain conditions may still yield a seemingly identical result. If
that is the case, the reasons for those matching results differ none the less.

**case 2: (node level 1 << node level 2)**

```
      n0
 ------------
 n1        n2
          ----
           n3
```

* `n2` is an inactive parent node
* `n1, n3` are type-2 sectioning nodes

If, in contrary to that, the next subsequent sectioning node `n3` has a higher
node level than a presequent sectioning node `n1`, then `n3` has an ancestor
that is a top-level node of `s1`. Consequently, `s3` is by implicit association
a subsection to `s1`. Because of that, and in order to avoid conflicting
statements, any instruction to close `s1` when `n3` is being entered, must be
ignored. That is, `s3` can not be independent of `s1` (e.g. a sibling section
to it).

Note that `s3` is a forced subsection of `s1`.

**case 3: (node level 1 == node level 2)**

```
      n0
 ------------
 n1        n3
----      ----
 n2        n4
```

* `n1, n3` are inactive container nodes
* `n2, n4` are type-2 sectioning nodes

Note that this case can be understood to contain two independent subtrees that
have `n1` and `n3` as their root nodes. Because of that, this case is similar
to case 1: `s2` will be closed before `n4` is even entered.

Note that the node levels of the corresponding sectioning nodes don't have to
be equal for as long as both nodes are located within two different subtrees.
The effect will still be covered by case 1 (i.e. `s2` is closed when `n4` is
entered).

**case 4: (same parent container)**

```
      n0
 ------------
 n1        n2
```

* `n1, n2` are type-2 sectioning nodes

However, `n2` is in principle free to close the open presequent section `s1`, if
(and only if) both type-2 sectioning nodes have the same parent node (i.e. the
same parent container).

Note that the parent section of `s2`, if `n2` is defined to close `s1`, can only
be one of the remaining open sections, which all are ancestor sections of `s1`.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Parent containers have significant impact on the use of close modifiers.

Note that the above considerations have precedence over any extended definition.
That is, such non-default definitions must be ignored, if they are in conflict
with structural dependencies. Hence, the use of close modifiers is limited.
