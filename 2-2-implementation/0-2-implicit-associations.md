
<!-- ======================================================================= -->
# Implementation - implicit associations

The focus of the following content is on the implementation of extensions: How
to avoid conflicts caused by implicit associations when closing sections due to
end-marker nodes? In short: How to implement the end-marker role?

<!-- ======================================================================= -->
## examples

```
      n0
================
n1 n2         n5
   --------
      n3 n4
```

* `n0` is an inactive node (associated with `s0`)
* `n1, n3-5` are type-2 sectioning nodes
* `ni` declares `si` for all `(i >= 1)`
* `n2` is an inactive node (associated with `s1`)

Note that the default definitions are assumed to always apply up until entering
the corresponding node. That is, close modifiers of presequent nodes (if any)
are ignored (i.e. think of the above fragment as representing multiple separate
examples).

### which sections nodes may close

```
 ni can   |
 close sj | s0 | s1 | s3 | s4
------------------------------
       n1 | 0  |    |    | 
       n2 | 0  | 1  |    | 
       n3 | 0  | 0  |    | 
       n4 | 0  | 0  | 1  | 
       n5 | 0  | 1  |    |  
```

* `1` := `ni` *can* close section `sj`
* `0, [empty]` := `ni` *can not* close section `sj`

Note that, if `n0` would be a type-1 sectioning node that declared section `s0`,
then `n1,n2,n5` could technically be allowed to close `s0`. That is, because
due to the definition of type-1 sectioning nodes, `n0` would not be associated
with `s0`.

### 'si' is a forced subsection of 'sj'

```
  \ sj |
si \   | s0 | s1 | s3 | s4
---------------------------
    s1 | 1  |    |    | 
    s3 | 1  | 1  |    | 
    s4 | 1  | 1  |    | 
    s5 | 1  |    |    | 
```

* `1 := true`, `0, [empty] := false`
* e.g. `s4` is a forced subsection of `s1` and `s0`
* e.g. `s4` is *not* a forced subsection of `s1`

Note the `1` entries are located in cells, which correspond with those cells in
the first table that hold `0` entries.

<!-- ======================================================================= -->
## switching to a different parent section

In essence, an implementation is executed on the tree's node sequence. That is,
it enters one node after another and, at some point, enters the next subsequent
node. When that happens, the implementation's current context contains the
current rooted path of nodes (begins in the node tree's root and ends in the
node being entered) and the current path of sections (begins in the root section
and ends in the current section).

Note that there is only one generic type of close modifiers:
Close sections when entering an end-marker node's enter event.

Note that, because no ancestor section can be closed before all of its
subsections are closed (sections must be closed in an orderly fashion),
the section that has to be closed first always is the current section.

In order to avoid any conflict due to implicit associations, an implementation
needs to execute the following loop when entering the next node:

0. Evaluate the current node's close modifier in order to determine, if and how
   many sections need to be closed. Obviously, if the current node has no close
   modifier (i.e. is no end-marker node), then no sections need to be closed.
1. Enter/Continue the loop, if sections (still) need to be closed.
3. Test if the current node is implicitly associated with the current section.
4. Exit the loop, if the current node *is* implicitly associated.
5. Close and pop the current section, if the current node *is not* implicitly
   associated. The old current section's parent section will then be the new
   current section.
6. (Continue the loop)

After exiting that loop, the current (end-marker) node must be associated with
the (new) current section (i.e. the node's parent section).

Note that, if the current node is also a sectioning node, then the section it
declares will be added as subsection to the (new) current section. After that,
the declared section will be next (new) current section.

<!-- ======================================================================= -->
## performance related aspects

In general, and from a formal perspective, "skipping some or most of the open
sections", by directly jumping to the next new current section, is not allowed.
That is, because ...

* (1) one or more open sections can be forced subsections of their ancestors
  (e.g. when entering `n4`, `s3` is a forced subsection of `s1` and `s0`).
* (2) one way or another, each section must be closed explicitly (see the
  definition of section states), in an orderly bottom-up fashion (close
  subsections first).

**TODO**
However, from a practical perspective (i.e. depending on the exact environment
of an implementation) certain improvements might be possible ...

* switching from the old current section to the new current section could be
  considered to "implicitly close" all descendant sections of the new current
  section.
* requires that no event handlers have to be supported
* question: could it be detected if such a jump would cause issues with forced
  subsections?

Note that, from a practical perspective, custom event handler routines could be
associated with each close operation. Because of that, even an implementation
might still have to close each section separately.

**TODO**
Note that a `bool Section.isForcedSubsection` property (i.e. `true` if the
property's section object is a forced subsection of its parent section), set
after exiting the above loop, can not be used to improve the performance.
That is, because all tests are with regards to the relationship between the
end-marker node and the corresponding current section, not with regards to
the relationship between the current section and its parent section.

<!-- ======================================================================= -->
## means of detection

The two most critical aspects of the above loop are: (1) starting with the
current node, determine how many sections need to be closed, and (2) detect
if the current section can be closed without any conflict.

Note that aspect (1) is not part of these considerations. That is, because it
depends on the specific notation used to specify close modifiers. In contrary
to that, aspect (2) is generic to all close modifiers and will be dealt with
by the following considerations.

The question therefore is: How can an implementation decide, whether or not
the current end-marker node can be allowed to close the current section?

As stated in the "implicit associations" chapter, a node is free to close a
section, if (and only if) the node being entered is a sibling to the section's
first content node. Because of that, several options are available, each with
its own advantages and disadvantages.

Note that, except for the last option, all other options technically allow to
close type-1 sections from within its sectioning node. That is, if it would not
be allowed to close a type-1 section, then additional type-dependent tests would
have to be included with these options. In contrary to that, and if it would not
be allowed to close type-1 sections, then no additional type-dependent tests are
required, if (and only if) the last option is used instead. That is, the last
option is truly type-independent (i.e. generic).

Note that the universal section has no existing parent container (i.e. virtual).
This aspect might have to be taken into account, if a close modifier would
instruct an implementation to close all open sections (i.e. up to and including
the root section). Obviously, and because the root node must act as a type-1
sectioning node, the question whether that should even be allowed depends on
the question whether in general it should be allowed to close type-1 sections.

Note that the root node can technically not act as an end-marker node. That is,
because the universal section is not allowed to ever be closed, this section is
defined to be omnipresent. Because of that, and if the root node has a close
modifier, an implementation must always ignore the root's modifier.

<!-- ======================================================================= -->
## Option 1: parent container references, node identifiers

The first option could be to test whether the end-marker's parent node is
identical to a section's parent container. That is, an implementation would
have to hold a reference to a section's parent container with each section
object (e.g. set when the corresponding section object is created):

```
1. Node Section.parentContainer
2. (node.parentNode === currentSection.parentContainer)
```

When a subsequent end-marker node is entered, an implementation could then use
that parent container reference to test whether the reference of the current
node's parent node is identical to the section's parent container reference.
If that is the case, the corresponding section has to be closed. Otherwise,
the end-marker node is identified to be implicitly associated, which is why
the current node's close modifier must be ignored.

Note that an implementation will neither encounter case-1 nor case-3 with
regards to type-2 sections (see the "implicit associations" chapter). That is,
because the corresponding sections are already closed and will therefore no
longer appear within the current path of sections. Because of that, the only
relevant cases are case-2 and case-4. Consequently, an entered end-marker
node either is a child node of the section's parent container, or one of the
container's distant descendants.

However, holding a node reference with each section object will increase the
memory footprint of the resulting outline. Hence, these references can, but
should not be used by implementations if memory requirements are critical,
or unless those references have any other use besides supporting the outline
algorithm itself. Otherwise, there is no need to add a permanent property to
each section object.

Note that node references are very similar to unique number identifier values.
Because of that, and depending on an implementation's specific environment
(e.g. adjacency lists), node identifiers could be (or even have to be) used
instead of object references.

<!-- ======================================================================= -->
## Option 2: sectioning node -> parent container reference

As a section's parent container can be determined from its sectioning node, the
parent container references could be determined on the fly by taking advantage
of the `Section.sectioningNode` properties (i.e. `sectioningNode` in case of a
type-1, and `sectioningNode.parentNode` in case of a type-2 sectioning node).
That is, if an implementation's environment provides the means to access a
node's parent node (e.g. event driven parsers?).

However, and depending on a specific environment (e.g. low-level implementations
optimized to produce hierarchical listings of section properties on the fly),
the node references of the sectioning nodes are neither required, nor guaranteed
to be valid when the algorithm has to execute the above mentioned loop.

Note that all nodes in the current rooted path of nodes have been entered,
but not yet exited. Therefore, and if an implementation has access to node
references (in contrary to pure node identifiers), the references of those
nodes remain valid for at least until those nodes are exited. This aspect
could turn out to be an issue, if low-level (i.e. pointer-based, no garbage
collection) programming languages or interfaces have to be used. Those have
in general the option to destroy node objects once the nodes have been exited
(e.g. presequent type-2 sectioning nodes). Therefore, an attempt to retrieve
a reference of a section's parent container, via a possibly invalid reference
to the section's sectioning node, could trigger access violation errors.

<!-- ======================================================================= -->
## Option 3: node levels of parent containers

Another option is to use node level values instead. That is, the current section
can be closed, if the node level of an end-marker's parent node is equal to the
node level of the current section's parent container. Otherwise, and because
case-1 and case-3 never apply, the end-marker node is implicitly associated.

In cases where the environment of an implementation does not provide the means
to determine a node's node level, these values have to be determined "manually".
However, the implementation of the tree traversal algorithm does provide the
means to efficiently maintain a "current node level" value. That is, because
it knows exactly when it enters the next node (level+1) and when that node is
being exited (level-1).

The tree traversal algorithm can therefore pass the node level of the current
node on to the corresponding event handler. Consequently, the node level of
the current node does not have to be calculated from scratch by counting the
number of its ancestors. In addition to that, and when creating a new section
object while entering its sectioning node, the node level of its parent
container can be determined and stored inside of section objects:

```
1. Number Section.parentContainerLevel
2. ((currentNodeLevel-1) == section.parentContainerLevel)
```

As mentioned before, such an additional property will increase the memory
footprint of the outline. But, as number values can usually be limited to
a reasonable range of values, those properties would require less memory
than reference properties (e.g. 64-bit in case of references vs. 8- or
16-bit in case of node level values). Because of that, node level properties
could be considered as an acceptable alternative. That is, instead of having
to re-calculate the node level of a section's parent container each time a
subsequent end-marker node is entered.

<!-- ======================================================================= -->
## Option 4-1: node levels of sectioning nodes

(if it *would be* allowed to close type-1 sections)

```
      n0
 ------------
 n1        n2
```

* `n0` is a type-1 sectioning node (declares `s0`)
* `n1` is a type-2 sectioning node (declares `s1`, closes `s0`)
* `n2` is an end-marker node (defined to close `s1`)

For obvious reasons, testing the end-marker's own node reference and the
section's sectioning node reference for equality (because a section object
already has such a property), can not work. That test is guaranteed to always
evaluate to `false`.

However, one might hope that (option-4-1) the node level of the end-marker node
could be compared with the node level of the section's sectioning node, instead
of (option-3) comparing the node level of the end-marker node's parent node with
the node level of the section's parent container (i.e. the section's sectioning
node vs. the section's parent container).

* test-1: `n1` may close `s0` => `if (level(n1) - 1 == level(n0))`
* test-2: `n2` may close `s1` => `if (level(n2) - 0 == level(n1))`

Note that in `if(a - b == c)`, the first value (`a`) represents the end-marker
node's level value, the second value (`b`) a type-dependent adjustment (`b`),
and the third value (`c`) the sectioning node's level value.

Obviously, test-1 is, due to the type-dependent adjustment, not identical to
test-2, which is why additional, type-dependent tests are required in order to
select the appropriate expression. Because of that, the node level of the
sectioning node and the node level of the end-marker node can not be used for
generic, type-independent testing.

Note that options 1-to-3 have a similar issue. That is, in cases 1 and 2, a
reference of the section's type-dependent parent container must be determined
at some point, regardless if that reference is stored with a section object,
or determined on the fly. Similar to that, and in case 3, the type-dependent
node level of the section's parent container must be determined at some point.

<!-- ======================================================================= -->
## Option 4-2: node levels of sectioning nodes

**TODO**
(if it *would not be* allowed to close type-1 sections)

* can these node level values (sectioning node, end-marker node)
  be used directly as generic filters (i.e. without any adjustment)?
* effectively only type-2 sections could be closed
* no additional, type-dependent tests would be required
* either store the sectioning node's node level with the section, or
  recalculate these values if needed (via the `Node.parentNode` property)

if tested for equality, then ...

* an end-marker node can not close a type-1 section
* the corresponding level values would always differ
* an end-marker node could only close a type-2 section, if (and only if)
  that node would be a sibling to it (i.e. same node level)

now that would be really type-independent ...

* (1) the node level of the section's sectioning node can be determined
  without having to know the type of the declared section
* (2) because the node level values can be compared without any adjustment,
  all comparisons may use the same expression, i.e. no type-dependent
  selection of the appropriate expression is required
