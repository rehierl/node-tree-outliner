
<!-- ======================================================================= -->
# Design (7) - type-1 sections

**QUESTION**
Would it be reasonable to allow an inner sectioning node to close a type-1
section before the end of its sectioning node (default scope) is reached?

Apart from that, allowing a type-1 section to end inside of its sectioning
node would imply to have nodes that are not supposed to belong to the declared
section. Consequently, the type-1 definition of an ordered tree would have to
be inconsistent with the type-1 definition of an unordered tree.

Note that the following considerations are based upon the associations of two
sectioning nodes. That is, if these associations result in conflicts, then such
an "option" can not be allowed. In contrary to that, such an "option" might
still not be possible, even if these associations would seem to support it.

```
========================== -> section s0
n1 n2 n3 n4 n5 n6 n7 n8 n9
```

* `s0` represents the next outer section (e.g. universal section)
* `n1` is a type-1 sectioning node (section `s1`)
* nodes `n2-5` are child nodes of `n1`

Case 1 - default

* `n5` is an inner type-1 sectioning node (section `s5`)
* nodes `n6-9` are child nodes of `n5` (i.e. descendants of `n1`)

Case 2 - alternatively

* `n5` is an inner type-2 sectioning node (section `s5`)
* nodes `n6-9` are siblings to `n5` (i.e. child nodes of `n1`)

In both cases, `n5` is assumed to be defined in such a way that it closes
section `s1` before the content nodes of `s5` are entered. That is, `s5` is
defined to be independent of `s1`. Put differently, no content node of `s1`
can be a content node of `s5` (and vice versa). Because of that, none of
these sections can be an ancestor section of the other. As such, both sections
can only be sibling sections with regards to the next outer section `s0`.

In addition to that, the nodes of both sections remain to have `n1` as one of
their ancestor nodes - this structural relationship can not be undefined.

<!-- ======================================================================= -->
## fundamental aspect

Node `n5` must be a child node of `n1`.

If `n5` is any other descendant, then the parent container of section `s5` will
be associated with `s1`. That is, because it will be associated before `n5` is
entered and thus before `s1` can even be closed. Consequently, all content nodes
of `s5` would then be implicitly associated with `s1`. That is, `s5` then is a
subsection of `s1`. And, because of that, `n5` can not close `s1` without being
in conflict with these implicit associations.

<!-- ======================================================================= -->
## overview

```
n1 \ n5 | s0 | s1 | s5
--------|----|----|----
     s0 |    | x  | ~
     s1 | x  | x  | x
     s5 | x  | x  | x
```

* rows represent those cases in which `n1` is associated with `s0/1/5`
* columns represent those cases in which `n5` is associated with `s0/1/5`
* `x` marks those cases which result in one or more conflicts
* `~` mark those cases which "only" result in some amount of inconsistency

Note that associating a sectioning node with its own section (i.e. `n1:s1` and
`n5:s5`) will automatically be in conflict with those considerations that are
related to not associating any sectioning node with its own section.

<!-- ======================================================================= -->
## n1:s0

```
========================== -> section s0
n1 n2 n3 n4 n5 n6 n7 n8 n9
   ===========             -> section n1
            ============== -> section n5
```

Because sectioning node `n1` is not associated with its own section, there can
not be any conflict with regards to implicit associations. Hence, closing the
declared section before `n1` will be exited is technically possible. That is,
if it does not result in any other conflict.

Note that, because of `n1:s0`, `n5` and all nodes of `s5` are automatically
implicitly associated with section `s0`. However, this is not in conflict
with the goal to have `s5` be independent of `s1` and, as such, a sibling
section to it.

### n1:s0, n5:s0

**TODO**

### n1:s0, n5:s1

Associating `n5` with `s1` results in a conflict:
(1 - due to `n5:s1`) section `s5` is located within `s1`, and
(2 - due to `n6-9`) section `s5` is not located within `s1`.

In order to avoid this conflict:
Node `n5` must not be associated with `s1`.

### n1:s0, n5:s5

With regards to case 1, associating `n5` with `s5` results in some inconsistency:
A type-1 sectioning node (i.e. `n1:s0`) is associated with an outer section,
and another type-1 sectioning node (i.e. `n5:s5`) with its own section.

That is, to which section a type-1 sectioning node belongs, would depend on the
context in which that sectioning node is used. As such, there is no straight
forward implementation.

<!-- ======================================================================= -->
## n1:s1

```
========================== -> section s0
n1 n2 n3 n4 n5 n6 n7 n8 n9
==============             -> section s1
            ============== -> section s5
```

Associating `n1` with `s1` results in the following conflict:
(1 - due to `n1:s1`) nodes `n6-9` are implicitly associated with `s1`, and
(2 - due to `n5` closing `s1`) nodes `n6-9` are completely unrelated to `s1`.

This conflict exists, regardless to which section node `n5` belongs.

In order to avoid this conflict:
Node `n1` must not be associated with `s1`.

### n1:s1, n5:s0

**TODO**

### n1:s1, n5:s1

Associating `n5` with `s1` results in another conflict:
(1 - due to `n5:s1`) section `s5` is located within `s1`, and
(2 - due to `n6-9`) section `s5` is not located within `s1`.

In order to avoid this conflict:
Node `n5` must not be associated with `s1`.

### n1:s1, n5:s5

No further conflict other than the one caused by the
above mentioned implicit association (i.e. `n1:s1`).

<!-- ======================================================================= -->
## n1:s5

```
========================== -> section s0
n1 n2 n3 n4 n5 n6 n7 n8 n9
  ============             -> section s1
            ============== -> section s5
==                         -> n1:s5
```

Associating `n1` with `s5` results in the following conflict:
The subsequent and subordinate node `n5` defines to which section
node `n1`, which is superordinate to `n5`, belongs.

Node `n5` is not within the context of node `n1`.

In addition to that, and because nodes `n2-4` are then also implicitly
associated with section `s5`, they thus implicitly depend on node `n5`,
which does not belong to their context.

In order to avoid this conflict:
Node `n1` must not be associated with such an inner section.

<!-- ======================================================================= -->
## considerations

Is there any good reason as to why place section `s5` inside of node `n1`, if
all the corresponding nodes are not supposed to be in any kind of relationship
with section `s1`? You might as well just add all these nodes after `n1` (i.e.
not as descendants of `n1`).

Placing section `s5` inside of node `n1` by itself states that both sections
(`s1` and `s5`) are, one way or another, in some kind of relationship with
each other. Forcefully trying to undefine that relationship, whatever it
exactly is, can only result in conflicting statements.

The only possible reason could be to also apply some other characteristic of a
type-1 sectioning node to the inner subsequent section `s5`. That is, use the
grouping capabilities of the outer type-1 sectioning node.

<!-- ======================================================================= -->
## HTML5

HTML5's association of sectioning nodes:

* sectioning root elements with the current outer section
* sectioning content elements with their first inner section
* heading content elements with their implied section.

Other notes on HTML:

* The 1st heading is (in general) defined to define the
  heading of the next ancestor element of sectioning content/root.
* A 2nd heading, which has the same rank as the 1st heading,
  will close the previous section and create an implied section.
* An inner sectioning root element does not close the section
  of an ancestor sectioning root/content element.
* An inner sectioning content element does (in general) not close
  the section of an ancestor sectioning root/content element.

### n1:s0, n5:s5

```
body h1 h1 /body
```

### n1:s1, n5:s5

```
section h1 h1 /section
```

With that in mind, the associations established by HTML's current approach are
not that arbitrary after all. However, the 2nd section is still also implicitly
associated with the 1st section (=> in conflict).
