
<!-- ======================================================================= -->
# Nested set model

* see also - sequences / nested intervals

<!-- ======================================================================= -->
## wikipedia, nested set model

* a model/technique used to represent nested sets in relational databases
* nested sets - aka. hereditarily finite set, trees, hierarchies
* due to difficulties to express operations on hierarchies
* hierarchies may be expressed as graph databses

technique

* number the nodes according to a tree traversal
* visit each node twice - two numbers per node
* test hierarchy membership by comparing these numbers
* updating is expensive - requires renumbering
* avoid renumbering by using rational numbers - complicated

dynamic endless database tree hierarchy

* used in combination with elements that have very few attributes
* good for queries, not so good for updates
* needs additional tagging for multi-parent support
* implemented as nested intervals
