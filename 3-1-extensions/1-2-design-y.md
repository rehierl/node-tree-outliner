
<!-- ======================================================================= -->
# Design - type-1 sections

**QUESTION**
Would it be reasonable to allow an inner sectioning node to close a type-1
section before the end of its sectioning node (default scope) is reached?

Note that the following considerations are based upon the association of two
sectioning nodes. That is, if all of the below mentioned associations result
in conflicts, then such an "option" can not be allowed. However, if certain
associations would seem to support such an "option", then that "option" might
still not be free of conflicts. That is because such conflicts could still
be caused based on reasons that are unrelated to the associations mentioned
below.

<!-- ======================================================================= -->
## introduction

**TODO**
fragments need a better structure -
i.e. a node hierarchy, not linear

```
n1 n2 n3 n4 n5 n6 n7 n8 n9
========================== -> s0
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
sections can be an ancestor section of the other. Consequently, both sections
are sibling sections with regards to the next outer section `s0`.

Note that if `n1` is itself defined to close the last outer open presequent
section, then section `s0`  represents the last presequent section that remains
to be open. That is, the following considerations need to be understood to be
independent of this outer aspect.

<!-- ======================================================================= -->
## fundamental considerations

The intention behind allowing to close section `s1` raises the question as
to why not to add an additional type-1 sectioning node as sibling to `n1` and
then use it to hold the contents of section `s5`. That is, the current default
definitions already allow to express the section hierarchy that the modified
definitions are supposed to allow.

One possible reason could be to apply some other characteristic of a type-1
sectioning node (i.e. due to its grouping characteristic) to the optional inner
subsequent section `s5`. However, a second subsequent sibling type-1 sectioning
node would have the very same characteristic.

> Based on optional subsequent nodes.

Such an option will obviously have to depend on optional subsequent descendant
nodes. That is because the definition of a type-1 sectioning node is only able
to cover a single default case (i.e. there is no such inner node). And, because
of that, a type-1 section will by default still have to end with its default
scope.

Note that this should not be understood as an argument against such an option.
That is because there is no other way to deviate from default definitions.

> Structural relationship

Placing section `s5` inside of node `n1` by itself states that sections `s1`
and `s5` are structurally related with each other. That is because nodes
`n2-9` all have `n1` as an ancestor node.

Note that this relationship can not be undefined.
That is, the modified definitions must take this dependency into account.

> In conflict with dynamic support.

One issue that results from such a placement (i.e. `s5` inside of `n1`) is,
that any dynamic operation (e.g. fold/unfold) on `n1` targeted at `s1` will
also affect `n5/s5`.

If, for example, `s1` would have to be folded, then that could not be done
without hiding `s5` at the same time (although `s5` is supposed to be
independent of `s1`). Transparent (i.e hidden/background) transformations
prior to such an operation could not be avoided.

(That consideration alone nullifies the purpose of any such definitions).

> Node `n5` must be a child node of `n1`.

If `n5` is some other descendant of `n1` (i.e. not a child node), then the
parent container of `s5` will be associated with `s1`. That is because it
will be associated before `n5` is entered and thus before `s1` can even be
closed.

Consequently, all content nodes of `s5` would be implicitly associated with
`s1`: Section `s5` would be (by structural relationship) a subsection of `s1`.
Because of that, and in order to avoid conflicting statements caused by these
implicit associations, `n5` could then not be allowed to close `s1`.

If that condition is not met, then an implementation can not support these kind
of modified definitions. Under these circumstances, these definitions would have
to be ignored. Consequently, the use of such definitions is limited.

> Context dependent associations must be avoided.

If a certain type of sectioning node is by default associated with a presequent
section, and under certain circumstances associated with some other section
(e.g. the section it declares), then the association of that type of sectioning
node would depend on its outer context in which it is used.

Consequently, an implementation would always have to first determine the context
in which this type of sectioning node is used. And, because of that, there could
not be a simple and straight forward implementation.

Note that any sectioning node could initially be associated according to some
default definition. Then, if certain conditions are detected/met, the default
association could be replaced with a context dependent association. However,
one would have to ensure that the initial association (until changed) does not
have any side effect, as that could result in a conflict with regards to the
node's final association. - Then again, how could one possibly know if the
association of such a sectioning node won't have to be changed at some later
point in time? That is, at what point does an implementation have the guarantee
that the node's association will remain as is?

<!-- ======================================================================= -->
## overview

```
   \ n5 |    |    | 
 n1 \   | s0 | s1 | s5
--------|----|----|----
     s0 | *  | x  | x
     s1 | x  | x  | x
     s5 | x  | x  | x
```

* rows represent those cases in which `n1` is associated with `s0/1/5`.
* columns represent those cases in which `n5` is associated with `s0/1/5`.
* `x` marks those cases which result in conflicts, inconsistencies
  and/or non-trivial associations.
* `*` marks those cases which don't disallow such modified definitions.

Note that associating a sectioning node with its own section (i.e. `n1:s1`
or `n5:s5`) will automatically be in conflict with those considerations that
are related to not associating any sectioning node with its own section. This
aspect applies to any case that does not follow this default definition.

Note that it is trivial to associate a sectioning node with its own section
(e.g. `n1:s1`, `n5:s5`). If a `currentSection` variable is available, then
it is also trivial to associate a sectioning node with the last open presequent
section (e.g. `n1:s0`, `n5:s1`, `n5:s0`).

Recall that `x:y` represents the association of node `x` with section `y`.

<!-- ======================================================================= -->
## n1:s0

```
n1 n2 n3 n4 n5 n6 n7 n8 n9
========================== -> s0
   ===========             -> s1
            ============== -> s5
```

Because the sectioning node `n1` is not associated with its own section, there
is no conflict with regards to implicit associations. Consequently, closing
`s1` before `n1` will be exited, appears to be possible.

Note that, because of `n1:s0`, `n5` and all nodes of `s5` are automatically
implicitly associated with section `s0`. However, this is not in conflict
with the goal of `s5` being independent of `s1`.

**n1:s0, n5:s0**

With regards to associations, this case does not seem to result in a
conflict, or add inconsistencies. => Requires further considerations.

**n1:s0, n5:s1**

Associating `n5` with `s1` results in a conflict:
(1 - due to `n5:s1`) section `s5` is located inside of `s1`, and
(2 - due to `n5` closing `s1`) nodes `n6-9` are not located inside of `s1`.

Both statements combined result in contradictory statements with
regards to the location of a section (/see/ strong connectivity /).

**n1:s0, n5:s5**

1. Context dependent associations (case 1).
2. Inconsistent associations across all types of sectioning nodes (case 2).

Note HTML's current associations:
sectioning root vs. heading content.

<!-- ======================================================================= -->
## n1:s1

```
n1 n2 n3 n4 n5 n6 n7 n8 n9
========================== -> s0
==============             -> s1
            ============== -> s5
```

Associating `n1` with `s1` results in the following conflict:
(1 - due to `n1:s1`) nodes `n6-9` are implicitly associated with `s1`, and
(2 - due to `n5` closing `s1`) nodes `n6-9` are unrelated to `s1`.

Both statements combined result in contradictory statements with
regards to `s5` being a subsection of `s1` or not.

This conflict exists, regardless to which section `n5` belongs.

**n1:s1, n5:s0**

1. Context dependent associations (case 1).
2. Inconsistent associations across all types of sectioning nodes (case 2).

**n1:s1, n5:s1**

1. Context dependent associations (case 1).
2. Inconsistent associations across all types of sectioning nodes (case 2).

Associating `n5` with `s1` adds another conflict:
(1 - due to `n5:s1`) section `s5` is located inside of `s1`, and
(2 - due to `n5` closing `s1`) section `s5` is not located inside of `s1`.

Both statements combined result in contradictory statements with
regards to the location of a section (/see/ strong connectivity /).

**n1:s1, n5:s5**

No conflict other than the one caused by the
afore mentioned implicit associations (i.e. `n1:s1`).

Note HTML's current associations (an error):
sectioning content vs. heading content.

<!-- ======================================================================= -->
## n1:s5

```
n1 n2 n3 n4 n5 n6 n7 n8 n9
========================== -> s0
  ============             -> s1
            ============== -> s5
==                         -> n1:s5
```

Associating `n1` with `s5` results in the following conflict:
The subsequent optional node `n5` determines to which
section the presequent node `n1` belongs.

Note that node `n5` is not within the context of `n1` and
therefore not allowed to have such an effect on it.

In addition to that, and because nodes `n2-4` are then also implicitly
associated with section `s5`, they would also depend on the subsequent
node `n5`. And, because of that, section `s1` would be a subsection
of the optional subsequent section `s5`.

<!-- ======================================================================= -->
## preliminary summary

With regards to associations, only case "n1:s0, n5:s0" does not seem to
result in any conflict. That is because the associations are consistent
with the default association of sectioning nodes.

Note that when entering `n5` and closing `s1`, the `currentSection` variable
needs to be modified to refer to `s1`'s parent section (e.g. `s0`). Because
of that, an implementation of the `n5:s0` association is trivial.

Note that the use of such definitions is still limited:
`n5` must be a child node of `n1`.

However, placing a section inside of a type-1 sectioning node and then define
it to be independent of that node still appears to be inconsistent. That is,
because `n5`, a descendant of `n1`, is associated with an outer section.

**TODO**
Further considerations are in order.

<!-- ======================================================================= -->

**TODO**
feels a bit like trying to redefine sectioning nodes -
i.e. appears to declare multiple sections instead of one -
can "declares one" support/include multiple, equally ranked sections? -
does a type-1 sectioning node not imply a single hierarchy?

**TODO**
Note that an inner type-1 sectioning node can (by default) not be allowed
to close its next outer type-1 section. If the default definition had that
characteristic, then no section hierarchy could be established, if only
type-1 sectioning nodes are available. That is, apart from sandboxing such
a sectioning node inside of an explicit parent container.

=> must be limited to an outer t1 in combination with inner t2s?

**TODO**
`t1 A t1 B /t1 C /t1`

to which section would C belong, if the inner t1 would end section A? -
to the next outer section - which is why one would be required -
problematic with regards to the root section -

lost in U - unrelated to A and B - although in the same tree -
really that lost? - yes, that lost -
the logical view (sections) must be complete/total -

can not end an outer section at the same time -
especially an outer type-1 section (e.g. root section) -
a type-1 sectioning node can not end a presequent type-1 section?

<!-- ======================================================================= -->
## derived statements

**TODO**
A single tree of sections?

**DEFINITION**
A type-1 section always ends with its default scope.
