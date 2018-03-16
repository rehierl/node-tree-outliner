
<!-- ======================================================================= -->
# How to implement ...

The following content is intended to clarify implementation specific aspects.

<!-- ======================================================================= -->
## top-level nodes

(related to the support of transformations)

associating a node (strict association) with a section is equivalent to
associating a whole subtree of nodes (implicit associations). -

two levels of implicitness -
implicitly with the explicitly associated section (associate a subtree),
and implicitly with the implicitly associated section (one section only)

can an algorithm easily store references to all top-level nodes? -
issue: associate with one section only (not that easy) -
issue: subsequent t2 with equal or higher rank (tricky) -

when a section is being closed, or as an on demand feature? -
is it possible to avoid having to determine them as a post-process
by providing a list of top-level nodes? -
e.g. `Node[] Section.getTopLevelNodes()` -

the first top-level node is easy to determine (entering) -
the last top-level node could be determined when closing a section -
after all, each section does have its own close event -
last child if closed by a parent container -
previous sibling when closed by a t2 sectioning node -

t2 -> t1 transformations must take into account, that
they could be the cause for new first and/or last top-level nodes -
the corresponding node references, if any, need to be updated

<!-- ======================================================================= -->
## test: is node 'n' associated with section 's'?

If node `n` is strictly associated with section `sX` (one reference per node),
and if the question is, whether node `n` is also associated with section `sY`,
then the expression `(sX == sY)` needs to be tested first. If that test fails,
then it needs to be tested whether section `sY` is an ancestor section of `sX`.

```
isAssociatedWith(Node node, Section section) begin
  parentSection = node.parentSection
  
  while(parentSection != null) begin
    if(parentSection == section) return true
    parentSection = parentSection.parentSection
  end
  
  return false
end
```

Consequently, node `n` is not associated with section `sY`,
if (and only if) all of the afore mentioned tests have failed.

Note that an implicit association is not guaranteed to be verified correctly
(i.e. false negatives are possible), if only the ancestor nodes of node `n`
are tested. That is, because type-2 sections can be hidden by that rooted
path of nodes.
