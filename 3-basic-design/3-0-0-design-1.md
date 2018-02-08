
<!-- ======================================================================= -->
# Design (1) - node sequence

The traversal of a tree can be used to create a sequence of nodes (aka. trace
of nodes), if each node of the tree's set of nodes `N` is added to a sequence
while it is being entered. This node sequence will be referred to as "the node
sequence" of the tree:

* `ns := [n1,...,ni,...,nk]`
* `(k == #N)`, `ns(i) in N`, `ns in N^k`
* `n1` was entered first and `nk` was entered last
* `ni` is entered after `ni-x` and before `ni+y`, `x,y in [1,k]`

Note that `x,y in [1,k]` is not accurate because the range of numbers (i.e.
`[1,k]`) is too large. In order to keep the explanations simple, think of
that range specification to only contain those values that are allowed.

The length of a node sequence is identical to the number of nodes in the node
tree. That is, because each node will be entered exactly once. Because of that,
the node sequence contains each node exactly once.

* `(ni+k subsequent-to ni)` is true, if `k in [1,*]`
* `(ni+k strictly-subsequent-to ni)`, if `(k == 1)`
* `(ni+k loosely-subsequent-to ni)`, if `(k > 1)`
* `(ni-k presequent-to ni)` is true, if `k in [1,*]`
* `(ni-k strictly-presequent-to ni)`, if `(k == 1)`
* `(ni-k loosely-presequent-to ni)`, if `(k > 1)`
* `(ni insequent-to ni)` for any `i in [1,k]`

Any node, that is neither the first nor the last node, is said to be subsequent
to the first and presequent to the last node. In addition to that, any node is
said to be insequent (i.e. neither pre- nor subsequent) to itself.

Note that the term "subsequent" can be seen to focus on possible future events.
That is, because the node `ni+k`, which is referred to, is entered after the
corresponding current node `ni`. In contrary to that, the term "presequent"
needs to be understood to focus on known past events. This switch in perspective
is critical because no algorithm, in the context of the following discussion,
can execute any operation based nodes that still need to be entered (therefore:
possible future events).

### order of nodes

An algorithm must, beginning with some initial node, traverse a tree from one
node to another and in the tree's order of nodes. After all, the algorithm's
result is intended to accurately represent the contents of the tree, which
obviously must include the tree's order of nodes.

Because of that, the tree traversal's sequence of enter events is understood
to correspond with the tree's node order. Consequently, the node order of a
tree's node sequence is understood to represent the node order of the tree.

### executing operations

In order to produce any result, an algorithm must execute certain operations,
which it can only do while entering or exiting a node.

Note that each enter and exit event is atomic. That is, nodes will neither be
entered nor exited while another node is still in the process of being entered
or exited.

### current knowledge

In order to execute any operation, an algorithm needs to have knowledge that
it can use to decide which operations it has to execute. The knowledge an
algorithm has, while it is entering or exiting a given node, will be referred
to as the algorithm's "current knowledge".

```
       [ s1    ][ s2  ]
ns := [n1,...,ni,...,nk]
       xxxxxxxxx         - knowledge when ni is entered
              xxxxxxxxx  - maximum scope of enter operations
```

An algorithm has, when entering its current node `ni`, knowledge of any node
within `s1 := [n1,ni]`. That is, because it has already entered the nodes in
that sequence.

However, because of an algorithm's current node, an algorithm's current
knowledge also contains those nodes that it will still have to exit at some
later point in time. That is, because the algorithm will still have to exit
the current node and all of its ancestors.

Apart from that, the existence of those nodes in `s1` is guaranteed.
This is obviously not the case with regards to the subsequent nodes in
`s2 := [ni+1,nk]`: These still need to be entered.

No algorithm can therefore make any reasonable decision based upon nodes that
are subsequent to its current node. That is, unless definitions exist which
guarantee that some specific subsequent node will be entered eventually. In
general, such guarantees do not exist.

Note that, even if such a guarantee would exist, relying on that kind of
guarantee makes it necessary to add additional logic in order to deal with
trees that do not comply with the corresponding rules (i.e. input/user errors).

In addition to that, any operation executed while entering a node is intended
to only have an effect on the node itself and/or on nodes that are subsequent
to it. That is, if the exit events of its ancestors are ignored (technically,
exit events allow to affect presequent nodes).

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
operations have the potential to produce conflicting statements.

```
<n1> <n2> </n2> <n3> </n3> </n1>
```

In addition to that, when executing any operation while a node is being exited,
the order of events must be taken into account. That is, ancestor nodes will be
entered before their descendant nodes are entered. In contrary to that,
descendants will be exited before their ancestors are exited. Consequently, and
compared to enter events, exit events will be executed in reversed order.

```
s5 := [n1, n2, n3]
s6 := [n2, n3, n1]
```

If a section would only contain the above three nodes, then associating
these while they are being entered would result in the node sequence `s5` and
associating them while they are being exited would result in sequence `s6`.

Obviously, the node order in sequence `s6`, does not correspond with the node
order of the tree, sequence `s5` however does. Because of that, and if those
three nodes would be the only nodes of a section, sequence `s6` can not be
used to accurately represent the contents of said section.

Consequently, executing any operation while a node is being exited is in
principle problematic. Exit events must be used to execute operations which
only affect those nodes that are subsequent, but not descendant to the node
being exited. That is, operations executed while exiting `ni` may only affect
those nodes in `s4`, but must not have any side effect on any node in `s3`.

<!-- ======================================================================= -->
## the context of a node

In general, the minimal set of data used by an operation can be referred to as
the context of an operation. And because an operation can not function properly,
if any data is taken away from its context (minimal set), the data within its
context is considered to be significant to it (see also en.wikipedia.org:
Context (computing), Operational context, Operating context).

**CLARIFICATION**
Operations executed during an event are in general only allowed to have any
effect on those nodes that are subsequent (forwards) to the corresponding event.
In addition to that, operations can only rely on those nodes that are presequent
(backwards) to the event in question.

Note that a node is presequent to its own exit event. That is, because "a node"
corresponds with the node's enter event.

**DEFINITION**
The context of a node, with regards to the execution of an operation, consists
of those nodes that are allowed to have an effect on it.

Note that this definition technically allows a node to have an effect on itself.
The question is, whether that would even be reasonable.

**CLARIFICATION**
The semantics of a node depends on its context.

In an unordered tree, the context of a node can only contain the ancestors
of a node. That is, because there is no guarantee that certain nodes will
always be presequent to a given node. The result of an algorithm, which
executes operations based upon presequent siblings, is not guaranteed to
be deterministic (i.e. repeated executions may yield different results).

In an ordered tree, the context of a node may obviously contain presequent
siblings. Note that the descendants of those siblings are not included as
they need to be understood to be locked up (i.e. sandboxed) inside of those
siblings. Note also that the context of a node may include those siblings
that are presequent to one of the node's ancestors.

Because of that, the current knowledge of an algorithm, is in general not
identical to the context of the current node. That is, because the current
knowledge includes the context of a node and, in addition to that, nodes
which are not part of it (i.e. not all nodes that are presequent to a node
are allowed to have an effect on it).

Note that even those nodes, which were exited, can be allowed to have an
effect on subsequent nodes (e.g. presequent siblings).

<!-- ======================================================================= -->
## look ahead

An implementation could technically have the ability to cheat the traversal of a
tree by directly examining the tree's structure when a certain node is entered.
Because of that, an implementation could simply determine ahead of schedule, if
that node has child nodes or a next sibling.

The downside of this kind of look ahead would be, that this ability would turn
into a necessity, if it could not be avoided. That is, implementations would
become impossible, if they can not support this kind of look ahead (e.g. due to
technical limitations).

However, if it is possible to implement an operation without such an approach,
a look ahead could be used for a more efficient implementation. The focus here
is to not rely on the availability of a look a head.

Despite of that, a look ahead is an attempt to bypass the current knowledge of
what is guaranteed by the traversal of the tree. As such, a look ahead
represents an attempt to bypass the context of a node (i.e. make an operation
depend on subsequent nodes) and thus to predict future events. Because of that,
a design must not use any kind of look ahead.

<!-- ======================================================================= -->
## sections, S

**DEFINITION**
A section is a set of nodes.

The common aspect of the initially mentioned requirements is that any node must
belong to at least one section. In addition to that, no node can belong to the
same section more than once. Hence, sections can be defined as sets of nodes:

* `s := {n1,...,nk}`, `s in S`, `ni in N`
* `S` represents the set of sections, `N` the set of nodes
* `(s subset-of N)` is true for any `s in S`
* `(is-empty s)` is true, if `(#s == 0)`
* `#s := k`, `k in [0,#N]`

If node `n` is determined to be associated with section `s`, then node `n` must
be added to section `s` as one of its elements (Note that this is just a formal
requirement). By itself, this `add` operation defines a many-to-many (N:M)
relation which will be referred to as the tree's "SxN relation".

* `(s contains ni)` is true, if `(ni in s)`
* `contains` is said to be the semantics of the `SxN` relation.
* `(ni element-of s)` is true, if `(ni in s)`
* synonymous - `element-of`, `belongs-to`, `located-within`, etc.
* `(s related-to ni)` is true, if `(ni in s)`
* `(ni related-to s)` is true, if `(ni in s)`

Note that the `contains` relation is said to be "directional" because the order
of elements in the corresponding expressions does matter. In contrary to that,
the `related-to` relation is said to be "undirectional".

**DEFINITION**
A section is a sequence of nodes.

In principle, an algorithm must traverse the node tree in order to visit and
associate each node with at least one section. As a result, the nodes of a
section will be added to it, one after another, in a specific order. Because
of that, a section has a first and a last node. Consequently, sections can
also be defined as node sequences:

* `s := [n1,...,nk]`, `s in S`, `ni in N`
* `n1` is the section's first node, `nk` is the section's last node
* `(ni != nj)` for `i,j in [1,k]` and `(i != j)`

**CLARIFICATION**
Both of these definitions technically allow to associate any node with multiple
sections. Rules are therefore required in order to uniquely determine the actual
context of a node (i.e. its location with regards to the sections of a tree).

Note that, because of this formal approach (i.e. associate each node with one
or more sections), the relationship between sections can be ignored for the
time being. Because of that, the relationship between sections must later be
determined from the associations the sections have with the nodes of the tree.

**DEFINITION**
The scope of a section is the range of nodes that are associated with it.

The scope of a section begins with the section's first node and ends with the
section's last node. Consequently, any non-empty section always has a non-empty
scope. The scope of an empty section is said to be empty. However, an empty
section can also be understood to have no scope at all.

<!-- ======================================================================= -->
## sectioning nodes, NxS

When beginning to traverse a node tree, the set of sections is initially empty.
Certain nodes are therefore needed in order to declare (aka. introduce) new
sections. These nodes will be referred to as the tree's "sectioning nodes".

**DEFINITION**
Any sectioning node always declares a single new section.

* No section can exist without the sectioning node that declares it.
* Any section can be identified by its sectioning node.

Consequently, there is a one-to-one (1:1) relation on the set of sectioning
nodes `SN` and the set of known sections `S`. This relation will be referred
to as the tree's "NxS relation".

* `(sn declared s)` is true, if node `sn` declared section `s`
* `(s declared-by sn)` is true, if `(sn declared s)` is true
* for any `sn in SN subset-of N` and for any `s in S`

An algorithm has knowledge of a section as soon as its sectioning node is being
entered. That is, because a sectioning node always and unconditionally declares
a new section. Because of that, any new section must be added to the set of
known sections as soon as its sectioning node is being entered.

In general, and from that point on, any subsequent node must be associated with
that new and any other known section. Consequently, any node potentially belongs
to multiple sections. That is, because any node can be subsequent to any number
of sectioning nodes.

**PROPERTIES**
The above mentioned 1:1 relation can be seen to define the following two
implementation specific object properties:

* `Section SectioningNode.declaredSection`
* `SectioningNode Section.sectioningNode`

**DEFINITION**
A sectioning node does not belong to its own section.

Even though a sectioning node is insequent and thus not subsequent to itself,
it is technically still possible to associate a sectioning node with the section
it declares. That is, because an algorithm knows about a section as soon as it
enters the section's sectioning node. However, this does not imply that it would
be reasonable to associate a sectioning node with its own section.

Note that associating a sectioning node with its own section can be seen to
add a node to its own context. That is, a sectioning node would consequently
have an effect on itself as this information would be used to set the
corresponding property of the sectioning node.

Obviously, and as far as possible, an algorithm needs to be able to treat all
sectioning nodes alike. (Note that this will be referred to as "consistent
association across all types of sectioning nodes".) That is, because associating
one type of sectioning nodes with their own section, but not the sectioning
nodes of another type, would make it necessary to add additional logic with
regards to the different types of sectioning nodes.

If all sectioning nodes would have to be associated with their own section,
then no section could ever be completely empty. That is, because any section
would then always begin with its own sectioning node. And because of that,
additional logic would always be required in order to determine if a section
contains any meaningful content or not.

Note that more explanations will follow, which explain from additional
perspectives why sectioning nodes must not be associated with their own
sections.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
A node sequence of length `N` can declare no more than `N` sections.
That is, because each sectioning node always declares a single section only.

**CLARIFICATION**
A section is said to be subsequent to its sectioning node.

Note that this perspective is based upon a section's first content node,
which always is subsequent to the section's sectioning node.

**CLARIFICATION**
A section is said to be presequent to a node, if the section
is declared by a sectioning node that is presequent to it.

Note that, because of that, a section is presequent to its first content node.
However, the focus of this statement is on nodes that are unassociated with
the corresponding section.

**CLARIFICATION**
A section is said to be presequent to another section, if its
sectioning node is presequent to the other section's sectioning node.

**CLARIFICATION**
A sectioning node can only be associated with sections
that are presequent to it.

Note that this is a mere consequence of the above statement that a sectioning
node does not belong to its own section.

**CLARIFICATION**
The combination of all sections is referred to as a tree's "outline".

Note that this basic term does not allow to determine which relationship the
sections have with each other. What structure exactly a tree's outline has,
if any, still needs to be determined.

**CLARIFICATION**
With regards to the process of creating an outline, the sectioning nodes of
a tree are said to be the tree's "active" nodes. Any other node is therefore
said to be an "inactive" or a "passive" node. Because of that, a tree's set
of nodes consists of: (1) the set of active and (2) the set of passive nodes.

Here, the notion of the terms "active" and "passive" refers to a node's
characteristic to have an effect on the outline of its tree. If a node
has such an effect, the node is active, otherwise it is passive.

Note that currently no other types of nodes are active. If that ever changes
(e.g. due to the definition of an end marker node, or some node property),
then the set of active nodes will also contain the corresponding nodes.

**CLARIFICATION**
In order to simplify discussion, all the nodes of a section, excluding the
section's sectioning node, are said to be the section's "content nodes". All
these nodes combined are said to define the "contents of a section". Finally,
the term "section" is in general only used with regards to its content nodes.

<!-- ======================================================================= -->
## the root node - universal section

**CLARIFICATION**
Any node always belongs to at least one section.

Because a section can not exist without a presequent sectioning node, the root
node, with which an algorithm has to begin, can not be associated with any
predeclared section. That is, because there is no presequent sectioning node
that could declare such a section.

However, the root node can be seen to be embedded into a theoretical universal
section `u`. As such, this universal section must be understood to be declared
by a virtual sectioning node that is presequent to any node. The universal
section must also be understood to never end. Because of that, the universal
section is omnipresent. That is, any node always is related to it (aka. global
scope).

Consequently, and because of this formal concept, any node within a tree always
belongs to at least one section. Put differently, there is no node that does
not belong to any section at all.

**CLARIFICATION**
The root node is a sectioning node
and its section is referred to as the "root section".

Without any further clarification, and assumed that a tree's root node does
itself not (strictly or loosely) contain any other sectioning node, all the
nodes in the root's subtree would then only belong to the universal section.
Because of that, the location of those nodes would be undefined as they would
all appear to be lost inside of the global scope.

Consequently, the root node of a tree must be understood to always declare its
own section. That is especially true, if the algorithm's initial node is the
tree's root node (e.g. the HTML `<body>` element).
