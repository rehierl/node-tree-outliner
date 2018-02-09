
<!-- ####################################################################### -->
<!-- ======================================================================= -->
# Design (9) - type-2 sections

**QUESTION**
Would it be reasonable to allow a sectioning node to close a type-2
section before the end of its default scope is reached?

difference between type-1 and -2 sections

<!-- ####################################################################### -->
<!-- ======================================================================= -->
# Design (9) - stack of open sections

**CLARIFICATION**
The path/stack of open sections is a rooted path in the tree of sections.

* contains all currently open sections
* connects the root section with the current section
* a presequent path of sections contains closed sections
* a subsequent path of sections contains subsequent sections
