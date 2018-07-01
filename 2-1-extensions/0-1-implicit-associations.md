
<!-- ======================================================================= -->
# Design - implicit associations

**CLARIFICATION**
Sections can not be closed arbitrarily.

```
   n0
========
 n1  n2
```

* `n0` is an inactive node (associated with `s0`)
* `n1` is an end-marker node (defined to close `s0`)
* `n2` is some other inactive node

Due to `n1`'s close modifier, `n2` is defined to not be located inside of `s0`.
However, and because `n0` is associated with `s0` (i.e. `n0:s0`), `n2` still is
implicitly associated with `s0`, and because of that, is still defined to be
located inside of `s0`. That is, `n1`'s close modifier, if its instruction is
executed, results in contradictory statements. Consequently, any close modifier
must be ignored, if it is in conflict with implicit associations.

Note that, because there is only one type of close modifiers, `n1`'s modifier
must applied when entering `n1`'s enter event. And, because of that, the
conflicting statements will also apply to `n1` itself.

Note that, because these structural dependencies can not be undefined, `n1`'s
close modifier must be understood to represent an user/input error. That is,
structural dependencies have precedence over any close modifier (i.e. a tree's
structure will override any such instruction). Consequently, the use of close
modifiers is limited.

Note that, like close modifiers which instruct to close no section at all, a
close modifier, which must be ignored due to the resulting conflicts, is said
to be not relevant. That is, a close modifier can only be relevant, if it
instructs to close one or more sections, and if it is not in conflict with
implicit associations.

Note that these considerations are independent of where (inside of a node tree)
a subtree is located. Such a subtree will always result in the afore mentioned
contradictory statements.

<!-- ======================================================================= -->
## forced subsections

**CLARIFICATION**
If a sectioning node (`n1`) can not close the current section (`s0`) because
an ancestor of that node (`n0`) is already strictly or loosely associated with
that section, then the section declared by the sectioning node can be referred
to as "a forced subsection of" the ancestor node's parent section (`s0`) and
all of the section's ancestor sections.

Note that the latter aspect is because a node still counts as being explicitly
associated with its parent section, and implicitly with all of the parent
section's ancestor sections (see `SxN` associations).

**Memory hook**
Section `s1` is "a forced subsection of" `s0`, if all content nodes of `s1`
are descendants of a node that is (strictly or loosely) associated with `s0`.

<!-- ======================================================================= -->
## means of detection

Any parent node is a parent container, if it is a type-1 sectioning node, or if
it has a type-2 sectioning node as child node. That is, because sections must
not be allowed to reach past their parent containers. Otherwise, consistent
dynamic support could not be guaranteed.

Any parent node can therefore be a section's parent container, regardless of
any other definition associated with it. Because of that, a section's parent
container exists whether it is manually injected (i.e. explicit), or due to
structural dependencies (i.e. implicit).

Note that a node can be defined to never be a section's parent container, if
(and only if) the node is not allowed to have active nodes as child nodes (e.g.
type-2 sectioning nodes). However, an implementation is in general unaware of
these additional definitions. That is, in case of input errors or redefinitions,
an implementation will still treat descendant active nodes as active nodes and
the corresponding nodes as parent containers. Because of that, the reuse of
sectioning nodes for purposes other than to declare new sections should be
avoided.

<!-- ======================================================================= -->
## means of detection: type-1 sections

**case 1: (parent node != parent container)**

```
   n1
  ====
   n2
--------
 n3  n4
```

* `n1` is a type-1 sectioning node (associated with `s0`, declares `s1`)
* `n2` is some other inactive node (a child of `n1`)
* `n3` is an end-marker node (a child of `n2`, defined to close `s1`)

In this case, the close modifier of `n3` must be ignored. That is, because `n3`,
and potentially any other descendant subsequent to it, is via `n2:s1` implicitly
associated with `s1`. That is, allowing `n3` to close `s1` would result in
conflicting statements with regards to the location (inside `s1` vs. outside of
`s1`) of `n3` and any other subsequent descendant of `n2`.

Note that the parent node of the end-marker node is not identical to the parent
container of the type-1 section it is supposed to close.

**case 2: (parent node == parent container)**

```
   n1
========
 n2  n3
```

* `n1` is a type-1 sectioning node (associated with `s0`, declares `s1`)
* `n2` is an end-marker node (defined to close `s1`)
* `n3` is some other inactive node

In this case, `n2` is in principle free to close `s1`. That is, because `n2`
is not implicitly associated with `s1`. The closure of `s1` will therefore
not result in contradictory statements with regards to the locations of the
corresponding nodes.

Note that the parent node of the end-marker node is identical to the parent
container of the type-1 section it is supposed to close.

Note that the question whether the closure of a type-1 section should even be
allowed, still needs a proper answer. In the context of these considerations,
closing type-1 section via end-marker nodes is technically possible.

<!-- ======================================================================= -->
## means of detection: type-2 sections

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
subsequent end-marker node `n3`, then the default scope of `s2` will be exited
before `n3` is entered. Consequently, `n3` can no longer close `s2` as that
section will already be closed by the time `n3` is being entered.

Note that, from the perspective of an implementation, this case is a non-issue.
That is, because closed sections will be ignored by subsequent operations. To
be more accurate, when entering `n3`, an implementation is no longer required
to know that `s2` ever existed. Because of that, the close modifier of `n3`
will not be understood by an implementation to be with regards to `n2/s2`, but
with regards to some other still open section (e.g. with regards to `n0:s0`).
Consequently, modifiers will yield unexpected results, if the structure of the
node tree is not taken into account.

**case 2: (node level 1 << node level 2)**

```
      n0
 ------------
 n1        n2
          ----
           n3
```

* `n0` is an inactive node (associated with `s0`)
* `n1` is a type-2 sectioning node (declares `s1`)
* `n2` is an inactive node (associated with `s1`)
* `n3` is an end-marker node (defined to close `s1`)

If, in contrary to case 1, the next subsequent end-marker node `n3` has a higher
node level than a presequent sectioning node `n1` (i.e. is located deeper inside
of the node tree), then `n3` has an ancestor which is a top-level node of `s1`.
Because of that, `n3` is implicitly associated with `s1`. And, in order to avoid
contradictory statements, `n3`'s instruction to close `s1` must be ignored.

Note that, if `n3` is replaced by a type-2 sectioning node, then the section
it declares (i.e. `s3`) is by implicit association (i.e. `n2:s1`), a forced
subsection of `s1`.

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

Note that this case can be understood to contain two independent subtrees which
have `n1` and `n3` as their root nodes. Because of that, this case is covered
by case 1. That is, `s2` will be closed by the time `n4` is entered.

Note that the node levels of the corresponding nodes (`n2` and `n4`) don't
have to be equal. Case 1 applies for as long as both nodes are located inside
of independent subtrees (i.e. `s2` will be closed before `n4` is entered).

**case 4: (parent node == parent container)**

```
      n0
 ------------
 n1        n2
```

* `n0` is an inactive node (associated with `s0`)
* `n1` is a type-2 sectioning node (declares `s1`)
* `n2` is an end-marker node (defined to close `s1`)

In this case, `n2` is in principle free to close section `s1`. That is, because
`s1` is still open by the time `n2` is being entered, and because `n2` is not
already implicitly associated with `s1`.

Note that the parent node of the end-marker node is identical to the parent
container of the type-2 section it is supposed to close.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
An end-marker node can be allowed to close a section, if (and only if) the
end-marker node is a sibling of the section's first content node.

That is, because ...

* (1) the section still needs to be open: That is, the end-marker node must be
  subsequent to the section's open event and presequent to the exit event of
  the section's parent container. Consequently, the end-marker node must be
  a descendant of the section's parent container.
* (2) the end-marker node must not already be implicitly associated with that
  section: That is, the end-marker can not be some random descendant of the
  section's parent container; it must be a child node of said container. That
  is, the end-marker node must have the same node level as the section's
  top-level nodes. And, because of that, the end-marker node must be a sibling
  to the section's first content node.

Note that, because no end-marker node will be associated with those sections
that it is supposed to close (i.e. a type-1 close modifier), an end-marker
node will always be the next sibling of a section's last top-level node.

Note that, because of (1) and (2), end-marker nodes are technically in the
position to close type-1 sections. However, the question whether that should
even be allowed, still needs to be answered.

**CLARIFICATION**
A section will either be closed by its parent container,
or by an optional end-marker node.

That is, because if there is no end-marker node before the end of a section's
default scope is reached, then that section ends with its parent container. If
however an end-marker node is reached before its default scope is exited, then
that section ends with the unassociated end-marker node.

Note that, because end-marker nodes do not belong to the sections they close,
the end of a section is still defined by exclusion (see "last nodes"). With
that regards, the definition of end-marker nodes is consistent with the 
definition of parent containers.

**CLARIFICATION**
A section either has an (i.e. one) end-marker node, or it doesn't.

That is, because if a subsequent end-marker node results in the closure of a
section, then that section is no longer relevant to any further subsequent
end-marker node. Put differently, only the first relevant subsequent end-marker
node can have a "close" effect on a section. And, because of that, no section
can ever have more than one relevant end-marker node.

Note that there can be non-relevant end-marker nodes presequent to a section's
relevant end-marker node. That is, if the instructions of those non-relevant
nodes had to be ignored due to structural dependencies.

**CLARIFICATION**
Closing a presequent section with an end-marker node can be understood to set
the following, implementation specific property:

```
Node Section.endMarkerNode
```

Note that this property will hold a `null` reference,
if the corresponding section ends with its parent container.

Note that this property allows to easily determine the last top-level node of
a non-empty section: If `(section.endMarkerNode == null)` is true, then (1) the
parent container's last child, or otherwise (2) the end-marker node's previous
sibling.
