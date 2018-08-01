
**TODO** - (open aspects)

* currently just a "summary" of thoughts

<!-- ======================================================================= -->
# Common properties

A unique point of view: The elements within a CSS are no "object properties",
they are "object identifiers". That is, any CE can be seen as a reference to
data that is unique to a set. This allows to associate a property with a set
that may hold the same value as the property of another set (e.g. a tag name).

The CSS of a set can obviously be considered to represent data which is "unique"
to that set. That is because there is always exactly one least significant set
which holds all the elements in that CSS. As such, the non-empty CSS of a set
can be understood to further characterize the corresponding set.

<!-- ======================================================================= -->
## One or more elements per CSS (???)

* a set of elements E allows to create subsets in P(E)
* these subsets are combinations of elements in E
* instead of unique single elements, such subsets could be used
* i.e. `(V subset-of E)` 
* i.e. single unique elements vs. unique sets of elements
* because E does not need to have as many elements as V
* hint, a CSS is still a set of elements
* what are the implications ?

the issue

* as elements of the parent set, any element in a css
* contributes to the relationships each set has with all the other sets

possible intermediate step

* one globally unqiue element per set
* in addition to that, non-unique elements
* the combination is still globally unique
* i.e. no other set will have the same combination

<!-- ======================================================================= -->
## Global, Local, Characteristic data (???)

characteristic data

* the characteristic subset of a set could be understood
  to represent data that is "unique" to the corresponding set

global data ?

* obviously, it is possible to add an element to all the sets
  within a hierarchy without changing the hierarchy itself
* such elements can be considered to have global scope
* possible to detect/retrieve - common to all leaf nodes

local data ?

* if it is possible to have global data, then it should also
  be possible to have data that is characteristic to a sub-tree
* after all, a sub-tree can then have "global" data that is
  scoped to the sub-tree

relevant to sections ?

* could be used to proof that -
  "a section contains a node an all of its descendants"
* see such an element as a flag that states -
  "this set belongs to that section" -
  and because each descendant set is a subset,
  any descendant set must also have that element -
  as such, any descendant set is automatically
  flagged to belong to the very same section.
* if true, sections are embedded into the tree
