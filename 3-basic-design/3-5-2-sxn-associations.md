
<!-- ======================================================================= -->
# Associating each node with one section only

**CLARIFICATION**
Each node can be associated with one section only, if (and only if) the node
can also be understood to be (implicitly) associated with all ancestors of
that section.

Note that this section reference will be referred to as
the node's strict (or explicit, direct) association.

Consequently, the implicit association with all ancestor sections is used to
condense the amount of associations, which would otherwise be required by the
formal definitions, into a single reference per node. That is, because all
formal associations (formal perspective) of a node can be derived from its
explicit association (practical perspective).

**CLARIFICATION**
The least significant presequent section, which is still open when a node is
entered, will be referred to as *the (unique) parent section* of that node.

Note that this parent section is the nearest (i.e. closest according to the
node sequence) open presequent section. Put differently, a node's (unique)
parent section is the least significant open presequent section which was
declared last, before the corresponding node was entered.

Note that all other sections, with which that node would have to be associated
according to the formal perspective, are ancestors of that section. And, because
of that, this section is the only section which can be used to represent all
the associations of the corresponding node.

**CLARIFICATION**
A node's unique parent section defines the following,
implementation specific property:

```
Section Node.parentSection
```

**CLARIFICATION**
A node's parent section can be understood to define the location of a node with
regards to the section hierarchy (i.e. its logical context).

**CLARIFICATION**
If each node is associated with one section only, then any ancestor section,
which is not the current node's parent section, can be understood to be
"loosely suspended". That is, because for as long as that parent section is
open, no node will be strictly associated with such a seemingly suspended
section.

Note that, because a section can not be "strictly suspended" (see the state
transitions), the term "suspended" must always be understood to be synonymous
to "loosely or seemingly suspended". That is, because these sections are not
closed (i.e. still open).

**CLARIFICATION**
If each node is associated with one section only, then a section's complete
node sequence can be re-created by concatenating the nodes that are associated
with it, and all those nodes that are associated with one of its subsections.
That is, in the tree's node order.

Consequently, a section still counts as a subsequence of the tree's node
sequence. The single `parentSection` reference won't change that.

<!-- ======================================================================= -->
## clarified definition of top-level nodes

Note that the initial definition of a top-level node (i.e. A node is a
top-level node of a section, if it must be strictly associated with it)
is with regards to the formal perspective (i.e. associate each node with
all open sections).

```
n0 n1 n2 n3 n4 n5 n6 n7 n8 n9
   ========================== -> s0
      ======================= -> s1
```

* All nodes are siblings to each other (i.e. descendants are ignored).
* `n0` and `n1` are type-2 sectioning nodes.

Strictly applying the initial definition, and associating each node with one
section only, has the following effect: (1) Node `n1` is the only top-level
node of `s0`, and (2) nodes `n2-9` all are top-level nodes of `s1`.

Because of that, the initial definition needs to be clarified:

**DEFINITION**
Node `n` is a top-level node of section `s`, if `n` must be (strictly or
loosely) associated with `s`, and if `n` has no ancestors that are already
(strictly or loosely) associated with `s`.

Note that the focus of this term is on the second part (i.e. has no ancestor
which is already (strictly or loosely) associated with the corresponding
section).

Applying this clarified definition, and associating each node with one section
only, has the following effect: (1) Nodes `n1-9` all are top-level nodes of
`s0`, and (2) nodes `n2-9` all are top-level nodes of `s1`.

Note that any node can still be a top-level node to one or more sections.
Because of that, any section can still be loosely described as a sequence
of siblings.

**CLARIFICATION**
A section's first content node always is a strictly associated top-level node.

That is, because the declared section will always be the new current, least
significant section. And, because of that, the declared section will always
be used to associate the section's first content node.
