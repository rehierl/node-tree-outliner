
<!-- ======================================================================= -->
# Design (1)

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
tree. That is, because each node will be entered exactly once. In addition to
that, the node sequence contains each node exactly once.

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
the context of the following discussion, must be allowed to execute any
operation based on possible future events.

### order of nodes

An algorithm must, beginning with some initial root node, traverse the tree from
one node to another. The order in which the nodes are visited must obviously
correspond with the node order of the tree. After all, the algorithm's result is
intended to accurately represent the tree's contents, which includes the correct
order of nodes.

The sequence of enter events is therefore assumed to correspond with the node
order of the tree. Consequently, the same applies to a tree's node sequence.

### executing operations

In order to produce any result, an algorithm must execute certain operations,
which it can only do while entering or exiting nodes.

Note that each enter and exit event is atomic. That is, nodes will neither be
entered nor exited while another node is still in the process of being entered
or exited.

### current knowledge

In order to execute any operation, an algorithm needs to have knowledge that
enables it to decide which operations need to be executed. The knowledge an
algorithm has, while it is entering or exiting a given node, will be referred
to as its "current knowledge".

```
       [ s1    ][ s2  ]
ns := [n1,...,ni,...,nk]
       xxxxxxxxx                - knowledge when ni is entered
              xxxxxxxxx         - maximum scope of enter operations
```

An algorithm has, when entering its current node `ni`, knowledge of any node
within `s1 := [n1,ni]`.

This sequence of nodes contains all the nodes an algorithm has entered until and
including its current node. However, because of an algorithm's current node, an
algorithm's current knowledge also contains nodes that it still needs to exit.

Apart from that, the existence of nodes in `s1` is confirmed. This is obviously
not the case with regards to the subsequent nodes in `s2 := [ni+1,nk]`: These
still need to be entered.

No algorithm can therefore make any reasonable decision based upon nodes that
are subsequent to its current node. That is, unless definitions exist which
guarantee that some specific subsequent node, or multiples thereof, will be
entered eventually. In general, such guarantees do not exist.

In addition to that, any operation executed while entering a node is intended
to only have an effect on the node itself and on nodes that are subsequent to
it. That is, if the exit events of its ancestors are ignored (technically, exit
events allow to affect presequent nodes).

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

Because of that, any node within `s3` can technically still have an effect on
its presequent ancestor `ni`. That is, because a process will have knowledge
of any node within `s3` by the time `ni` is being exited.

However, this delayed knowledge must not be used to execute any operation that
could turn out to have side effects on nodes in `s3`. That is, because these
operations have the potential to produce conflicts.

```
<n1><n2> n3 </n2></n1>
```

In addition to that, when executing any operation while a node is being exited,
the order of events must be taken into account. That is, ancestor nodes will be
entered before their descendant nodes are entered. In contrary to that,
descendants will be exited before their ancestors are exited. Compared to enter
events, exit events will be executed in reverse order.

```
s5 := [n1, n2, n3]
s6 := [n3, n2, n1]
```

Example: If a section would only contain the above three nodes, then associating
these while they are being entered would result in sequence `s5` and associating
them while they are being exited would result in sequence `s6`.

Obviously, the order of nodes in sequence `s6`, does not correspond with the
section's actual order of nodes. That is, this order is in conflict with the
tree's order of nodes.

Consequently, executing any operation while a node is being exited is per se
problematic. Exit events must therefore only be used to execute operations
which only affect nodes that are subsequent, but not descendant to the node
being exited. That is, operations executed while exiting `ni` may only affect
the nodes in `s4`, but must not have any side effect on nodes in `s3`.

<!-- ======================================================================= -->
## Context of a node

In general, the minimal set of data used by an operation is referred to as the
operation's context. And because an operation can not function properly, if any 
data is taken away from its context, the data within its context is considered
to be significant to it. With that in mind, the context of a node can be defined
as follows:

**DEFINITION**
The context of a node, with regards to the execution of an operation, consists
of those nodes that are allowed to have an effect on it.

**CLARIFICATION**
The semantics of a node also depends on its context.

In an undirected tree, the context of a node can only contain the ancestors of
a node. In a directed tree, the context of a node can also contain presequent
siblings (but not their descendants). Note that a context might also include
presequent siblings of the node's ancestors.

The reason why the context of a node in an undirected tree must not contain any
siblings is that, in such a tree, a node has no next and no previous sibling.
That is, there is no guarantee that certain nodes will always be presequent to
a given node. The result of an algorithm, which executes operations in such a
tree, based upon presequent siblings, is therefore not guaranteed to be
deterministic (i.e. repeated executions may yield different results).

Because of that, the current knowledge of an algorithm, is in general not
identical to the context of the current node. That is, because the current
knowledge includes the context of a node and, in addition to that, nodes that
are not part of it (i.e. not all the nodes that are presequent to a node are
allowed to have an effect on it).

Note that even nodes, which were exited, can be allowed to have an effect on
subsequent nodes (e.g. a heading element).

<!-- ======================================================================= -->
## Look ahead

A certain implementation could technically have the ability to cheat the
traversal of a tree by directly examining the tree's structure as soon as a
certain sectioning node is entered. Because of that, an implementation could
simply determine ahead of schedule, if that sectioning node has for example
a 2nd child, a 2nd subsequent sibling, or even a certain ancestor.

The downside of this kind of look ahead would be, that this ability would turn
into a requirement, if it could not be avoided. That is, implementations that
can not support any kind of look ahead (e.g. due to technical limitations),
would become impossible. However, if it is guaranteed to implement an operation
without such an approach, a look ahead could be used as the basis of a more
efficient implementation.

Despite that, a look ahead is an attempt to bypass the current knowledge of what
is guaranteed by the traversal of the tree. As such, a look ahead represents an
attempt to predict future events. Because of that, a design must avoid such an
attempt.

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

In principle, an algorithm must traverse the node tree in order to visit and
associate each node with at least one section. As a result, the nodes of a
section will be added to it, one after another, in a specific order. Because of
that, a section has a first and a last node. Consequently, sections can also be
defined as node sequences:

* `s := [n1,...,nk]`, `s in S`, `ni in N`
* `(ni != nj)` for `i,j in [1,k]` and `(i != j)`
* `n1` is the section's first node, `nk` is the section's last node

Both of these definitions technically allow to associate any node with multiple
sections. Rules are therefore required in order to uniquely determine the actual
context of a node (i.e. its location with regards to the tree's sections).

**DEFINITION**
The scope of a section, respectively the scope of a sectioning node, is the
range of subsequent nodes that are related to it.

The scope of a section therefore begins with the section's first node and ends
with the section's last node. Consequently, any non-empty section has a
non-empty scope. The scope of an empty section is said to be empty. However, an
empty section can also be seen to have no scope at all.

<!-- ======================================================================= -->
## Sectioning nodes, NxS

When beginning to traverse a node tree, the set of sections is initially empty.
Certain nodes are therfore required to declare (aka. introduce) new sections.
This type of nodes will be referred to as "sectioning nodes".

**DEFINITION**
Any sectioning node always declares a single new section.

* No section can exist without the sectioning node that declares it.
* Any section can be identified by its sectioning node.

Consequently, there is a one-to-one (1:1) relation on the set of sectioning
nodes `SN` and the set of sections `S`. This relation will be referred to as
"the NxS relation".

* for any `sn in SN subset-of N` and for any `s in S`
* `(sn declared s)` is true, if node `sn` declared section `s`
* `(s declared-by sn)` is true, if `(sn declared s)` is true

An algorithm has knowledge of a section as soon as its sectioning node is being
entered. That is, because a sectioning node always and unconditionally declares
a new section. Because of that, any new section must be added to the set of
known sections `S` as soon as its sectioning node is being entered.

In general, and from that point on, any subsequent node must be associated with
the new and any other known section. Consequently, any node potentially belongs
to multiple sections. That is, because any node can be subsequent to any number
of sectioning nodes.

**DEFINITION**
A sectioning node does not belong to its own section.

Even though a sectioning node is insequent to itself, it is technically still
possible to associate a sectioning node with the section it declares. That is,
because an algorithm knows about a section as soon as it enters the section's
sectioning node. However, this does not imply that it would be reasonable to
associate a sectioning node with its own section.

Obviously, and as far as possible, an algorithm needs to be able to treat all
sectioning nodes alike. Associating one type of sectioning nodes with their own
section, but not sectioning nodes of another type, would be bad. That is,
because this would require to always add additional logic with regards to the
different types of sectioning nodes.

If any sectioning node would have to be associated with its own section, then
no section would ever be truly empty. That is, because any section would then
always contain at least its own sectioning node. Because of that, additional
logic would be required to determine if a section contains meaningful content
or not.

**TODO**
Note that more reasons will follow, which better explain why sectioning nodes
must not be associated with their own sections. For the moment, it is easier
to simply assume that this is how it has to be.

**CLARIFICATION**
Any sectioning node must be associated with sections that are declared by
presequent sectioning nodes.

**TODO**
descendants, if sibling is first node

<!-- ======================================================================= -->
## The root node

Because a section can not exist without a presequent sectioning node, the root
node, with which an algorithm has to begin, can not be associated with any
predeclared section. That is, because there is no presequent sectioning node
that could declare such a section.

### The universal section (u)

However, the root node can be seen to be embedded into a theoretical universal
section `u`. As such, that universal section must be understood to be declared
by a virtual sectioning node that is presequent to any node. The universal
section must also be seen to never end. Because of that, the universal section
is omnipresent (i.e. any node is in relationship with it).

Consequently, any node of any tree always belongs to at least the universal
section. Put differently, there is in theory no node that does not belong to
any section at all.

**CLARIFICATION**
Any node always belongs to at least one section.

### The root node is a sectioning node

Without any further clarification, and assumed that a tree's root node does
itself not (strictly or loosely) contain any other sectioning node, all the
nodes in the root's subtree would then only belong to the universal section.

Because of that, it would not be possible to locate the nodes of a tree inside
of the universal section. That is, all the nodes would always appear to be lost
inside of the universal section.

Consequently, the root node of a tree must be understood to always declare its
own section. That is especially true, if the initial node is not an arbitrarily
selected node.

**TODO**
what type of sectioning node is the root node?
