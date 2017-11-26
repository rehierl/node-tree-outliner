
<!-- ======================================================================= -->
## General goals

The most fundamental goal of an outline algorithm is to allow the generation
of an accurate listing of sections (aka. table of contents, TOC) that can be
found within a given node tree.

As such, a TOC provides a static overview of the contents. However,
the more sections there are, the less helpful such a listing becomes.
An outline algorithm must therefore allow to support dynamic behavior.

An outliner must allow to influence the display of a TOC based on actions
executed on a tree's display (i.e. tree -> toc):

* Allow to determine the context of any given node in order to display and
  update a current location (aka. bread crumbs). The current location is a
  minimalistic display of information based upon the corresponding TOC.
* Allow to dynamically change the TOC of a tree based upon a given node
  (i.e. unfold/show local parts, fold/hide distant parts).

An outliner must allow to influence the display of a tree based on actions
executed on a TOC's display (i.e. toc -> tree):

* Allow to focus on a section of a tree based on the selection of a TOC entry.
* Allow to dynamically change the display of the tree depending on which TOC
  entry was selected (i.e. unfold/show parts that are within the current
  context and fold/hide parts that are outside it).

An outliner must allow to manually influence the display of a tree based on
actions executed on the display of a tree (i.e. tree -> tree):

* Allow to trigger events by performing an action on a section's representative.
  This will allow to fold/unfold the corresponding section, or multiples thereof.

In order to support these dynamic goals, certain requirements must be met:

* Any node within a tree must belong to one or more sections.
  This requirement is needed in order to determine the context of any node.
* It must be possible to localize a section within a tree, even if it is empty.
  This requirement is needed in order to focus on any given section.
* It must be possible to treat a section as one entity. This requirement is
  needed in order to fold/unfold whole sections via a single operation.

<!-- ======================================================================= -->
## Sections

The most fundamental aspect of the above requirements is, that any node must
belong to one or more sections. As a result, any section can initially be
defined as a set of nodes. Because of that, operators defined for sets also
apply to sections:

* `s := {n1,...,nk}`, `s in S`, `ni in N`
* `S` represents the set of sections, `N` the set of nodes
* `#s := k`, `k in [0,#N]`
* `(s subset-of N)` for any `s in S`

A node `n` must be added to section `s`, if it must be associated with it. This
`add` operation itself defines an unrestricted, many-to-many (N:M, SxN) relation.

* `(s contains ni)` is true, if `(ni in s)`
* `contains` is said to be the the `SxN` relation's semantics.
* `(ni element-of s)` is true, if `(ni in s)`
* synonymous - `element-of`, `belongs-to`, `located-within`, etc.
* `(s related-to ni)` is true, if `(ni in s)`
* `(ni related-to s)` is true, if `(ni in s)`

Consequently, an outline algorithm must traverse the node tree in order to
visit and associate each and every node. As a result, the nodes of a section
will be added to it in some particular order, which is based upon the traversal
of the node tree. A section can therefore be defined as a sequence of nodes:

* `s := [n1,...,nk]`, `s in S`, `ni in N`
* `(ni != nj)` for `i,j in [1,k]` and `(i != j)`
* `n1` is the section's first node, `nk` is the section's last node

Despite the definition as a sequence of nodes, no node must be added more than
once to any section. Hence, the set operators stilly apply.

**TODO** -
no node can be added to more than one section

<!-- ======================================================================= -->
## Node sequence

A tree traversal can be used to create a sequence of nodes (aka. trace of nodes),
if each node is added to a sequence while it is in the process of being entered.

Note that each enter and exit event is an atomic operation. That is, a subsequent
node will not be entered or exited, while a presequent node is still being
entered or exited.

Such a node sequence will be referred to as the node sequence `ns` of the
corresponding node tree:

* `ns := [n1,...,ni,...,nk]`
* `(k == #N)`, `ns(i) in N`, `ns in N^k`
* `n1` was entered first and `nk` was entered last
* `ni` was entered after `ni-x`, but before `ni+y`, `x,y in [1,*]`

Because each node will be entered exactly once, the length of a node sequence
is identical to the number of nodes in the corresponding tree of nodes. Also,
any node that is neither the first nor the last node is said to be subsequent
to the first and presequent to the last node. In addition to that, any node
is said to be insequent (i.e. neither pre- nor subsequent) to itself.

```
       [ s1    ][ s2  ]
ns := [n1,...,ni,...,nk]
       xxxxxxxxx                - knowledge when ni is entered
              xxxxxxxxx         - maximum scope of enter actions
```

The effects of such a sequence is such that any process, that executed
actions based upon this kind of order can only depend on a node, if that node
was already, or is in the process of being entered. A process that has already
entered node `ni` can therefore only have knowledge of any node within
`s1 := [n1,ni]`. The nodes within subsequence `s1`, that have already been
exited, will generally be ignored. That is, decisions and actions will usually
only depend on a node itself and/or on its ancestors.

Consequently, no process can make any reasonable decision based upon subsequent
nodes (i.e. nodes in `s2 := [ni+1,nk]`). That is, unless definitions exist
which guarantee that some specific subsequent node, or multiples thereof, will
eventually be entered. In general, such guarantees do not exist (i.e. you must
not attempt to make decisions based on possible future events).

In addition to that, any action executed while entering a node can only have an
effect on the node itself, or on nodes that are subsequent to it. That is, if
exit events are ignored.

**TODO** -
can a node be allowed to have any effect on itself
(e.g. associate with its own section)?

### exit events

```
                [ s1  ][ s2  ]
ns := [n1,...,ni,...,nj,...,nk]
       xxxxxxxxx                - knowledge when ni is entered
       xxxxxxxxxxxxxxxx         - knowledge when ni is exited
              xxxxxxxxxxxxxxxx  - maximum scope of enter actions
                     xxxxxxxxx  - maximum scope of exit actions
```

Any node within subsequence `s1 := [ni+1,nj]` is descendant to `ni` and will
be entered and exited after `ni` was entered and before `ni` is exited. In
contrary to that, any node within subsequence `s2 := [nj+1,nk]` will be entered
and exited after `ni` was exited.

Consequently, any node within `s1` may technically still have an effect on its
presequent ancestor `ni`. That is because a process will have knowledge of any
node within `s1` by the time `ni` is being exited.

However, this kind of delayed knowledge must not be used to execute any actions
that may have a side effect on any nodes in `s1`. That is because these kind of
operations will produce a causality paradox (e.g. associate nodes while exiting).

Therefore, exit events must only be used for actions which affect nodes that are
subsequent, but not descendant to the node being exited (i.e. they can affect
nodes in `s2`, but must not have any side effect on any nodes in `s1`).

```
<n1><n2><n3> ... </n3></n2></n1>
```

In addition to that, when making any decision while a node is being exited,
the overall order of events must be taken into account. That is, ancestors
will be entered before their descendants are entered. In contrary to that,
descendants will be exited before their ancestors are exited (i.e. exit
events will be executed in reversed order).

<!-- ======================================================================= -->
## Sectioning nodes

```
             [ s1  ][ s2  ][ s3  ][ s4  ][ s5  ]
ns := [...,ni,...,nj,...,nk,...,nl,...,nm,...,nn,...]
           xxxxxxxxxxxxxxxx  - scope of ni enter actions
                  xxxxxxxxx  - scope of ni exit actions
```

<!-- ======================================================================= -->
# Associations

At some point in this process, nodes will eventually be entered that declare
(aka. introduce) the existence of a new section (=> sectioning nodes).

* Any sectioning node always declares a single new section.
* That is, there is a one-to-one (1:1, NxS) relation (i.e. `(n declares s)`)
  on the set of sectioning nodes and the set of sections.
* Any section can be identified by its sectioning node.
* There is no knowledge of a section before its sectioning node is entered.
* No section can exist without first being declared by some sectioning node.

In general, if node `x` declares section `s`, then any node
`(y subsequent-to x)` must be associated with that section `s`.

* A sectioning node is insequent and therefore not subsequent to itself.
* However, it is technically still possible to associate a sectioning node
  with the section it declares. That is because a section's existence is
  obvious as soon as its sectioning node is entered.
* A node must potentially be associated with multiple sections, if it is
  subsequent to multiple presequent sectioning nodes.

Certain rules are required that allow to determine when no more associations
with certain sections are allowed. Without such rules, the last node entered
would have to be associated with all declared sections.

* Sections must have an open-or-closed state.
* Nodes can be associated with a section, if a section is open.
* No more associations are allowed, if a is closed.
* A section is fully defined once it is closed.
