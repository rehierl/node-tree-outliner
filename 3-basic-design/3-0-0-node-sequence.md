
<!-- ======================================================================= -->
# Design - node sequence

The traversal of a tree can be used to create a sequence of nodes (aka. trace
of nodes), if each node of the tree's set of nodes `N` is added to the sequence
while it is being entered. This node sequence will be referred to as "the node
sequence" of the tree:

* `ns := [n1,...,ni,...,nk]`
* `(k == #N)`, `ns(i) in N`, `ns in N^k`
* `n1` was entered first and `nk` was entered last
* `ni` is in general referred to as "the current node"
* `ni` is entered after `ni-x` and before `ni+y`, `x,y in [1,k]`

Note that `x,y in [1,k]` is not accurate because the range of numbers (i.e.
`[1,k]`) is too large. That is, because `(i-x)` could turn out to be less than
`1` and `(i+y)` greater than `k`. In order to keep explanations simple, that
range needs to be understood to only contain values that result in a valid node
index.

The length of a node sequence is identical to the number of nodes in the node
tree. That is, because each node will be entered exactly once.

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
That is, because node `ni+k` is entered after the current node `ni`. In contrary
to that, the term "presequent" needs to be understood to focus on known past
events. This switch in perspective is critical because no algorithm, in the
context of the following discussion, can execute any operation based nodes that
still have to be entered.

### order of nodes

An algorithm must, beginning with some initial node, traverse a tree from one
node to another and in the tree's order of nodes. After all, the algorithm's
result is intended to accurately represent the contents of the tree, which
obviously must include the tree's order of nodes.

Note that the tree traversal's sequence of enter events is understood to
correspond with the tree's node order. Consequently, the node order of a
tree's node sequence corresponds with the node order of the tree.

Note that a sibling is assumed to be presequent to its next sibling (no doubt
about that) and that any parent is presequent to its descendants.

### executing operations

In order to produce any result, an algorithm must execute operations, which it
can only do while entering or exiting a node. Because of that, an algorithm, in
the context of this discussion, represents an event-driven process.

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
within subsequence `s1 := [n1,ni]`. That is, because it already came in contact
with all the nodes in that sequence.

Note that, due to an algorithm's current node, an algorithm's current knowledge
contains nodes that it will still have to exit at some later point in time.
That is, because the algorithm will still have to exit the current node and
therefore also all of its ancestors.

In addition to that, the existence of those nodes in `s1` is guaranteed.
This is obviously not the case with regards to any subsequent node in
`s2 := [ni+1,nk]`: These still need to be entered.

No algorithm can therefore make any reasonable decision based upon nodes that
are subsequent to its current node. That is, unless definitions exist which
guarantee that some specific subsequent node will be entered eventually. In
general, such guarantees do not exist.

Note that, even if such a guarantee would exist, relying on that kind of
guarantee makes it necessary to add additional logic in order to deal with
trees that do not comply with the corresponding rules (i.e. input/user errors).

In addition to that, any operation executed while entering a node is allowed
to have an effect on the node itself and/or on nodes that are subsequent to
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
and exited after `ni` was exited. Consequently, `ni` will be exited in between
the exit event of `nj` and the enter event of `nj+1`.

Because of that, any node in `s3` can technically have an effect on its
presequent ancestor `ni`. That is, because a process will have knowledge
of any node within `s3` by the time `ni` is being exited.

However, such delayed knowledge must not be used to execute any operation that
could turn out to have implicit side effects on any node in `s3`. That is,
because these operations have the potential to produce conflicting statements.

```
n1  n2  /n2  n3  /n3  /n1
```

Note that, when exiting `n1`, the knowledge of `n3`'s existence can technically
be used to change properties of `n1` when exiting that node. Because of that,
and if such a property would have an implicit effect on `n1`'s descendants, then
`n3` would have an implicit effect on itself and its presequent sibling `n2`.
These kind of circumstances can be therefore understood to contain an implicit
feedback loop (`n3 -> n1 -> n3`).

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
them while they are being entered would result in node sequence `s5` and
associating them while they are being exited would result in sequence `s6`.

In contrary to `s5`, sequence `s6` does not correspond with the node order of
the above fragment. Because of that, and if those nodes would be the only nodes
of a section, sequence `s6` does not represent the contents of that section.

Consequently, executing any operation while a node is being exited is in
principle problematic. Exit events must be used to execute operations which
only affect those nodes that are subsequent, but not descendant to the node
being exited (i.e. subsequent to the exit event). That is, operations executed
while exiting `ni` may only affect those nodes in `s4`, but must not have any
side effect on any node in `s3`.

<!-- ======================================================================= -->
## the context of a node

In general, the minimal set of data used by an operation can be referred to as
the context of an operation. And because an operation can not function properly,
if any data is taken away from its context (minimal set), any data within an
operation's context is considered to be significant to that operation (see
en.wikipedia.org: Context (computing), Operational context, Operating context).

**CLARIFICATION**
Operations executed during a node event (referred to as the current event) are
in general only allowed to have an effect on those nodes that are subsequent
(forwards) to the current event. In addition to that, operations can only rely
on those nodes that are presequent (backwards) to the current event.

Note that a node is presequent to its own exit event. That is, because the
term "a node" refers in general to the node's enter event. Exit events are
therefore considered to be secondary (but not unimportant) events.

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
siblings. Note that the context of a node may also include those siblings
that are presequent to one of the node's ancestors.

Because of that, the current knowledge of an algorithm, is in general not
identical to the context of the current node. That is, because the current
knowledge includes the context of a node and, in addition to that, nodes
which are not part of that context (i.e. not all nodes that are presequent
to a node are allowed to have an effect on it).

Note that even those nodes, which have already been exited, can be allowed
to have an effect on subsequent nodes (e.g. presequent siblings).

<!-- ======================================================================= -->
## look ahead

An implementation could technically have the ability to cheat the traversal of a
tree by directly examining the tree's structure when a certain node is entered.
Because of that, an implementation could simply determine ahead of schedule, if
that node has child nodes or a next sibling, and therefore gain additional
knowledge which it could use to choose between different operations.

The downside of this kind of look ahead would be, that this ability would turn
into a necessity, if it could not be avoided. That is, implementations would
become impossible, if they can not support this kind of look ahead (e.g. due
to technical limitations).

However, if it is possible to implement an operation without such an approach,
a look ahead could be used for a more efficient implementation. The focus here
is to not rely on the availability of a look a head.

Despite that, a look ahead is an attempt to bypass the current knowledge of
what is guaranteed by the traversal of the tree. As such, a look ahead
represents an attempt to bypass the context of a node (i.e. make an operation
depend on subsequent nodes) and therefore an attempt to predict future events.
Because of that, a design must not rely on any kind of look ahead.
