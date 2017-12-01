
<!-- ======================================================================= -->
## General goals

The most fundamental goal of an outline algorithm is to allow the generation
of an accurate listing of sections (aka. table of contents, TOC) that can be
found within a given node tree. As such, a TOC provides a static overview of
the tree's contents.

However, the more sections there are, the less helpful such a listing becomes.
An outline algorithm must therefore allow to support dynamic behavior.

An outliner must allow to change the display of a TOC based on actions
executed on the display of a tree (i.e. tree -> toc):

* Allow to determine the context of any given node in order to display and
  update the display of the current location (e.g. bread crumbs).
* Allow to dynamically change the TOC of a tree based upon any given node.
  It must be possible to show/unfold those parts of a tree that are within
  a given context and to hide/fold parts that are outside of it.

An outliner must allow to change the display of a tree based on actions
executed on the display of a TOC (i.e. toc -> tree):

* Allow to focus on a section depending on which TOC entry was selected.
* Allow to dynamically change the display of a tree depending on which TOC
  entry was selected. It must be possible to show/unfold those parts of a
  TOC that are within the current context and to hide/fold parts that are
  outside of it.

An outliner must allow to manually change the display of a tree depending
on actions executed on the display itself (i.e. tree -> tree):

* Allow to show/unfold and to hide/fold a section, if the corresponding
  event was triggered on a section's representative.

In order to support these dynamic goals, certain requirements must be met:

* Any node within a tree must effectively belong to exactly one section.
  This is needed to uniquely determine the context of any node.
* It must be possible to determine the location of a section, even if that
  section turns out to be empty. This is needed to focus on any given section.
* It must be possible to treat any section as a single entity.
  This is needed to fold/unfold whole sections via a single operations.

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
operation that might have some side effect on any node within `s3`. These
kind of operations have the potential to produce contradictions.

**TODO** - 
associate nodes when entering

```
<n1><n2><n3> ... </n3></n2></n1>
```

In addition to that, when executing any operation while a node is being exited,
the overall order of events must be taken into account. That is, ancestor nodes
will be entered before their descendant nodes are entered. In contrary to that,
descendant nodes will be exited before their ancestor nodes are exited. Hence,
compared to enter events, exit events will be triggered in reverse order.

Consequently, executing any operation while a node is being exited is per se
problematic. Because of that, exit events must only be used to execute actions
which affect nodes that are subsequent, but not descendant to the node being
exited (i.e. they can affect nodes in `s4`, but must not have any side effect
on any node in `s3`).

**TODO** -
can a node be allowed to have any effect on itself
(e.g. associate with its own section)?

<!-- ======================================================================= -->
## Sectioning nodes, NxS

When beginning to traverse a node tree, the set of sections is initially empty.
Certain nodes are therfore required to declare (aka. introduce) new sections.
These type of nodes will be referred to as "sectioning nodes".

**DEFINITION** - Any sectioning node always declares a single new section.

* No section can exist without the sectioning node that declared it.
* Any section can be identified by its sectioning node.

Consequently, there is a one-to-one (1:1) relation on the set of sectioning
nodes `SN` and the set of sections `S`. This relation will be referred to as
"the NxS relation".

* for any `sn in SN subset-of N` and for any `s in S`
* `(sn declared s)` is true, if node `sn` declared section `s`
* `(s declared-by sn)` is true, if `(sn declared s)` is true

An algorithm has knowledge of a section as soon as its sectioning node is being
entered. That is, because a sectioning always (i.e. unconditionally) declares
a new section. And because of that, any new section must be added to the set of
sections `S` as soon as its sectioning node is entered. The set of sections `S`
therefore represents the set of known sections.

In general, and from that point on, any subsequent node must be associated with
the new and any other known section. Consequently, any node potentially belongs
to multiple sections. That is, because any node can be subsequent to any number
of sectioning nodes.

**DEFINITION** - A sectioning node does not belong to its own section.

Even though a sectioning node is insequent to itself, it is technically still
possible to associate a sectioning node with the section it declared. That is,
because an algorithm knows about a section as soon as it enters the section's
sectioning node. However, this does not imply that it would be reasonable to
establish such a relationship.

Obviously, and as far as possible, an algorithm needs to be able to treat all
sectioning nodes alike. Associating one type of sectioning nodes with their
own section, but not sectioning nodes of another type, would be bad practice.
That is, because this would always make it necessary to add additional logic
in order to distinguish between those types of nodes.

If any sectioning node would have to be associated with its own section, then
no section would ever be truly empty. That is, because any section would then
always contain at least its own sectioning node. Consequently, sectioning nodes
must not be associated with the sections they declare.

Note that this is only the easiest to explain reason. As such, it is also the
weakest of them all. More difficult to explain reasons, which have more impact,
will follow.

### Scope of a section

**CLARIFICATION** - A section has three states: "initialized", "open", "closed".

*initialized*:

As soon as a sectioning node is known, it is technically possible to associate
nodes with it. Because of that, and if a section had no delayed start,
sectioning nodes would have be associated with their own section. Consequently,
a section's "initialized" state has the following meaning: (1) the section is
known and (2) an algorithm must start associating nodes with it at some later
point in the process.

*open*

Once the first node of a section is reached, any subsequent node must be
associated with it. This means that it is not allowed to skip any subsequent
node and to continue associating nodes with a section at some later point in
time. 

*closed*

The "scope of a section" (respectively the scope of a sectioning node) can be
understood to define when to begin and when to stop associating nodes with a
section. The scope of a section therefore defines which nodes belong to the
section of a sectioning node.

Because of that, any section always has a scope:
 The scope of an empty section is empty (i.e. empty scope). In addition to that,
the first node that can potentially be associated with a section is the section's
sectioning node, and the last node possible is the last node of the corresponding
node sequence (i.e. unrestricted scope).

Obviously, additional rules are required to limit the scope of a section
because the last node entered would otherwise have to be associated with
all the sections declared inside of the whole node tree.

**TODO** -
there can be no empty sections, if sectioning nodes belong to their sections

### States of a section

Certain rules are required that can be used to determine when it is no longer
allowed to associate nodes with a section. Similar to binary streams, sections
can be seen to be either "open" or "closed" for associations:

* Nodes must be associated with a section, if it is considered to be "open".
* No more associations are allowed, if a section is considered to be "closed".



* A section is fully defined once it is closed.
* 

However, the very first node that must be associated with a section does not
necessarily have to be strictly subsequent to the section's sectioning node.
That is, a section must be allowed to have a delayed start.

* The first child of any node is strictly subsequent to it.
* If any node has no child, then its next sibling (or some other node) is
  strictly subsequent to it.
* If a sectioning node `sn` has a child and a next sibling, and if this next
  sibling has to become the first node of `sn`'s section, then that first node
  is not strictly subsequent to `sn`.

### available events

In order to limit the scope of a section, a sectioning node must, one way or
another, tell the algorithm where the node's section begins and where it ends.
In return, an algorithm must have the means to execute the corresponding
operations when entering or exiting certain nodes.

```
             [ s1  ][ s2  ][ s3  ][ s4  ][ s5  ]
ns := [...,ni,...,nj,...,nk,...,nl,...,nm,...,nn,...]
           xxxxxxxxxxxxxxxx  - scope enter operations
                  xxxxxxxxx  - scope exit operations
```



* associate a sectioning node with its own section?
* A sectioning node binds its section to presequent nodes and sections.

<!-- ======================================================================= -->
## The root node

Because a section can not exist without a presequent sectioning node, the
root node, with which each process has to start, can not be associated with
any predeclared section. That is because there is no sectioning node that
is presequent to the root.

The universal section (u):

However, the root node can be thought of as being embedded into some universal
section `u`. This special section can be understood to represent a theoretical
section that contains any tree of nodes.

With that in mind, any node of a node tree always belongs to one or multiple
sections. Consequently, there is no node that does not belong to any section.

The root is itself a sectioning node:

Without any further clarification, and assumed that a given root does itself
not (strictly or loosely) contain any other sectioning node, all the nodes in
the root's subtree would only belong to the universal section. That is, there
would be no section which represents their relationship with the other nodes
of the root's subtree (i.e. location inside of the very same subtree).

In order to establish that kind of relationship, the root itself must to declare
its own section. Consequently, the root node is always considered to be a
sectioning node.
