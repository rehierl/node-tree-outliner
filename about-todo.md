
## Heading X introduces section X

Assume that any heading element can be identified by the heading's inner nodes,
or some other unique characteristic (e.g. the heading's `id`).

The intention behind this definition is to identify a section by the heading
element that introduced it. Note that each heading element always introduces a
single section (i.e. never more than one).

A reference of the form "section `A`" therefore refers to the section introduced
by the corresponding heading element.

## Heading X of section Y

If a section `A` is introduced by heading element `A`, then that heading element
is also said to be the heading of that section.

## Node X (is located inside | belongs to | is associated with) section Y

Node `B` is said to be located inside section `A` because there is nothing that
introduces a new section in between heading `A` and node `B`. There is also
nothing that indicates that section `A` ends before node `B` is reached.

If a node is located inside a section, then it is also said to belong to, or to
be associated with, that section. In such a case, the node and its section are
both said to have a direct relationship.

Note that this definition is based upon the direct relationship between a node
and its section (i.e. no subsections in between).

## Section X (contains | is associated with) node Y

Section `A` contains node `B` because node `B` is located inside section `A`.

If a node is located inside a section, then that section is said to contain, or
to be associated with, that node.

Note the direct relationship between the node and its section.

## Element X contains section Y

A container element `X` contains section `Y` as an inner section, if `X` is the
section`s parent container. **TODO** - based on container - excludes subsections

## Section X (is located inside | belongs to | is associated with) container Y

A section is said to be located inside of its parent container.

In addition to that, a section can also be said to be belong to, or to be
associated with its parent container element.

Note that a section's belongs-to-node (outwards) and contains-node (inwards)
associations have different direction!
