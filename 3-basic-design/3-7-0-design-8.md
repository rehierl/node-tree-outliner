
<!-- ======================================================================= -->
# Design (7) - type-1 sections

**TODO**
A single tree of sections?

**QUESTION**
Would it be reasonable to allow an inner sectioning node to close a type-1
section before the end of its sectioning node (default scope) is reached?

Note that such an option will have to depend on optional subsequent descendant
nodes. That is, because the definition of a type-1 sectioning node is only able
to cover a single default case. And, because of that, a type-1 section will by
default still have to end with its default scope.

Note that the following considerations are based upon the association of two
sectioning nodes. That is, if all of the below mentioned associations result
in conflicts, then such an "option" can not be allowed. If however certain
associations would seem to support such an "option", then that "option" might
still not be possible. That is, because it could still result in conflicts
that are unrelated with the below mentioned associations.

<!-- ======================================================================= -->
## introduction

```
========================== -> section s0
n1 n2 n3 n4 n5 n6 n7 n8 n9
```

* `s0` represents the next outer section (e.g. the universal section)
* `n1` is a type-1 sectioning node (declares section `s1`)
* nodes `n2-5` are child nodes of `n1`

Case 1 - default

* `n5` is an inner type-1 sectioning node (declares section `s5`)
* nodes `n6-9` are child nodes of `n5` (i.e. distant descendants of `n1`)

Case 2 - alternatively

* `n5` is an inner type-2 sectioning node (declares section `s5`)
* nodes `n6-9` are siblings to `n5` (i.e. additional child nodes of `n1`)

In both cases, `n5` needs to be understood to be defined in such a way that it
closes section `s1` before the content nodes of `s5` are entered. That is, `s5`
is defined to be independent of `s1`. Put differently, no content node of `s1`
can be a content node of `s5` (and vice versa). Because of that, none of these
sections can be an ancestor section of the other. As such, both sections are
sibling sections with regards to the next outer section `s0`.

<!-- ======================================================================= -->
## fundamental aspect

The goal of allowing to close section `s1` raises the question as to why not
to add an additional type-1 sectioning node as sibling to `n1` and then use it
to hold the contents of section `s5`. That is, the current default definitions
already allow to express the structure that this option is intended to support.

Placing section `s5` inside of node `n1` by itself states that sections `s1`
and `s5` have a strong structural relationship with each other. That is, because
nodes `n2-9` all have `n1` as one of their ancestor nodes. Trying to undefine
that relationship can in general only result in conflicting statements.

The only possible reason could therefore be to apply some other characteristic
of a type-1 sectioning node (i.e. due to its grouping characteristic) to the
inner optional subsequent section `s5`. Then again, a second subsequent sibling
type-1 sectioning node would have the very same characteristic.

<!-- ======================================================================= -->
## fundamental aspect

Node `n5` must be a child node of `n1`.

If `n5` is a type-2 sectioning node and, in addition to that, some other
descendant of `n1`, then the parent container of `s5` will be associated with
`s1`. That is, because it will be associated before `n5` is entered and thus
before `s1` can even be closed. Consequently, all content nodes of `s5` would
be implicitly associated with `s1`. That is, `s5` would be a subsection of `s1`.
And, because of that, `n5` could not be allowed to close `s1` in order to avoid
conflicting statements with regards to these implicit associations.

Such an option can therefore only be supported under certain circumstances.
If the above condition is not met, then an implementation can not support such
an option. That is, the corresponding definition must be ignored if the parent
node of such an inner sectioning node is not a type-1 sectioning node.

<!-- ======================================================================= -->
## fundamental aspect

Context dependent associations must be avoided.

If a certain type of sectioning node is by default associated with a presequent
section, and under certain circumstances associated with some other section
(e.g. the section it declares), then the association of that type of sectioning
node would depend on the context in which it is used.

Consequently, an implementation would always have to first determine the context
in which that type of sectioning node is used. Consequently, there can not be a
simple and straight forward implementation.

<!-- ======================================================================= -->
## overview

```
n1 \ n5 | s0 | s1 | s5
--------|----|----|----
     s0 | x  | x  | x
     s1 | x  | x  | x
     s5 | x  | x  | x
```

* rows represent those cases in which `n1` is associated with `s0/1/5`.
* columns represent those cases in which `n5` is associated with `s0/1/5`.
* `x` marks those cases which result in conflicts, inconsistencies
  and/or non-trivial associations.

Note that associating a sectioning node with its own section (i.e. `n1:s1` or
`n5:s5`) will automatically be in conflict with those considerations that are
related to not associating any sectioning node with its own section.

Note that it is trivial to associate a sectioning node with its own section
(e.g. `n1:s1` or `n5:s5`). If a `currentSection` variable is available, then it
is also rather straight forward to associate a sectioning node with the last
presequent open section (e.g. `n1:s0` or `n5:s1`). 

<!-- ======================================================================= -->
## n1:s0

```
========================== -> section s0
n1 n2 n3 n4 n5 n6 n7 n8 n9
   ===========             -> section n1
            ============== -> section n5
```

Because the sectioning node `n1` is not associated with its own section, there
is no conflict with regards to implicit associations. Consequently, closing
`s1` before `n1` will be exited is technically possible. That is, if no other
conflict prohibits the corresponding definitions.

Note that, because of `n1:s0`, `n5` and all nodes of `s5` are automatically
implicitly associated with section `s0`. However, this is not in conflict
with the goal to have `s5` be independent of `s1` and, as such, a sibling
section to it.

### n1:s0, n5:s0

Note that associating `n5` with `s0` is non-trivial.

### n1:s0, n5:s1

Associating `n5` with `s1` results in a conflict:
(1 - due to `n5:s1`) section `s5` is located within `s1`, and
(2 - due to `n6-9`) section `s5` is not located within `s1`.

This is obviously in conflict with the section's strong connectivity
between its sectioning node and its content nodes.

### n1:s0, n5:s5

1. Context dependent associations with regards to case 1.
2. Inconsistent associations with regards to the types of sectioning nodes.

Note that HTML's current associations aren't that arbitrary after all:
compare sectioning root with heading content.

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
(2 - due to `n5` closing `s1`) nodes `n6-9` are unrelated to `s1`.

This conflict exists, regardless to which section node `n5` belongs.

### n1:s1, n5:s0

1. Context dependent associations with regards to case 1.
2. Inconsistent associations with regards to the types of sectioning nodes.

Note that associating `n5` with `s0` is non-trivial.

### n1:s1, n5:s1

Associating `n5` with `s1` results in another conflict:
(1 - due to `n5:s1`) section `s5` is located within `s1`, and
(2 - due to `n6-9`) section `s5` is not located within `s1`.

This is obviously in conflict with the section's strong connectivity
between its sectioning node and its content nodes.

### n1:s1, n5:s5

No conflict other than the one caused by the
implicit associations (i.e. `n1:s1`).

Note that HTML's current associations aren't that arbitrary after all:
compare sectioning content with heading content.

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
The subsequent optional node `n5` determines to which
section the presequent node `n1` belongs.

Note that node `n5` is not within the context of node `n1` and
therefore not allowed to have any effect on `n1`.

In addition to that, and because nodes `n2-4` are then also implicitly
associated with section `s5`, they would also depend on the subsequent
node `n5`. And, because of that, section `s1` would become a subsection
of the optional subsequent section `s5`.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
With regards to the association of sectioning nodes, allowing a type-1 section
to be closed before the end of its default scope is reached, is ill advised. No
sectioning node can therefore be allowed to prematurely close a type-1 section.

That is, because any combination of associations results in
(1) conflicts, (2) inconsistencies, and/or (3) non-trivial associations.

Note that the most interesting case of the above considerations is
case "n1:s0, n5:s0". However, the association "n5:s0" is non-trivial.

**DEFINITION**
A type-1 section always ends with its default scope.
