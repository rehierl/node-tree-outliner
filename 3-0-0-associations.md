
<!-- ======================================================================= -->
## General goals

The most fundamental goal of an outline algorithm is to allow the generation
of an accurate listing of sections (aka. table of contents, TOC) that can be
found within a given node tree.

As such, a TOC provides a static overview of the tree's contents. However,
the more sections there are, the less helpful such a listing becomes.
An outline algorithm must therefore allow to support dynamic behavior.

An outliner must allow to change the display of a TOC based on actions
executed on the display of a tree (i.e. tree -> toc):

* Allow to determine the context of any given node in order to display and
  update a current location (aka. bread crumbs). The current location is
  a minimalistic display of information taken from the corresponding TOC.
* Allow to dynamically change the TOC of a tree based upon a given node.
  It must be possible show/unfold parts that are within a given context
  and hide/fold parts that are outside of it.

An outliner must allow to change the display of a tree based on actions
executed on the display of a TOC (i.e. toc -> tree):

* Allow to focus on a section depending on which TOC entry was selected.
* Allow to dynamically change the display of a tree depending on which TOC
  entry was selected. It must be possible to show/unfold parts that are
  within the current and hide/fold parts that are outside of it.

An outliner must allow to manually change the display of a tree depending
on actions executed on the display itself (i.e. tree -> tree):

* Allow to show/unfold a section, or hide/fold one, if the corresponding
  event was triggered on a section's representative.

In order to support these dynamic goals, certain requirements must be met:

* Any node within a tree must belong exactly one section.
  This is needed to uniquely determine the context/location of any node.
* It must be possible to determine the location of a section, even if that
  section turns out to be empty. This is needed to focus on any given section.
* It must be possible to treat any section as a single entity.
  This is needed to fold/unfold whole sections via single operations.

<!-- ======================================================================= -->
## Sections, SxN

The most fundamental aspect of the above requirements is, that any node must
belong to at least one section. In addition to that, no node can belong to the
same section more than once. Hence, sections can initially be defined as sets
of nodes. Operators defined for sets can therefore also be used on sections:

* `s := {n1,...,nk}`, `s in S`, `ni in N`
* `S` represents the set of sections, `N` the set of nodes
* `#s := k`, `k in [0,#N]`
* `(s subset-of N)` for any `s in S`

A node `n` must be added to section `s`, if it must be associated with it.
On its own, the `add` operation defines a many-to-many (N:M) relation.
This relation will be referred to as "the SxN relation".

* `(s contains ni)` is true, if `(ni in s)`
* `contains` is said to be the the `SxN` relation's semantics.
* `(ni element-of s)` is true, if `(ni in s)`
* synonymous - `element-of`, `belongs-to`, `located-within`, etc.
* `(s related-to ni)` is true, if `(ni in s)`
* `(ni related-to s)` is true, if `(ni in s)`

Consequently, an outline algorithm must traverse the node tree in order to
visit and associate each and every node. As a result, the nodes of a section
will be added to it, one after another, in some particular order (this is why
a section can also be defined as a sequence of nodes):

* `s := [n1,...,nk]`, `s in S`, `ni in N`
* `(ni != nj)` for `i,j in [1,k]` and `(i != j)`
* `n1` is the section's first node, `nk` is the section's last node

Both the above definitions allow to associate any node with multiple sections.
Additional rules are therefore required to uniquely determine the actual
context/location of a node.

<!-- ======================================================================= -->
## Node sequence

The traversal of a tree can be used to create a sequence of nodes (aka. trace
of nodes), if each node is added to a sequence while it is in the process of
being entered. Such a node sequence will be referred to as "the node sequence"
`ns` of the corresponding node tree:

* `ns := [n1,...,ni,...,nk]`
* `(k == #N)`, `ns(i) in N`, `ns in N^k`
* `n1` was entered first and `nk` was entered last
* `ni` is entered after `ni-x` and before `ni+y`, `x,y in [1,*]`

Because each node will be entered exactly once, the length of a node sequence
is identical to the number of nodes in the corresponding node tree.

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

Note that each enter and exit event is an atomic operation. That is, subsequent
nodes will not be entered or exited, while a presequent node is still in the
process of being entered or exited.

### current knowledge

```
       [ s1    ][ s2  ]
ns := [n1,...,ni,...,nk]
       xxxxxxxxx                - knowledge when ni is entered
              xxxxxxxxx         - maximum scope of enter operations
```

Any outline algorithm must, beginning with a first node, traverse from one node
to another. In addition to that, an algorithm must execute operations based on
the knowledge it gained from visiting presequent nodes.

Such an algorithm has, when entering its current node (e.g. `ni`), knowledge of
any node within subsequence `s1 := [n1,ni]`. The algorithm's current knowledge
therefore consists of all the nodes within subsequence `s1`.

The nodes within `s1`, that have already been exited, will in general be ignored
when making any kind of decision. That is, operations will usually only depend
on a node itself and/or on the ancestors of its current node.

Consequently, no process can make any reasonable decision based upon subsequent
nodes (i.e. nodes in `s2 := [ni+1,nk]`). That is, unless definitions exist
which guarantee that some specific subsequent node, or multiples thereof,
will eventually be entered. In general, such guarantees do not exist (i.e. no
attempts must be made to take any action based on possible future events).

In addition to that, any operation executed while entering a node can only have
an effect on the node itself, or on nodes that are subsequent to it. That is,
if the exit event of its parent node is ignored.

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
and exited after `ni` was exited.

Consequently, any node within `s3` might technically still have an effect on its
presequent ancestor `ni`. That is because a process will have knowledge of any
node within `s1` by the time `ni` is being exited.

However, this kind of delayed additional knowledge must not be used to execute
any operation that might have some side effect on any node within `s1`. That
is because operations, which depend on this kind of delayed knowledge, have the
potential to produce contradictions.

**TODO** - 
associate nodes when entering them

```
<n1><n2><n3> ... </n3></n2></n1>
```

In addition to that, when executing any operation while a node is being exited,
the overall order of events must be taken into account. That is, ancestor nodes
will be entered before their descendant nodes are entered. In contrary to that,
descendant nodes will be exited before their ancestor nodes are exited (i.e.
exit events will be triggered in reverse order).

Consequently, executing any operation while a node is being exited is per se
highly problematic. Because of that, exit events must only be used to execute
operations which affect nodes that are subsequent, but not descendant to the
node being exited (i.e. they can affect nodes in `s2`, but must not have any
side effect on any node in `s1`).

**TODO** -
can a node be allowed to have any effect on itself
(e.g. associate with its own section)?

<!-- ======================================================================= -->
## Sectioning nodes, NxS

When beginning to traverse a tree of nodes, the set of sections is initially
empty. Certain nodes are therfore needed to declare (aka. introduce) new
sections. These type of nodes will be referred to as "sectioning nodes".

* **DEFINITION**: Any sectioning node always declares a single new section.
* No section can exist without the sectioning node that declared it.
* Any section can be identified by its sectioning node.

Consequently, there is a one-to-one (1:1) relation on the set of sectioning
nodes `SN` and the set of sections `S`. This relation will be referred to as
"the NxS relation".

* for any `sn in SN subset-of N` and `s in S`
* `(sn declared s)` is true, if node `sn` declared section `s`
* `(s declared-by sn)` is true, if `(sn declared s)` is true

As soon as a sectioning node `sn` is entered, the section it declares is known
to the process and must immediately be added to the set of sections `S`. In
general and from that point on, any subsequent node must be associated with it.

Because of that, any node potentially belongs to multiple sections. That is
because any node can be subsequent to any number of sectioning nodes.

Obviously, rules are required to limit the scope of a section because the very
last node entered would otherwise have to be associated with all the sections
that are declared inside of the current tree of nodes.

### Scope of a section



In order to limit the scope of a section, a sectioning node must tell the
algorithm where its section begins and where it ends. In return, an algorithm
must know when to start and when to stop associating subsequent nodes with a
section.

```
             [ s1  ][ s2  ][ s3  ][ s4  ][ s5  ]
ns := [...,ni,...,nj,...,nk,...,nl,...,nm,...,nn,...]
           xxxxxxxxxxxxxxxx  - scope of ni enter operations
                  xxxxxxxxx  - scope of ni exit operations
```

* associate a sectioning node with its own section?
* A sectioning node binds its section to presequent nodes and sections.

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

### Reflexive associations

Although a sectioning node is insequent to itself, it is technically still
possible to associate a sectioning node with the section it declares. That is
because a section is a known section as soon as its sectioning node is entered.

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