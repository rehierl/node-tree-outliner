
<!-- ======================================================================= -->
# Node Tree <=> Strict Hierarchy

heavily builds upon

* basics / hierarchy of sets
* basics / hierarchy of sequences

unordered tree <=> hierarchy of sets

* a strict hierarchy of sets can be created based on an unordered tree
* such a strict hierarchy can be used to recreate the unordered tree

ordered tree <=> hierarchy of sequences

* a strict hierarchy of sequences can be created based on an ordered tree
* such a strict hierarchy can be used to recreate the ordered tree

ordered tree => hierarchy of sets <=> unordered tree

* the sequences within the strict hierarchy of an ordered tree are traces of nodes
* as such they represent ordered sets of nodes (visit each node exactly once)
* a hierarchy of sets can be created based on an unordered tree
* that hierarchy of sets however can not be used to recreate the node tree
* that is, because the node order is not stored within that hierarchy
