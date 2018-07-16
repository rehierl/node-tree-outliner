
<!-- ======================================================================= -->
# Design - type-2 sections

**QUESTION**
Would it be reasonable to allow a subsequent type-2 sectioning node to close an 
open presequent type-2 section before the end of its default scope is reached?

Note that the injection of inactive parent containers can not answer that
question. That is because only the default scope of an affected section is
changed, which is why any section will still end with its default scope and
not any sooner. In addition to that, the subsequent type-2 sectioning node
won't be the node that closes the corresponding presequent section.

Note that the following considerations focus on type-2 sectioning nodes only.
That is, they do not cover the question whether a type-1 sectioning node should
be allowed to close a type-2 section, nor if an inner type-2 sectioning node
should be allowed to close a type-1 section.

<!-- ======================================================================= -->

**TODO**
default definitions are rank-less

**TODO**
difference between type-1 and -2 sections -
type-1 is always rank-less? -
associate a rank with a rank-less node? -

could be allowed to close presequent type-2 sections -
as such, they would have an outer rank associated with them
