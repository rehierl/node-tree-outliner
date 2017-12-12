
<!-- ======================================================================= -->
# Associations

This section describes fundamental definitions and considerations.

<!-- ======================================================================= -->
## Node sequence

The traversal of a tree can be used to create a sequence of nodes (aka. trace
of nodes), if each node is added to a sequence while it is in the process of
being entered. Such a node sequence will be referred to as "the node sequence"
of the corresponding tree:

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

Any node, that is neither the first nor the last node, is said to be subsequent
to the first and presequent to the last node. In addition to that, any node is
said to be insequent (i.e. neither pre- nor subsequent) to itself.

Note that the term "subsequent" can be seen to focus on possible future events.
In contrary to that, the term "presequent" needs to be seen to focus on known
past events. This switch in perspective is critical, because no algorithm, in
the context of this discussion, must be allowed to execute any operation based
on possible future events.

Note also that each enter and exit event is atomic. That is, nodes will neither
be entered nor exited while a different node is still in the process of being
entered or exited.

### order of nodes

An algorithm must, beginning with some initial root node, traverse from one
node to another. Obviously, the order in which the nodes of a tree are visited
is not arbitrary. That is, because it must reflect the node order of the tree.

(How else is an algorithm supposed to produce a result, that is intended
to accurately represent the contents of a tree?)

**CLARIFICATION**
The sequence of enter events corresponds with a tree's order of nodes.
Because of that, the same applies to the node sequence of a tree.

### current knowledge

```
       [ s1    ][ s2  ]
ns := [n1,...,ni,...,nk]
       xxxxxxxxx                - knowledge when ni is entered
              xxxxxxxxx         - maximum scope of enter operations
```
An algorithm can only execute operations based on the knowledge it gained
from the nodes it has already visited. Such an algorithm therefore has, when
entering its current node `ni`, knowledge of any node within subsequence
`s1 := [n1,ni]`.

**DEFINITION**
An algorithm's "current knowledge" consists of its current node and all the
nodes that are presequent to it.

This set of nodes therefore contains all the nodes an algorithm has entered
until and including its current node. However, because of an algorithm's
current node, an algorithm's current knowledge also contains nodes that it
still has to exit.

No algorithm can make any reasonable decision based upon nodes that are
subsequent to its current node (i.e. those within `s2 := [ni+1,nk]`) -
it still has to enter these. That is, unless definitions exist which
guarantee that some specific subsequent node, or multiples thereof,
will eventually be entered. In general, such guarantees do not exist.

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
and exited after `ni` was exited. Hence, node `ni` will be exited in between the
exit event of `nj` and the enter event of `nj+1`.

Consequently, any node within `s3` can technically still have an effect on its
presequent ancestor `ni`. That is, because a process will have knowledge of any
node within `s3` by the time `ni` is being exited.

However, this delayed knowledge must not be used to execute any kind of operation
that could turn out to have side effects on nodes in `s3`. That is, because these
kind of operations have the potential to produce conflicts.

```
<n1><n2> n3 </n2></n1>
```

In addition to that, when executing any operation while a node is being exited,
the overall order of events must be taken into account. That is, ancestor nodes
will be entered before their descendant nodes are entered. In contrary to that,
descendant nodes will be exited before their ancestor nodes are exited. Compared
to enter events, exit events will be executed in reverse order.

```
s5 := [n1, n2, n3]
s6 := [n3, n2, n1]
```

Example: If a section would only contain the above three nodes, then associating
these while they are being entered would result in sequence `s5` and associating
them while they are being exited would result in sequence `s6`. Obviously, the
order of nodes, that is reflected by sequence `s6`, does not correspond with the
section's actual order of nodes. That is, because this order is in conflict with
the tree's node order.

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
defined as follows:

**DEFINITION**
The context of a node, with regards to the execution of an operation,
consists of those nodes that are allowed to have an effect on it.

**CLARIFICATION**
The semantics of a node also depends on its context.

In an undirected tree, the context of a node can only contain the ancestors of
a node. In a directed tree, the context of a node also contains any presequent
siblings (but not their descendants). Note that this also includes all the
presequent siblings of its ancestors.

The reason as to why the context of a node in an undirected tree must not contain
any siblings is that, in such a tree, a node has no next and no previous sibling.
That is, there is no guarantee that certain nodes will always be presequent to a
given node. The result of an algorithm, that executes operations in such a tree,
which are based upon presequent siblings, is therefore not guaranteed to be
deterministic. That is, repeated executions can yield different results.

Because of that, the current knowledge an algorithm has is in general not
identical to the context of the current node. That is, because the current
knowledge includes the context of a node and also nodes that are not part
of it (i.e. not all the nodes that are presequent to a node are allowed to
have an effect on it).

In general, those nodes within subsequence `s1`, that have already been exited,
will be ignored when executing an operation. That is, operations may in general
only depend on the current node itself, on its ancestors and any of its
presequent siblings.

<!-- ======================================================================= -->
## Sections, SxN

**DEFINITION**
A section is a set of nodes.

The common aspect of the initially mentioned requirements is that any node must
belong to at least one section. In addition to that, no node can belong to the
same section more than once. Hence, sections can initially be defined as sets
of nodes:

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
context of a node (i.e. the node's location with regards to the tree's sections).

**DEFINITION**
The scope of a section, respectively the scope of a sectioning node,
is the range of subsequent nodes that are related to it.

The scope of a section therefore begins with the section's first node and
ends with the section's last node. Consequently, any non-empty section has
a non-empty scope.

The scope of an empty section is therefore said to be empty.
However, an empty section can also be seen to have no scope at all.

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
declares a new section. Because of that, any new section must be added to the
set of known sections `S` as soon as its sectioning node is being entered.

In general, and from that point on, any subsequent node must be associated with
the new and any other known section. Consequently, any node potentially belongs
to multiple sections. That is, because any node can be subsequent to any number
of sectioning nodes.

**CLARIFICATION**
A sectioning node does not belong to its own section.

Even though a sectioning node is insequent to itself, it is technically still
possible to associate a sectioning node with the section it declares. That is,
because an algorithm knows about a section as soon as it enters the section's
sectioning node. However, this does not imply that it would be reasonable to
associate a sectioning node with its own section.

Obviously, and as far as possible, an algorithm needs to be able to treat all
sectioning nodes alike. Associating one type of sectioning nodes with their own
section, but not sectioning nodes of another type, would be bad practice. That
is, because this would always make it necessary to add additional logic in order
to account for the different types of sectioning nodes.

If any sectioning node would have to be associated with its own section, then
no section would ever be truly empty. That is, because any section would then
always contain at least its own sectioning node. Because of that, additional
logic would be required to determine if a section contains meaningful content
or not.

Sectioning nodes must therefore not be associated with the sections they declare.

**TODO**
Note that more reasons will follow, which better explain why sectioning nodes
must not be associated with their own sections. For the moment, it is easier
to simply assume that this is how it has to be.

<!-- ======================================================================= -->
## The root node

Because a section can not exist without a presequent sectioning node, the
root node, with which an algorithm has to begin, can not be associated with
any predeclared section. That is, because there is no sectioning node which
is presequent to this first node.

*The universal section (u)*

However, the root node can be seen to be embedded into some virtual universal
section `u`. As such, that universal section must be understood to be declared
by some virtual sectioning node that is presequent to any possible node. In
addition to that, the universal section must be seen to never end. Because of
that, the universal is omnipresent.

Consequently, any node of any tree always belongs to at least the universal
section. Put differently, there practically is no node that does not belong
to any section at all. That is, any node always belongs to at least one section.

*The root node acts as a sectioning node*

Without any further clarification, and assumed that a tree's root node does
itself not (strictly or loosely) contain any other sectioning node, all the
nodes in the root's subtree would only belong to the universal section.

Because of that, it would not be possible to locate the nodes of a tree inside
of the universal section. That is, all the nodes would always appear lost inside
of the universal section.

Consequently, the root node of a tree must be understood to declare its own
section. As such, the root node of a tree always represents a sectioning node.

**TODO**
what type of sectioning node is the root node?
