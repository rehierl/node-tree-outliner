
<!-- ======================================================================= -->
# Design (2)

This section builds upon the fundamental definitions, considerations and
conclusions mentioned previously.

<!-- ======================================================================= -->
## States of a section

Similar to output streams, any section has the following states:

### initialized

As soon as a sectioning node is known, it is technically possible to, beginning
with the current node, associate any subsequent node with it. Because of that,
and if a section had no delayed start, a sectioning node would have to be
associated with its own section.

Consequently, a section's "initialized" state means that: (1) the section is
known and (2) an algorithm must start associating nodes with it at some later
point in time.

### open

Once a section's first node is entered, this first node and any subsequent node
must be associated with it. An algorithm therefore needs additional rules that
enable it to determine when to begin associating nodes with a section.

A section is considered to be "open" as soon as the next subsequent node must
be associated with it.

### closed

Any section must eventually end at some point. By default, that point is reached
when the initial root node of the process is being exited. That is, because
there is no subsequent node with regards to this exit event.

This default case is obviously insufficient, because the very last node of
a node sequence would then always have to be associated with all the known
sections. An algorithm therefore needs additional rules that enable it to
determine, when it is no longer allowed to associate any subsequent node
with a section.

A section is considered to be "closed" as soon as it is no longer allowed to
associate any more nodes with it.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Once closed, a section is fully defined/specified. That is, because no
subsequent node will, by definition, have any further effect on it.

**CLARIFICATION**
A section can not be re-opened.

The "closed" state, and the corresponding rules, can therefore also be seen
to represent a guarantee, that a closed section will not change any further.

This guarantee is critical to an efficient TOC generator, because it allows to
drop a section object once the corresponding section is closed and once the the
information it holds has been extracted. After that, any attempt to execute any
kind of operation on a dropped section object will result in an access violation
error.

Re-opening a section for additional associations would therefore be in conflict
with the above guarantee. Because of that, such an operation must be seen to
represent an attempt to suspend and resume a section.

**CLARIFICATION**
A section can not be strictly suspended.

Note that it is assumed, that a "resume" operation must always follow a
"suspend" operation ("suspend" would otherwise be equivalent to "close").

Technically, it would be possible to define rules that tell an algorithm to
suspend and then, at some later point in time, resume associating nodes with a
section. However, this does not mean that it would be reasonable to allow such
an operation.

Assumed that section `s` would have to be suspended after some node `ns` was
associated with it, and that section `s` would have to be resumed beginning with
some node `nr`. This would in return mean that, in between both nodes, there
need to be any number of nodes that are supposed to be completely unrelated to
this section (hence, strictly suspended).

Such a section would then consist of multiple subsequent parts that are separate
from each other. Due to the gaps in between the section's parts, an algorithm
would then have no means to treat a section as as one entity by grouping all of
the section's nodes, which would obviously be in conflict with the initial
requirements.

In addition to that, the intermediate nodes in between the separate parts of a
strictly suspended section can still be seen to be in relationship with it. That
is, because the very reason, as to why these intermediate nodes would have to be
excluded, puts these intermediate nodes into a relationship with said section.
After all, they would be surrounded by the section's parts. Because of that, the
ultimate goal of such an attempt (i.e. completely unrelated nodes) can't even be
reached without producing a conflict.

Note that these considerations do not take the definition of nodes into account,
that would be necessary to clearly define when a section has to be suspended.

Finally, the subsequent part of a strictly suspended section can also be seen to
represent a section of its own. Hence, the nodes that would be required in order
to tell an algorithm that it has to resume a section can themselves be seen to
represent separate sectioning nodes. The separate parts can then be seen to
represent separate sections.

**CLARIFICATION**
A section has no gaps.

Because of that, any node belongs to a section, if it is subsequent to the
section's first and presequent to the section's last node.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Nodes must be associated with sections while they are being entered.

Because exit events will be executed in reverse order, associating any nodes
while they are being exited would constitute a deviation of the tree traversal's
order of nodes, and, as such, a deviation of the tree's semantics. Consequently,
associating any nodes with sections while they are being exited can in principle
not result in sections that accurately represent the contents of a tree.

Apart from that, the location of a node (with regards to a tree's sections)
could then be affected by nodes that are subsequent to it. Because of that,
a subsequent node could end up having an effect presequent nodes.

**CLARIFICATION**
A section is a sequence of subsequent nodes.

That is, because any node must be associated with a section while it is being
entered. Consequently, the node order of a section corresponds with the node
sequence of a tree.

**CLARIFICATION**
A section is a sequence of strictly subsequent nodes.

That is, because a section corresponds with the node sequence of a tree, and
because a section has no gaps in between any two of its adjacent nodes.

<!-- ======================================================================= -->
## Sectioning nodes - first nodes (2)

Because a section is a sequence of strictly subsequent nodes, definitions only
need to tell an algorithm, with which node a section begins and with which node
it ends. In addition to that, an algorithm must have the means to implement the
corresponding operations efficiently (or even at all).

Because an algorithm knows about a section as soon as it enters the section's
sectioning node, it has the ability to execute operations that prepare itself
for the association of the section's first node (e.g. mark a section as being
"open"). That is, either when entering or when exiting the sectioning node.

The use of the sectioning node's enter or exit event is, by itself, not a
requirement for the definition of a certain type of sectioning nodes (In theory,
any event could be used). However, an algorithm must know which event exactly
it has to use. Because of that, the relationship of the sectioning node and the
section's first node must be clearly defined.

### type-1, first child

Because a sectioning node does not belong to its own section, the very first
node that could possibly be associated with a section is the first child of a
sectioning node.

All an algorithm has to do in such a case is to mark the declared section as
being open when it is about to exit the sectioning node's enter event.

**DEFINITION**
A section will be referred to as a "type-1 section", if its scope begins with
the first child of its sectioning node. Consequently, a sectioning node that
declares a type-1 section will be referred to as a "type-1 sectioning node".

Note that, in an unordered tree of nodes, any child would have to belong to
such a section. That is, because, in an unordered tree, there is no guarantee
that a certain child will be a parent's first child. Any of these nodes have
to be considered equal.

### type-2, next sibling

Likewise, an algorithm can easily implement a rule that defines the next
sibling of a sectioning node as the section's first node.

All an algorithm has to do in such a case is to mark the declared section
as being open when it is about to exit the sectioning node's exit event.

**DEFINITION**
A section will be referred to as a "type-2 section", if its scope begins with
the next sibling of its sectioning node. Consequently, a sectioning node that
declares a type-2 section will be referred to as a "type-2 sectioning node".

Note that this type of section requires an ordered tree of nodes. That is,
because nodes in an unordered tree are not guaranteed to have any specific
next sibling, or even a specific first child. Any of these nodes have to be
considered equal.

Attempting to use such a section in an unordered tree will not produce
deterministic results. That is, because the nodes of an unordered tree
are not guaranteed to be served to an algorithm in any particular order.
Subsequent executions will eventually produce different results.

### associate nodes while entering

```
<n1><n2> n3 </n2></n1>
```

Assumed that node `n1` would be defined to be a section's first node.

If an algorithm would associate nodes while they are being exited, then node
`n3` would not be determined to be the section's first node. Put differently,
the algorithm would not recognize that node as the section's first node.

Or, if whitespace nodes would have to be taken into account, an algorithm would
determine the whitespace node, located in between `n2` and `n3`, to be the
section's first node.

Consequently, associating nodes while they are being exited can not guarantee
that the first node of a section (by definition) will actually become the first
node of its section (by association).

**CLARIFICATION**
All nodes must be associated while they are being entered.

<!-- ======================================================================= -->
### derived statements

**CLARIFICATION**
Type-1 and type-2 sectioning nodes force no pattern upon a tree's structure.

That is, the declared section is empty, if the sectioning node has, depending
on its type, no first child or no next sibling. Because of that, there is no
requirement with regards to the structure of a tree.

**CLARIFICATION**
The first node's enter event is strictly subsequent to the corresponding event
of the sectioning node.

Unless further types of sections are defined, the first node of a section is
strictly subsequent to the corresponding event of the sectioning node. That is,
no other event will be executed after the sectioning node's event was exited
and before the first node is entered.

**CLARIFICATION**
The first node's enter event is not necessarily strictly subsequent to the
enter event of the sectioning node.

The next sibling of a parent node can only be loosely subsequent to it. That
is, because a node can only be a parent node, if it has at least one child
node. No sibling can therefore be strictly subsequent to any parent node.

Because of that, the first node of a section is strictly subsequent to the
section's sectioning node, if it is also the sectioning node's first child.

In contrary to that, the first node of a section is only loosely subsequent
to the section's sectioning node, if it is the sectioning node's next sibling
and if the sectioning node is a parent node.

Put differently, type-2 sections allow any number of events in between the
sectioning node's enter event and the first node's enter event.

<!-- ======================================================================= -->
## Why the strict, why no loose type-2 definition?

Note that a type-2 sectioning node, if it has no next sibling, can still have
nodes that are subsequent to its exit event (i.e. the next sibling of one of
its ancestors). After all, once a section is marked as being open, in the exit
event of the sectioning node, it remains to be open until it is closed.

The question therefore is: Would it be reasonable to loosely define a type of
section as "begins with the 'next subsequent' node" instead of the above strict
definition (i.e. "begins with the next sibling of the sectioning node").

If such a loose sectioning node would itself have no next sibling, then the
section's first node is going to be the next sibling of one of its ancestors.

Note that readers tend to create implicit whitespace nodes. Because of that, if
an implicit whitespace node would be the next sibling of such a sectioning node,
and if that sectioning node would have no other subsequent sibling, then the
next subsequent node would not be the next sibling of an ancestor. Consequently,
in order to truly support the loose definition of such a sectioning node, these
implicit whitespace nodes would have to be taken into account.

Note that a loose definition would, in itself, combine multiple strict
definitions (i.e. "next sibling", "the parent's next sibling", etc).

Note that it does matter, where exactly the sectioning node and the section's
first node is located (see subsections). **TODO**

A loose definition would have to find clear answers to multiple issues:

() The relationship between the sectioning node and the first node is unclear.

Additional logic would always be required in order to traverse from such a
sectioning node to the first node, or vice versa. That is, the potentially
greater distance between those two nodes would always have to be taken into
account.

() An ancestor could be seen as the actual sectioning node.

Because the previous sibling of the first node could be an ancestor of the
sectioning node, there would have to be a clear reason as to why that ancestor
is not supposed to be the actual sectioning node.

() The sectioning node and the first node could have different parent nodes.

Because of that, the first node can then be seen to state: "begins with an
ancestor". In contrary to that, the sectioning node can be understood to state:
"begins inside of a descendant". That is, such a loose definition will result
in conflicting semantics.

() Such a definition would prevent consistent transformations.

In general, type-2 patterns can be transformed into type-1 patterns by grouping
all the nodes of a type-2 section beneath a type-1 sectioning node.

(forwards) Where exactly would such a type-1 sectioning node would have to be
placed, if it were supposed to replace the pattern of such a loose definition?
At the location of the sectioning node, or at the first node of its section?

(backwards) If, in addition to that, the inserted type-1 sectioning node would
have to be replaced with the initial pattern, the resulting structure would be
different to initial node structure, i.e. the result could not be semantically
equivalent to the initial structure. After all, the information of the distance
between sectioning node and the first node would be no longer available.

**CLARIFICATION**
A loose type-2 definition is not sufficient to guarantee consistent dynamic
support. A strict type-2 definition is necessary (see requirements).

<!-- ======================================================================= -->
## Overview of other possible first nodes

Attempting to define any other type of node, as a section's first node, will add
secondary constraints to a definition and to an implementation. Apart from the
additional effort needed to detect when to actually begin associating subsequent
nodes with a section, an implementation would also have to take into account
that a tree's structure might not be as expected (i.e. error handling).

In order to justify these constraints, a definition would need to have a clear
reason as to why certain nodes (i.e. those in between the sectioning node and
the section's first node) would have to be excluded. That is, the semantics of
these unrelated nodes must be defined separately and with regards to the
declared section. Because of that, such an attempt is, although technically
possible, ill advised.

### look ahead

In theory, an implementation has the ability to cheat the traversal of the node
tree by directly examining the tree's structure as soon as a certain sectioning
node is entered. Because of that, it could simply determine ahead of schedule,
if that sectioning node has for example a 2nd child, a 2nd subsequent sibling,
or even a any ancestors. Consequently, an algorithm can potentially configure
itself to act accordingly.

The downside of this kind of look ahead would be, that this ability would become
a requirement, if it could not be avoided. That is, implementations that can not
support any kind of look ahead (e.g. due to technical limitations), would become
impossible. However, if it is guaranteed that a section type can be supported
without such an approach, a look ahead could be used as the basis of a more
efficient implementation.

Despite that, a look ahead is an attempt to bypass the current knowledge that
is guaranteed by the traversal of the tree. As such, it represents an attempt
to predict possible future events.

Because of that, such an approach must be avoided.

### second sibling

As mentioned above, type-2 sectioning nodes define the next sibling of the
sectioning node to be the first node of the declared section. As such, there
must be a definition of what the semantics of the sectioning node's descendants
are with regards to the declared section.

`<type-2> A </type-2> B C`

Here, node `B` will be the 1st and `C` the 2nd node of the declared section.
Because of that, node `A` can be understood to represent data that can be
used to initialize the section that is declared by the sectioning node:

```
// while exiting "type-2"
section = new Section("A")
knownSections.add(section)
section.open()
```

Note that node `A` does not necessarily have to be a single node. As such, node
`A` can represent a whole subtree of nodes, which must all be inactive with
regards to the algorithm. That is, no node within subtree `A` must be allowed
to have any effect on predeclared sections, or declare new sections themselves.

If node `C` would have to become the section's actual 1st node, then node `B`
would have to have semantics defined with regards to the declared section. That
is, `B`'s semantics would have to be similar to those of node `A`. Because of
that, the definition of a 2nd subtree that has similar semantics to node `A`,
does not justify the additional requirements that would have to be met because
of having to skip the subsequent subtree `B`.

Consequently, defining any other subsequent sibling as the section's first node
is unreasonable, because any node in the sequence of skipped nodes could easily
be added as descendants of the sectioning node.

### second child

Type-1 sectioning nodes define the first child of the sectioning node to be the
first node of the declared section. Because of that, these type of nodes can not
support any data that can be used to set any section properties.

`<type-1> A B </type-1> C`

However, the first child of the sectioning node could be used to specify data
that could be used to set such properties before any node will be associated
with the corresponding section.

```
// while entering "type-1"
section = new Section()
knownSections.add(section)

// while exiting "A"
section.configure("A")
section.open()
```

But in that case, the question would have to be answered as to why node `A`
must not be associated with the declared section. After all, even if the above
data container `A` would be associated with that section, it could still be
excluded from a subsequent process (e.g. excluded from being displayed).

`<container> <type-2> A </type-2> B </container> C`

In addition to that, there needs to be sufficient reason to choose this pattern
over the pattern of a type-2 sectioning node. That is, because subtree `A` could
then be understood to be the actual sectioning node.

Out of all the other options, and because a type-1 sectioning node does not
support any configuration data, this option could be seen to be reasonable
enough to justify the above mentioned additional constraints.

Note the HTML `<header>` element.

### next sibling of an ancestor

Although not every node is guaranteed to have an ancestor node, an algorithm
technically has the means to begin with associating nodes, if one of the
sectioning node's ancestors was exited. However, this would add additional
difficulty to a clear definition of such a sectioning node.

`<container> ... <A:type-x/> ... <B:type-x/> ... </container> C`

That is, because there would have to be a clear answer, as to which section node
`C` would have to belong, if a child contains multiple sectioning nodes of this
type. In addition to that, the corresponding ancestor could then be understood
to be the actual sectioning node.

### further options

Although there are even further ways to define the first node of a section (e.g.
variable relationship, descendants of siblings or children, etc.), it seems that
the more intricate the relationship between a sectioning node and the section's
first node is, the more questions would have to be answered in order to clearly
define an additional section type.
