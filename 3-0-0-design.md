
<!-- ======================================================================= -->
# Associations

This section describes fundamental definitions and considerations.

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

The length of a node sequence is identical to the number of nodes in the node
tree. That is, because each node will be entered exactly once.

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

Note also that each enter and exit event is atomic. That is, nodes will neither
be entered nor exited while a different node is still in the process of being
entered or exited.

### current knowledge

```
       [ s1    ][ s2  ]
ns := [n1,...,ni,...,nk]
       xxxxxxxxx                - knowledge when ni is entered
              xxxxxxxxx         - maximum scope of enter operations
```

Any algorithm must, beginning with some initial node, traverse from one node to
another. In addition to that, an algorithm can only execute operations based on
the knowledge it gained from the nodes it has already visited.

Such an algorithm therefore has, when entering its current node `ni`, knowledge
of any node within the subsequence `s1 := [n1,ni]`. The algorithm's "current
knowledge" at that point in the process consists of all the nodes within
subsequence `s1`.

Consequently, no process can make any reasonable decision based upon subsequent
nodes (i.e. nodes within `s2 := [ni+1,nk]`). That is, unless definitions exist
which guarantee that some specific subsequent node, or multiples thereof, will
eventually be entered. In general, such guarantees do not exist. Because of that,
no attempt must be made to execute operations based on possible future events.

In addition to that, any operation executed while entering a node is intended
to only have an effect on the node itself and on nodes that are subsequent to
it. That is, if the exit events of its ancestors are ignored.

### exit events

```
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
and exited after `ni` was exited. Thus, node `ni` will be exited in between the
exit event of `nj` and the enter event of `nj+1`.

Consequently, any node within `s3` can technically still have an effect on its
presequent ancestor `ni`. That is, because a process will have knowledge of any
node within `s3` by the time `ni` is being exited.

However, this kind of delayed knowledge must not be used to execute any kind
of operation that could have some side effect on a node inside `s3`. That is,
because these kind of operations have the potential to produce conflicts
(see - associating nodes while exiting).

```
<n1><n2><n3> ... </n3></n2></n1>
```

In addition to that, when executing any operation while a node is being exited,
the overall order of events must be taken into account. That is, ancestor nodes
will be entered before their descendant nodes are entered. In contrary to that,
descendant nodes will be exited before their ancestor nodes are exited. Compared
to enter events, exit events will be executed in reverse order.

Consequently, executing any operation while a node is being exited is per se
problematic. Exit events must therefore only be used to execute actions which
can only have an effect on nodes that are subsequent, but not descendant to the
node being exited. That is, operations executed while exiting `ni` are only
allowed to have an effect on the nodes in `s4`, but must not have any side
effect on any node in `s3`.

<!-- ======================================================================= -->
## Context of a node

In general, the minimal set of data used by an operation is referred to as the
operation's context. And because an operation can not function properly, if any 
data is taken away from its context, the data within it is considered to be
significant to the operation. With that in mind, the context of a node can be
defined:

**DEFINITION**
The context of a node, with regards to the execution of operations,
consists of those nodes that are intended to have an effect on said node.

**CLARIFICATION**
The semantics of a node also depends on a node's context.

In an undirected tree, the context of a node can only contain the ancestors of
a node. In a directed tree, the context of a node also contains any presequent
siblings (but not their descendants). Note that this also includes all the
presequent siblings of its ancestors.

The reason as to why the context of a node in an undirected tree must not contain
any siblings is that, in such a tree, a node has no next and no previous sibling.
That is, there is no guarantee that certain nodes will always be presequent to a
given node. The result of an algorithm, that executes operations in such a tree
which are based upon presequent siblings, is therefore not guaranteed to be
deterministic. That is, repeated executions can yield different results.

Because of that, the current knowledge an algorithm has when traversing a tree
of nodes and when entering a specific node, is in general not identical to the
context of the current node. That is, because the current knowledge includes
the context of a node and also nodes that are not part of it (i.e. not all the
nodes that are presequent to a node are allowed to have an effect on it).

In general, those nodes within subsequence `s1`, that have already been exited,
will be ignored when executing an operation. That is, operations may in general
only depend on the current node itself, on its ancestors and any of its
presequent siblings.

<!-- ======================================================================= -->
## Sections, SxN

**DEFINITION**
A section is a set of nodes.

The common aspect of the initially mentioned requirements is, that any node must
belong to at least one section. In addition to that, no node can belong to the
same section more than once. Hence, sections can initially be defined as sets of
nodes:

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

**DEFINITION**
A section is a sequence of nodes.

In principle, an outline algorithm must traverse the node tree in order to visit
and associate each node with at least one section. As a result, the nodes of a
specific section will be added to a section, one after another, in a particular
order. Because of that, sections can also be defined as node sequences:

* `s := [n1,...,nk]`, `s in S`, `ni in N`
* `(ni != nj)` for `i,j in [1,k]` and `(i != j)`
* `n1` is the section's first node, `nk` is the section's last node

Both of these definitions technically allow to associate any node with multiple
sections. Rules are therefore required in order to uniquely determine the actual
context of a node (i.e. the node's location with regards to the sections of a
node tree).

**DEFINITION**
The scope of a section, respectively the scope of a sectioning node, is the
range of subsequent nodes that must be associated with a section.

The scope of a section therefore begins with the section's first node and ends
with the section's last node. Consequently, any non-empty section has a
non-empty scope.

The scope of an empty section is therefore said to be empty. However, an empty
section can also be seen to have no scope at all.

<!-- ======================================================================= -->
## Sectioning nodes, NxS

When beginning to traverse a node tree, the set of sections is initially empty.
Certain nodes are therfore required to declare (aka. introduce) new sections.
These type of nodes will be referred to as "sectioning nodes".

**DEFINITION**
Any sectioning node always declares a single new section.

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
the set of sections `S` as soon as its sectioning node is being entered. This
set of sections therefore represents the set of known sections.

In general, and from that point on, any subsequent node must be associated with
the new and any other known section. Consequently, any node potentially belongs
to multiple sections. That is, because any node can be subsequent to any number
of sectioning nodes.

**CLARIFICATION**
A sectioning node does not belong to its own section.

Even though a sectioning node is insequent to itself, it is technically still
possible to associate a sectioning node with the section it declared. That is,
because an algorithm knows about a section as soon as it enters the section's
sectioning node. However, this does not imply that it would be reasonable to
associate a sectioning node with its own section.

Obviously, and as far as possible, an algorithm needs to be able to treat all
sectioning nodes alike. Associating one type of sectioning nodes with their own
section, but not sectioning nodes of another type, would be bad practice. That
is, because this would always make it necessary to add additional logic in order
to distinguish between the different types of sectioning nodes.

If any sectioning node would have to be associated with its own section, then
no section would ever be truly empty. That is, because any section would then
always contain at least its own sectioning node. Because of that, additional
logic would be required to determine if a section contains meaningful content
or not.

Sectioning nodes must therefore not be associated with the sections they declare.

**TODO**
More reasons will follow, that better explain why sectioning nodes must not be
associated with the sections they declare.

<!-- ======================================================================= -->
## The root node

Because a section can not exist without a presequent sectioning node, the first
node, with which an algorithm has to begin, can not be associated with any
predeclared section. That is, because there is no sectioning node in the current
process which is presequent to this initial node.

*The universal section (u)*

However, the first node can be seen to be embedded into some virtual universal
section `u`. As such, that universal section must be understood to be declared
by some virtual sectioning node that is presequent to any possible node. In
addition to that, the universal section must be seen to never end. Because of
that, the universal section must be seen to be omnipresent.

Consequently, any node of any tree always belongs to at least the universal
section. Put differently, there is no node that does not belong to any section
at all. That is, any node always belongs to at least one section.

*The root node acts as a sectioning node*

Without any further clarification, and assumed that a tree's root node does
itself not (strictly or loosely) contain any other sectioning node, all the
nodes in the root's subtree would only belong to the universal section.

Because of that, it would not be possible to locate the nodes of a tree inside
of the universal section. That is, all the nodes would always appear lost inside
of the universal section.

Consequently, the root node of a tree must be understood to declare its own
section. As such, the root node of a tree always represents a sectioning node.

<!-- ======================================================================= -->
## States of a section

Similar to output streams, any section has the following states:

*initialized state*

As soon as a sectioning node is known, it is technically possible, beginning
with the current node, to associate any subsequent node with it. Because of
that, and if a section had no delayed start, a sectioning node would have to
be associated with its own section.

Consequently, a section's "initialized" state has the following meaning: (1)
the section is known and (2) an algorithm must start associating nodes with
it at some later point in time.

*open state*

Once a section's first node is entered, this first node and any subsequent node
must be associated with it. An algorithm therefore needs additional rules that
enable it to determine when to begin associating nodes with a given section.

A section counts as being "open" as soon as the next subsequent node must be
associated with it.

*closed state*

Any section must eventually end at some point. By default, that point
is reached when the initial/root node of the process is being exited.

This default case is obviously insufficient, because the very last node of
a node sequence would then always have to be associated with all the known
sections. An algorithm therefore needs additional rules that enable it to
determine, before the initial node is being exited, when it is no longer
allowed to associate any subsequent node with a given section.

A section counts as being "closed" as soon as it is no longer allowed to
associate any more nodes with it. From that point on, a section is fully
defined/specified. That is, because no subsequent node is allowed to modify
a section that counts as being closed.

*A section can not be re-opened*

The "closed" state, and the corresponding rules, can therefore also be seen to
represent a guarantee, that a closed section will not change any further at some
later point in time.

This guarantee is critical to an efficient TOC generator, because it allows to
drop a section object once its corresponding section is closed and once the
required information has been read from it. After that, any attempt to execute
any kind of operation on the dropped section object will issue an access
violation error.

Re-opening a section for additional associations would therefore mean to violate
the above guarantee. Because of that, such an operation must be seen to represent
an attempt to suspend and then resume a section.

*It must not be allowed to strictly suspend a section*

Technically, it would be possible to define rules that tell an algorithm to
suspend and then, at some later point in time, resume associating nodes with
a section. However, this does not mean that it would be reasonable to allow
such operations.

Note that it is assumed, that a "resume" operation must always follow a
"suspend" operation ("suspend" would otherwise be equivalent to "close").

Assumed that some section `s` would have to be suspended after some node `ns`
was associated with it and that section `s` would have to be resumed beginning
with some node `nr`. This would in return mean that, in between both nodes (i.e.
`ns` and `nr`), there could potentially be any number of nodes that have are not
intended to have any kind of relationship with section `s` (hence, strictly
suspended).

Because these completely unrelated nodes would then always have to be taken into
account, it would be impossible treat a section as one entity (see requirements).
That is, because such a section would then consist of multiple parts that are
separated from each other. Because of that, such a section can be said to have
gaps. Consequently, strict suspend and resume operations as described above must
not be allowed.

Because of that, any node, that is located in between a section's first and last
nodes (i.e. subsequent to the first and presequent to the last node), must belong
to a section.

Note that this does not take the definition of nodes into account, that would
be necessary to clearly define when an algorithm has to strictly suspend and
then resume a given section.

Note that the subsequent part of a strictly suspended section can also be seen
to represent a new/different section. Hence, the nodes that would be required
to tell an algorithm that it has to resume a section can themselves be seen to
represent sectioning nodes.
