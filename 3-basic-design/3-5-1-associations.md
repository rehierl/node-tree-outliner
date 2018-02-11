
<!-- ======================================================================= -->
# Design (6) - associating nodes

The following statements clarify the first practical (i.e. implementation
specific) implication that results from the formal definition of what a
subsection is.

<!-- ======================================================================= -->
## associate with one section only

**CLARIFICATION**
Each node can be associated with one section only, if (and only if) the node
can also be understood to be (implicitly) associated with all ancestors of
that section.

Consequently, these implicit associations are used to condense the amount of
strict associations (i.e. section references) into a single reference per node.

Note that the only reason, why a node can be associated with a single section,
is that the multiple associations of a node, which would be required by the
formal definitions, can be derived from those implicit associations, that
are defined by the relationships that the sections have with each other.

**CLARIFICATION**
A node must be associated with the closest open presequent section.

That is, because this one (strict) association must reflect all the
formal associations that a node has with all open presequent sections.

**CLARIFICATION**
The section, with which a node must be associated, is referred to as the
node's parent section. As such, a node's parent section defines the most
important, implementation specific property:

```
Section Node.parentSection
```

Because of this unique reference, a node's parent section defines
the context/location of a node with regards to the sections of a tree.

**CLARIFICATION**
If each node is associated with one section only, then any ancestor section,
which is not the node's parent section, can be understood to be "loosely
suspended". That is, because for as long as that parent section is open,
no node will be strictly associated with those seemingly suspended sections.

Note that, because a section can not be "strictly suspended" (see the state
transitions), the term "suspended" must always be understood to be synonymous
to "loosely or seemingly suspended". That is, because these sections still
count as being "open".

**CLARIFICATION**
If each node is associated with one section only, then a section's complete
node sequence can be re-created by concatenating the nodes that are associated
with it, and all those nodes that are associated with one of its subsections.
That is, in the tree's node order.

Consequently, a section still counts as a subsequence of the tree's
node sequence. The single `parentSection` reference does not change that.

**CLARIFICATION**
If node `n` is strictly associated with section `sX`, and if the question is,
whether node `n` is also associated with section `sY`, then the expression
`(sX == sY)` needs to be tested first. If that test fails, then it needs to be
tested whether section `sY` is an ancestor section of `sX`. Consequently, node
`n` is not associated with section `sY`, if (and only if) all of the afore
mentioned tests have failed.

Note that an implicit association is not guaranteed to be verified correctly
(i.e. false negatives are possible), if only the ancestor nodes of node `n`
are tested. That is, because a type-2 section can be hidden by that rooted
path of nodes.

<!-- ======================================================================= -->
## top-level nodes

Note that the initial definition of a top-level node (i.e. A node is a
top-level node of a section, if it must be strictly associated with it)
is with regards to the formal definitions (i.e. associate each node with
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
that is (strictly or loosely) associated with the corresponding section).

Note that a section's first content node still and always is a top-level node.
A section can therefore still be loosely understood as a sequence of siblings.

Applying this clarified definition, and associating each node with one
section only, has the following effect: (1) Nodes `n1-9` all are top-level
nodes of `s0`, and (2) nodes `n2-9` all are top-level nodes of `s1`.

Note that any node can still be a top-level node to multiple sections.
