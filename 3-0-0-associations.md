
<!-- ======================================================================= -->
# Associations

In general, an outline algorithm is responsible to associate any node within a
tree with one or more sections. Because of that, all nodes within a tree must
be entered and exited in some particular order (=> tree traversal, node sequence).

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

<!-- ======================================================================= -->
## General goals

The most fundamental goal of an outline algorithm is to allow the creation of
a listing of sections that can be found within a tree of nodes (aka. table of
contents, TOC). As such, a TOC provides an accurate, static overview of the
contents found within a tree of nodes.

However, the more sections a tree has, the less helpful a static listing
becomes. An outline algorithm must therefore support dynamic behavior:

(toc -> tree)

* Allow to select an entry within a TOC in order to to jump to the
  corresponding parts within the tree.
* Allow to dynamically change the display of the tree depending on
  which TOC entry was selected (i.e. 

(tree -> toc)

* Allow to determine the context of any given node in order to display and
  update a current location (aka. bread crumbs).
* Allow to dynamically change the TOC of a tree based on a given node
  (i.e. fold distant parts, unfold the current parts).

<!-- ======================================================================= -->
## General process



<!-- ======================================================================= -->
## Associations

The final result of an outline algorithm must allow to determine what the
context of any given node is. Here, the context of a node can be understood
to be the set of those sections with which a node is associated.



Associating a node with a section can be understood as adding a node to a
section.
Whenever a node must be associated with a section, it must be added to a section
as one of its elements, if the node must be
associated with it. As such, a section can initially be seen to represent a set
of nodes. Because of that, operators defined for sets also apply to sections:

* `s := {n1,...,nk}`, `s in S`, `ni in N`
* `#s := k`, `k in [0,#N]`
* `(s subset-of N)`

Technically, the association operation defines an unrestricted, many-to-many
(N:M, SxN) relation. However, no section can be related to the same node more
than once (and vice versa).

* `(s related-to ni)` and `(ni related-to s)`
* `(s contains ni)`, `(ni element-of s)`

<!-- ======================================================================= -->
## Node sequence

The tree traversal process can be used to create a sequence of nodes (aka.
trace of nodes), if each node is added to a sequence while it is being entered.
Such a sequence will be referred to as the tree's node sequence `ns`:

* `ns := [n1,...,ni,...,nk]`
* `(k == #N)`, `ns(i) in N`, `ns in N^k`
* `n1` was entered first and `nk` was entered last
* `ni` was entered after `ni-x`, but before `ni+y`, `x,y in [1,*]`

Because each node is entered exactly once, the length of a node sequence is
identical to the number of nodes in a given tree. Also, any node that is
neither the first nor the last node is said to be subsequent to the first and
presequent to the last node. In addition to that, any node is said to be
insequent (i.e. neither pre- nor subsequent) to itself.

```
       [ s1    ][ s2  ]
ns := [n1,...,ni,...,nk]
       xxxxxxxxx                - knowledge when ni is entered
              xxxxxxxxx         - scope of enter actions
```

The effect of such an order is that any process can only have knowledge
of a node, if that node was already, or is in the process of being entered.
A process that has already entered node `ni` can therefore only have knowledge
of any node in `s1 := [n1,ni]`. In general, nodes within that subsequence, which
have already been exited, will commonly be ignored (i.e. decisions usually only
depend on a node itself and on its ancestors).

Consequently, no process can make any reasonable decision based upon subsequent
nodes (i.e. nodes in `s2 := [ni+1,nk]`). That is, unless definitions exist which
guarantee that some specific subsequent node, or multiples thereof, will
eventually be entered. In general, such guarantees do not exist.

In addition to that, any node can only have an effect on itself or on nodes
that are subsequent to it.

**TODO** must a node be allowed to have an effect on itself?

**exit events**

```
                [ s1  ][ s2  ]
ns := [n1,...,ni,...,nj,...,nk]
       xxxxxxxxx                - knowledge when ni is entered
       xxxxxxxxxxxxxxxx         - knowledge when ni is exited
              xxxxxxxxxxxxxxxx  - scope of enter actions
                        xxxxxx  - scope of exit actions
```

Nodes that are subsequent to some node `ni` represent a subsequence of the node
sequence (i.e. `s := [ni+1,nk]`). These kind of subsequences may begin with
nodes that are descendant to `ni` (i.e. `s1 := [ni+1,nj]`). Any node within `s1`
will be entered and exited after `ni` was entered and before `ni` is exited. In
contrary to that, the remaining other nodes (i.e. `s2 := [nj+1,nk]`) of that
subsequence will be entered and exited after `ni` was exited.

Consequently, any node in `s1` may technically still have an effect on their
common presequent ancestor `ni`. That is because a process does have knowledge
of any node within `s1` by the time `ni` is being exited.

However, this kind of delayed knowledge must not be used to change those
properties of `ni` that have an effect on any nodes in `s1`. That is because
these kind of changes will produce a conflict. In such a case, descendant nodes
depend upon a property that is itself based upon another, subsequent descendant
node (i.e. a causality paradox is created).

Therefore, exit events must only be used for actions which affect nodes that are
subsequent, but not descendant to the node being exited (i.e. nodes in `s2`).

```
<n1><n2><n3> ... </n3></n2></n1>
```

In addition to that, when making any decision while a node is being exited,
the overall order of events must be taken into account. That is, ancestors
will be entered before their descendants are entered. In contrary to that,
descendants will be exited before their ancestors are exited (i.e. exit
events will be triggered in reversed order).
