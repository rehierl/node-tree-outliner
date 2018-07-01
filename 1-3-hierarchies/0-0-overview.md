
<!-- ======================================================================= -->
# Node Tree <=> Strict Hierarchy

heavily builds upon setups/hierarchies of sets/sequences

* [basics / sets of sets](../1-basics/2-2-sets-of-sets)
* [basics / hierarchy of sets](../1-basics/2-3-hierarchy-of-sets)
* [basics / hierarchy of seqs](../1-basics/3-1-hierarchy-of-seqs)

unordered tree <=> hierarchy of sets

* a strict hierarchy of sets can be created based on an unordered tree
* that hierarchy can then be used to recreate the unordered tree

ordered tree <=> hierarchy of sequences

* a strict hierarchy of sequences can be created based on an ordered tree
* that hierarchy can be used to recreate the ordered tree

ordered tree => hierarchy of sets <=> unordered tree

* the sequences of the strict hierarchy of an ordered tree are traces of nodes
* they represent ordered sets of nodes (each node is visited exactly once)
* a hierarchy of sets can be created based on an unordered tree
* that hierarchy of sets however can not be used to recreate the node tree
* the tree's node order is not stored within that hierarchy
