
<!-- ======================================================================= -->
## HTML's reason

```
fragment             assoc-1    assoc-2
================     =======    =======
<t1>                 A          U
  <t2:R> A </t2>     A          U
  B                  A          U A
  <t2:R> C </t2>     C          U A
  D                  C          U A C
</t1>                A          U
```

* the first element of heading content defines a section's heading/title
* does not state anything about a heading's rank (R)
* no indication that the 1st heading's rank is relevant in any way
* however, if the 2nd heading's rank has equal or higher rank, the initial
  section is closed and a sibling section (implied section) is created
* consequently, the 1st heading's rank is relevant to the internal structure
* this is what forces an outline to be a list of sections

In other words: HTML's current structure of sections is dictated by the rank
of heading content elements, an addition to the default/base definition.

* looks the same - must act the same - wrong
* the default/base definition must define the overall structure
* and no addition must be allowed to deviate from it
* additions must respect the default case, not vice versa

section+heading

* section+heading won't work
* irritating as the 2nd heading (same rank) needs to be a subsection
* the actual reason behind this decision - less irritating for authors?
* courtesy to authors while ignoring implementations/theory?
* the title element should be used for the 1st section's heading/title

inconsistent transformations (t2 -> t1)

* the section element is defined as a subsection to the next upper t1 section
* not that accurately defined, but that is what the algorithm implements
* in contrary to t2 nodes, a t1 node does not end a parent t1 section
* the above t2 sequence can therefore not be transformed into a t1 sequence
* a transformation must tear the parent t1 node apart into two sibling t1 nodes
* transforming those t1 nodes back into t2 nodes can not result in the original
  fragment - the initial parent t1 node is lost
* i.e. inconsistent

does a t1 section need/have a rank?

* or is this a t2-only property?
* HTML's approach uses the (arbitrary) rank only internally
* has no effect whatsoever on any outer section

<!-- ======================================================================= -->
## the h element

* the `<h>` element
* what would be the rank of the H element?
* highest or lowest rank?

explicit parent containers

* the use of explicit parent containers can be used to support any hierarchy
* due to implicit associations, the section will always be a subsection
* regardless of what the element's rank is

highest rank (infinity)

* a sequence of H elements defines a flat list of sibling sections
* consistent with HTML's current design (not an argument)
* this seems to be the better choice

lowest rank (epsilon)

* a sequence of H elements defines the tree of sections to be a rooted path
* matches the default definition of a rank-less type-2 sectioning node

<!-- ======================================================================= -->

issue implied headings
