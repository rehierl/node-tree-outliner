
<!-- ======================================================================= -->
# Associating each node with one section only

**CLARIFICATION**
Each node can be associated with one section only, if (and only if) the node
can also be understood to be (implicitly) associated with all ancestors of
that section.

The implicit association with all ancestor sections is therefore used to
condense the amount of associations into a single reference per node, which
would otherwise be required by the formal definitions. That is, because all
formal associations (formal perspective) of a node can be derived from its
explicit association (practical perspective).

**CLARIFICATION**
The least significant presequent section, which is still open when a node is
entered, will be referred to as *the (unique) parent section* of that node.

Note that this parent section is the nearest (i.e. closest according to the
node sequence) open presequent section. Put differently, a node's (unique)
parent section is the least significant open presequent section, which was
entered/declared last, before the corresponding node was entered.

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

Note that this section reference will be referred to as
the node's strict (or explicit, direct) association.

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
to "loosely (or seemingly) suspended". That is, because these sections still
count as being open.

**CLARIFICATION**
If each node is associated with one section only, then a section's complete
node sequence can be re-created by concatenating the nodes that are associated
with it, and all those nodes that are associated with one of its subsections.
That is, in the tree's order of nodes.

Consequently, a section still counts as a subsequence of the tree's node
sequence. The single/unique `parentSection` reference won't change that.

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
* `n0-1` are type-2 sectioning nodes.
* `n2-9` are represent inactive nodes.

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

Note that any node can therefore still be a top-level node to one or more
sections. Because of that, any section can still be loosely described as
"a sequence of siblings".

**CLARIFICATION**
A section's first content node is always a strictly associated top-level node.

Put differently, a section's first content node will always be strictly
associated with that section, never with one of the section's subsections.

That is, because the declared section will always be the new current and
least significant section when a section's first content node is entered.
Consequently, the declared section will always be used to associate its
first content node.

Note again, that a section's first content node
is also a section's first top-level node.
