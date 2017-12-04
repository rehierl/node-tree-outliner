
<!-- ======================================================================= -->
## Sections, SxN

The common aspect of the above requirements is, that any node must belong to at
least one section. In addition to that, no node can belong to the same section
more than once. Hence, sections can initially be defined as sets of nodes.
Because of that, operators defined for sets can be used on sections:

* `s := {n1,...,nk}`, `s in S`, `ni in N`
* `S` represents the set of sections, `N` the set of nodes
* `(s subset-of N)` is true for any `s in S`
* `(is-empty s)` is true, if `(#s == 0)`
* `#s := k`, `k in [0,#N]`

If node `n` is determined to be associated with section `s`, then node `n` must
be added to section `s` as one of its elements. By itself, this `add` operation
defines a many-to-many (N:M) relation. This relation will be referred to as
"the SxN relation".

* `(s contains ni)` is true, if `(ni in s)`
* `contains` is said to be the the `SxN` relation's semantics.
* `(ni element-of s)` is true, if `(ni in s)`
* synonymous - `element-of`, `belongs-to`, `located-within`, etc.
* `(s related-to ni)` is true, if `(ni in s)`
* `(ni related-to s)` is true, if `(ni in s)`

In principle, an outline algorithm must traverse the node tree in order to visit
and associate each node with at least one section. As a result, the nodes of a
specific section will be added to a section, one after another, in a particular
order. Because of that, sections can also be defined as node sequences:

* `s := [n1,...,nk]`, `s in S`, `ni in N`
* `(ni != nj)` for `i,j in [1,k]` and `(i != j)`
* `n1` is the section's first node, `nk` is the section's last node

Both of the above definitions technically allow to associate any node with
multiple sections. Additional rules are therefore required to uniquely determine
the effective context/location of a node.

<!-- ======================================================================= -->
## Node sequence

The traversal of a tree can be used to create a sequence of nodes (aka. trace
of nodes), if each node is added to a sequence while it is in the process of
being entered. Such a node sequence will be referred to as "the node sequence"
of the corresponding node tree:

* `ns := [n1,...,ni,...,nk]`
* `(k == #N)`, `ns(i) in N`, `ns in N^k`
* `n1` was entered first and `nk` was entered last
* `ni` is entered after `ni-x` and before `ni+y`, `x,y in [1,*]`

Because each node will be entered exactly once, the length of a node sequence
is identical to the number of nodes in the node tree.

* `(ni-k presequent-to ni)` is true, if `k in [1,*]`
* `(ni-k strictly-presequent-to ni)` for `(k == 1)`
* `(ni-k loosely-presequent-to ni)` for `(k > 1)`
* `(ni+k subsequent-to ni)` is true, if `k in [1,*]`
* `(ni+k strictly-subsequent-to ni)` for `(k == 1)`
* `(ni+k loosely-subsequent-to ni)` for `(k > 1)`
* `(ni insequent-to ni)` for any `ni in ns`

Any node that is neither the first nor the last node is said to be subsequent
to the first and presequent to the last node. In addition to that, any node is
said to be insequent (i.e. neither pre- nor subsequent) to itself.

Note also, that each enter and exit event is an atomic operation. That is,
subsequent nodes will neither be entered nor exited, while a presequent node
is still in the process of being entered or exited.

### current knowledge

```
       [ s1    ][ s2  ]
ns := [n1,...,ni,...,nk]
       xxxxxxxxx                - knowledge when ni is entered
              xxxxxxxxx         - maximum scope of enter operations
```

Any outline algorithm must, beginning with a first node, traverse from one node
to another. In addition to that, an algorithm must also execute operations based
on the knowledge it gained from the nodes it has already visited.

Such an algorithm has, when entering its current node `ni`, knowledge
of any node within subsequence `s1 := [n1,ni]`. The algorithm's "current
knowledge" therefore consists of all the nodes within subsequence `s1`.

Those nodes within `s1`, that have already been exited, will in general be
ignored when executing any kind of operation. That is, operations will usually
only depend on the current node itself and on any of its ancestors.

Consequently, no process can make any reasonable decision based upon subsequent
nodes (i.e. nodes in `s2 := [ni+1,nk]`). That is, unless definitions exist
which guarantee that some specific subsequent node, or multiples thereof,
will eventually be entered. In general, such guarantees do not exist (i.e.
no attempts must be made to take any action based on possible future events).

In addition to that, any operation executed while entering a node can only have
an effect on the node itself, or on nodes that are subsequent to it. That is,
if the exit events of its ancestors are ignored.

### exit events

```
                [ s2         ]
                [ s3  ][ s4  ]
ns := [n1,...,ni,...,nj,...,nk]
       xxxxxxxxx                - knowledge when ni is entered
       xxxxxxxxxxxxxxxx         - knowledge when ni is exited
              xxxxxxxxxxxxxxxx  - maximum scope of enter operations
              xx       xxxxxxx  - maximum scope of exit operations
```

Any node within subsequence `s3 := [ni+1,nj]` is descendant to `ni`. These nodes
will be entered and exited after `ni` was entered and before `ni` is exited. In
contrary to that, any node within subsequence `s4 := [nj+1,nk]` will be entered
and exited after `ni` was exited. Hence, node `ni` will be exited after `nj` was
exited and before node `nj+1` is entered.

Consequently, any node within `s3` might technically still have an effect on
its presequent ancestor `ni`. That is, because the outline process will have
knowledge of any node within `s3` by the time `ni` is being exited.

However, this kind of delayed knowledge must not be used to execute any
operation that might have some side effect on any node within `s3`. That is,
because these kind of operations have the potential to produce contradictions.

```
<n1><n2><n3> ... </n3></n2></n1>
```

In addition to that, when executing any operation while a node is being exited,
the overall order of events must be taken into account. That is, ancestor nodes
will be entered before their descendant nodes are entered. In contrary to that,
descendant nodes will be exited before their ancestor nodes are exited. Hence,
compared to enter events, exit events will be executed in reverse order.

Consequently, executing any operation while a node is being exited is per se
problematic. Because of that, exit events must only be used to execute actions
which affect nodes that are subsequent, but not descendant to the node being
exited (i.e. they can affect nodes in `s4`, but must not have any side effect
on any node in `s3`).

<!-- ======================================================================= -->
## Sectioning nodes, NxS

When beginning to traverse a node tree, the set of sections is initially empty.
Certain nodes are therfore required to declare (aka. introduce) new sections.
These type of nodes will be referred to as "sectioning nodes".

**DEFINITION** Any sectioning node always declares a single new section.

* No section can exist without the sectioning node that declared it.
* Any section can be identified by its sectioning node.

Consequently, there is a one-to-one (1:1) relation on the set of sectioning
nodes `SN` and the set of sections `S`. This relation will be referred to as
"the NxS relation".

* for any `sn in SN subset-of N` and for any `s in S`
* `(sn declared s)` is true, if node `sn` declared section `s`
* `(s declared-by sn)` is true, if `(sn declared s)` is true

An algorithm has knowledge of a section as soon as its sectioning node is being
entered. That is, because a sectioning node always (i.e. unconditionally)
declares a new section. And because of that, any new section must be added to
the set of sections `S` as soon as its sectioning node is entered. This set of
sections therefore represents the set of known sections.

In general, and from that point on, any subsequent node must be associated with
the new and any other known section. Consequently, any node potentially belongs
to multiple sections. That is, because any node can be subsequent to any number
of sectioning nodes.

**DEFINITION** A sectioning node does not belong to its own section.

Even though a sectioning node is insequent to itself, it is technically still
possible to associate a sectioning node with the section it declared. That is,
because an algorithm knows about a section as soon as it enters the section's
sectioning node. However, this does not imply that it would be reasonable to
associate a sectioning node with its own section.

Obviously, and as far as possible, an algorithm needs to be able to treat all
sectioning nodes alike. Associating one type of sectioning nodes with their
own section, but not sectioning nodes of another type, would be bad practice.
That is, because this would always make it necessary to add additional, logic
in order to distinguish between those types of nodes.

If any sectioning node would have to be associated with its own section, then
no section would ever be truly empty. That is, because any section would then
always contain at least its own sectioning node. Because of that, additional
logic would be required to determine if a section contains meaningful content
or not. Consequently, sectioning nodes must not be associated with the sections
they declare.

Note that the latter reason is only the easiest to explain reason. As such, it
is also the weakest of them all. More difficult to explain reasons, which have
more impact, will follow.

<!-- ======================================================================= -->
## The root node

Because a section can not exist without a presequent sectioning node, the root
node, with which an algorithm has to begin, can not be associated with any
predeclared section. That is, because there is no sectioning node that is
presequent to the root.

*The universal section (u)*

However, the root node can be thought of as being embedded into some universal
section `u`. This special section can be understood to represent a theoretical,
always available section that contains any tree of nodes.

As such, that universal section must be seen to be declared by some virtual
sectioning node that is presequent to any possible node. As such, the universal
section never ends.

Consequently, any node of any tree therefore belongs to at least the universal
section. Put differently, there can not be any node that does not belong to any
section at all.

*The root node is a sectioning node*

Without any further clarification, and assumed that a given root does itself
not (strictly or loosely) contain any other sectioning node, all the nodes in
the root's subtree would only belong to the universal section. Because of that,
it would in theory not be possible to locate the root's inner nodes inside of
said universal section.

Consequently, the root node must always be seen to declare its own section.
As such, the root must itself be seen to always represent a sectioning node.

<!-- ======================================================================= -->
## States of a section

Similar to output streams, any section has the following states:

*initialized state*

As soon as a sectioning node is known, it is technically possible to associate
any nodes with it. Because of that, and if a section had no delayed start, a
sectioning node would have to be associated with its own section.

Consequently, a section's "initialized" state has the following meaning: (1)
the section is known and (2) an algorithm must start associating nodes with
it at some later point in time.

*open state*

Once a section's first node is entered, this first node and any subsequent node
must be associated with it. An algorithm therefore needs additional rules that
enable it to determine when to begin associating subsequent nodes with a given
section.

A section counts as being "open" as soon as the next subsequent node must be
associated with it.

*closed state*

Any section will eventually end at some point. By default, that point
is reached when the initial/root node of the process is being exited.

This default case is obviously insufficient, because the very last node of
a node sequence would then always have to be associated with all the known
sections. An algorithm therefore needs additional rules that enable it to
determine, before the initial node is being exited, when it is no longer
allowed to associate any subsequent node with a given section.

A section counts as being "closed" as soon as it is no longer allowed to
associate any subsequent node with it. From that point on, a section is
fully defined/specified.

*A section can not be re-opened*

The "closed" state, and the corresponding rules, can therefore also be seen to
represent a guarantee, that a closed section will not change any further at some
later point in time.

This guarantee is critical to an efficient TOC generator, because it allows to
drop a section object once its corresponding section is closed. After that, any
attempt to execute any kind of operation on the dropped section object will issue
an access violation error.

Re-opening a section for additional associations would therefore mean to violate
said guarantee. Because of that, such an operation must be seen to represent an
attempt to suspend and then resume a section.

*It must not be allowed to strictly suspend a section*

Technically, it would be possible to define rules that tell an algorithm to
suspend and then, at some later point in time, resume associating nodes with
a section. However, this does not mean that it would be reasonable to allow
such a operations.

Here, it is assumed that a "resume" operation must always follow a "suspend"
operation ("suspend" would otherwise be equivalent to "close").

Assumed that some section `s` would have to be suspended after some node `ns`
was associated with it and that section `s` would have to be resumed beginning
with some node `nr`. This would in return mean that, in between both nodes (i.e.
`ns` and `nr`), there could potentially be any number of nodes that have are not
intended to have any kind of relationship with section `s` (hence, strictly
suspended).

Because these completely unrelated nodes would then always have to be taken into
account, it would be impossible treat a section as one entity (see requirements).
That is, because such a section would then consist of multiple parts that are
separated from each other. Such a section can be said to have gaps. Consequently,
strict suspend and resume operations as described above must not be allowed.

Because of that, any node, that is located in between a section's first and last
node (i.e. subsequent to the first and presequent to the last node), must belong
to a section.

Note that this does not take the definition of nodes into account, that would be
necessary to clearly define when an algorithm has to strictly suspend and then
resume a given section.

Note that the subsequent part of a strictly suspended section can also be seen
to represent a new/different section. Hence, the nodes that would be required
to tell an algorithm that it has to resume a section can themselves be seen to
represent additional sectioning nodes.
