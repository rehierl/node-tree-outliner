
<!-- ======================================================================= -->
# Design - close modifiers

close-n-value - absolute - bottom-up perspective
depth-value - absolute - top-down perspective
rank-value - absolute or relative - eq. depth if absolute

it is in principle possible to mix different types of close modifiers -
the algorithm will treat each modifier as an isolated instruction -
i.e. always with regards to the current path of sections -
but, if relative, could depend on section properties? -

<!-- ======================================================================= -->
## close N sections values

> `<node close="N">`,
> where `N in [0,*]`

<!-- ======================================================================= -->
## depth values

> `<node depth="N">`,
> where `N in [1,*]`

<!-- ======================================================================= -->
## rank values

> `<node rank="N">`,
> where `N in [1,*]`

<!-- ======================================================================= -->

**DEFINITION**
The rank of a section is the number of its ancestor sections -
or better outline depth

Note that the universal section is always included. That is, the root section
has rank 1 and the universal section has rank 0. Note also that this is similar
to a node's node level within a tree of nodes. That is, the root node has node
level 1.

plot twist: sections have no rank

a rank value, absolute or relative, represents a top-down perspective -
a close-n-sections value represents a bottom-up perspective -
the former is more user friendly than the latter

**type-1 sectioning nodes**
they can in principle also have a rank value -
however a subsequent t1 section can not become
a subsection of a closed presequent t1 section -
rank values are with regards to open sections -
a t1 rank can only refer to presequent t2 sections -

plot twist: a rank value is essentially a user-defined outline depth

i.e. add the section to the tree such that it has the given outline depth -
that is the top-down perspective - close the last couple of open section such
that the section has the given outline depth - bottom-up perspective -

rank only with regards to the outline depth -
not a presequent rank-infected sectioning node? -
what would be the difference if any?

plot twist: the essence of a rank value is to instruct to close sections

<!-- ======================================================================= -->
## conditional modifiers

HTML's sectioning content nodes are defined as -
subsection-of the nearest ... -
if deep into the structure, then close multiple sections -
if shallow, then close just a few, if any -
i.e. context-dependent - inconsistent? -
an implicit, constant, case-dependent close modifier? -
