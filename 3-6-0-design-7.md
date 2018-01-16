
<!-- ======================================================================= -->
# Design (6) - conclusions

**TODO** -
issue - list of sections - elevate a t2 sectioning node to the same level a
t1 sectioning node has - also - the nodes of a t1 section are all descendants
of the t1 sectioning node

`[section, A, section, B, /section, C, /section]`

<!-- ======================================================================= -->
## sectioning nodes ()

**CLARIFICATION**
A sectioning node does not belong to its own section:
A consistent `Node.parentSection` property.

**TODO** -
don't associate sectioning nodes with the sections they declare -
`Section Node.parentSection` property would be inconsistent

<!-- ======================================================================= -->
## sectioning nodes ()

**CLARIFICATION**
A sectioning node does not belong to its own section:
Multi-step transformations.

**TODO** -
a practical issue -
transformations

<!-- ======================================================================= -->
## sectioning nodes ()

**CLARIFICATION**
A sectioning node does not belong to its own section:
Provides a "physical" connection to the subsection's parent section.

i.e. the defining node of a section's location -
strongly connected

describe the purpose of a sectioning node inside of presequent sections -
not associated with its declared section

<!-- ======================================================================= -->
## implementation specific

`Section Node.parentSection`

**CLARIFiCATION**
Because of that, an implementation does not have to always keep references to
all open sections at hand. That is, because an algorithm only needs to know
what the parent section of the next subsequent node is. 

**CLARIFICATION**

are being entered and (2) the section's default scope ends with the first
exit event of a presequent (i.e. with regards to the first node) and
unassociated node.

Note that the latter aspect already is
a hint towards how it has to be implemented.

<!-- ======================================================================= -->
## sectioning nodes (1)

**CLARIFICATION**
A sectioning node does not belong to its own section:
Less confusion with regards to a discussion.

If sectioning nodes would have to be associated with their own sections,
then there would always be the difficulty of having to distinguish between
(1) the first node that is associated with a section, which then is the
section's sectioning node and (2) the section's actual first content node.

<!-- ======================================================================= -->
## sectioning nodes (2)

**CLARIFICATION**
A sectioning node does not belong to its own section:
Non-Empty parent sections.

If all sectioning nodes would have to be associated with their own section,
then a section's sectioning node (and possibly also its descendant nodes)
would have to be skipped in order to reach the first actual content node.

If, in addition to that, a parent section would only contain a single
subsection, but no actual content node of its own, then a parent section
would appear to be empty. And, because of that, one would therefore always
also have to explicitly check for the existence of possible subsections.

Note that the sectioning node of a subsection would then only be associated
with the subsection it declares. That is, because each node can and will be
associated with one section only (although the sectioning node still counts
as being implicitly associated with all of its parent sections).

Because of that, the advantage of not associating a sectioning node with
its own section is that no parent section will ever appear to be empty. A
parent section will always have at least one content node and, because of
that, can never be mistakenly understood to be empty.

That is, there is no need to check the existence of possible subsections,
if the only question that needs to be answered is, whether the parent
section is empty or not. One only needs to check, if a node exists that
is strictly associated with the corresponding section.

* has subsections => has one or more strictly associates nodes => not empty
* not empty => does not necessarily have subsections
* has no nodes strictly associated with it => guaranteed to be empty
