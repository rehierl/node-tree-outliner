
<!-- ======================================================================= -->
# Design - implicit associations

```
   n0
========
 n1  n2
```

* `n0` is an inactive node (associated with `s0`)
* `n1` is an end-modifier node (defined to close `s0`)
* `n2` is some inactive node

Due to `n1`'s close modifier, `n2` is defined to not be located inside of `s0`.
However, and because `n0` is associated with `s0`, `n2` is still implicitly
associated with `s0` and as such located inside of `s0`. That is, the modifier
of `n1` results in contradictory statements. Consequently, any instruction to
close a section under these kind of circumstances must be ignored.

Note that, because there is only one type of close modifiers, `n1`'s modifier
will have to be applied when entering the `n1`'s enter event. And, because of
that, the conflicting statements will also apply to `n1` itself.

Note that these structural dependencies can not be undefined. Because of that,
structural relationships override any such extension. That is, such dependencies
always have precedence over any close modifier.

Note that these considerations are independent of where (inside of a node tree)
such a subtree can be found. Such a subtree will always result in the afore
mentioned contradictory statements.

**CLARIFICATION**
Sections can not be closed arbitrarily.

<!-- ======================================================================= -->
## means of detection

Any parent node is a parent container, if it is a type-1 sectioning node, or
if it has a type-2 sectioning node as child node. That is, because sections
must not be allowed to reach past their parent containers. Consistent dynamic
support could otherwise not be guaranteed.

Any parent node can therefore become a section's parent container, regardless
of the definitions associated with its node type. Because of that, such parent
containers exist whether they are manually injected (explicit), or due to
structural dependencies (implicit).

Note that a node can be defined to never be a section's parent container, if
(and only if) the node is not allowed to have type-2 sectioning nodes as child
nodes (e.g. the type-2 sectioning nodes themselves). However, an implementation
is in general unaware of these kind of additional definitions. That is, in
case of input errors or redefinitions, an implementation will still treat
descendant sectioning nodes as actual sectioning nodes and the corresponding
nodes as parent containers. Because of that, reusing sectioning nodes for
purposes other than to declare new sections should be avoided.

**case 1: (node level 1 >> node level 2)**

```
      n0
 ------------
 n1        n3
----
 n2
```

* `n0,n1` are an inactive nodes (associated with `s0`)
* `n2` is a type-2 sectioning node (declares `s2`)
* `n3` is an end-marker node (defined to close `s2`)

If the presequent sectioning node `n2` has a higher node level than the next
subsequent end-marker node `n3`, then the default scope of `s2` will be closed
before `n3` is even entered. Consequently, `n3` can not close `s2`.

Note that, from the perspective of an algorithm, this case is a non-issue. That
is, because closed sections will be ignored by subsequent operations. To be more
accurate, an implementation, when entering `n3` does no longer have to be aware
that `s2` even existed. Because of that, the close modifier of `n3` will not be
understood to be with regards to `n2/s2`, but with regards to some other open
presequent section (i.e. with regards to `n0:s0`). Consequently, modifiers may
yield unexpected results, if this structural aspect is not taken into account.

**case 2: (node level 1 << node level 2)**

```
      n0
 ------------
 n1        n2
          ----
           n3
```

* `n0` is an inactive node (associated with `s0`)
* `n1` is a type-2 sectioning node (associated with `s0`, declares `s1`)
* `n2` is an inactive node (associated with `s1`)
* `n3` is an end-marker node (defined to close `s1`)

If, in contrary to case 1, the next subsequent end-marker node `n3` has a higher
node level than a presequent sectioning node `n1` (i.e. is located deeper within
the node tree), then `n3` has an ancestor which is a top-level node of `s1`.
Because of that, `n3` is implicitly associated with `s1`. Consequently, and in
order to avoid conflicting statements, the close modifier of `n3` can not close
`s1`.

Note that, if `n3` would be a type-2 sectioning node that declared `s3`,
then `s3` would be, by implicit association, a forced subsection of `s1`.

**case 3: (node level 1 == node level 2)**

```
      n0
 ------------
 n1        n3
----      ----
 n2        n4
```

* `n0,n1,n3` are inactive nodes (associated with `s0`)
* `n2` is a type-2 sectioning node (declares `s2`)
* `n4` is an end-marker node (defined to close `s2`)

Note that this case can be understood to contain two independent subtrees that
have `n1` and `n3` as their root nodes. Because of that, this case is similar
to case 1. That is, `s2` will be closed before `n4` is even entered.

Note that the node levels of the corresponding nodes (`n2` and `n4`) don't have
to be equal. For as long as both nodes are located within two different subtrees,
this case will be covered by case 1 (i.e. `s2` is closed before `n4` is entered).

**case 4: (same parent nodes)**

```
      n0
 ------------
 n1        n2
```

* `n0` is an inactive node (associated with `s0`)
* `n1` is a type-2 sectioning node (declares `s1`)
* `n2` is an end-marker node (defined to close `s1`)

In this case, `n2` is in principle free to close the presequent section `s1`.
That is, because the section is still open and because the end-marker node is
not implicitly associated with it.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
An end-marker node may close a section, if (and only if)
the end-marker node is the next sibling of the section's last top-level node.

That is, because ...

* the section still needs to be open. Because of that, the end-marker node
  must be subsequent to the section's sectioning node and presequent to the
  exit event of the section's parent container. Consequently, the end-marker
  node must be a descendant of the section's parent container.
* the end-marker node must not be implicitly associated with the to-be-closed
  section. Because of that, the end-marker node must be a child node of the
  section's parent container. Put differently, the end-marker node must have
  the same node level as the section's top-level nodes.
* Note that the sectioning node's parent node is therefore not the section's
  relevant node, the section's parent container is.

Note that, if the end-marker node had no close modifier, i.e. if it would not
be defined to close the section, then it would be one of the section's top-level
nodes. Due to implicit associations, that node could otherwise not be allowed
to close the corresponding section.

Note that this technically puts end-marker nodes in the position to close type-1
sections. However, the question whether that should even be allowed, still needs
to be answered.

Note that the above considerations have precedence over any extended definition.
That is, close modifiers must be ignored, if they would result in contradictory
statements. Hence, the use of close modifiers is limited.
