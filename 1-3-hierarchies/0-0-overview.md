
<!-- ======================================================================= -->
# Directed Node Tree <=> Strict Hierarchy

unordered tree <=> hierarchy of sets

* a strict hierarchy of sets can be created based on an unordered tree
* that hierarchy can then be used to recreate the unordered tree

ordered tree <=> hierarchy of sequences

* a strict hierarchy of sequences can be created based on an ordered tree
* that hierarchy can be used to recreate the ordered tree

ordered tree => (hierarchy of sets <=> unordered tree)

* the sequences in the strict hierarchy of an ordered tree are linear sequences
* these represent ordered sets of nodes (each node is visited once)
* a hierarchy of sets can be created based on an ordered tree
* this hierarchy can not be used to recreate the ordered tree
* the tree's node order is not stored within the hierarchy
* this hierarchy can however be used to create an unordered tree
* the initial ordered tree and the created unordered tree have the same
  tree-order, but differ in child order (the unordered tree has no such order)
