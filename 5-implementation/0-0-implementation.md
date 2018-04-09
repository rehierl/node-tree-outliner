
<!-- ======================================================================= -->
# Implementation

Minor or isolated implementation specific aspects:

<!-- ======================================================================= -->
## general statements

**CLARIFICATION**
The sectioning node of a node's parent section
never is identical to the corresponding node itself.

```
(node.parentSection.sectioningNode !== node)
```

That is obviously true for any node which is not a sectioning node. However,
this expression is also true for sectioning nodes. That is, because no such
node is associated with the section it declares.

Note that, if a sectioning node would have to be associated with the section it
declares, then the first part of the above expression would be a self-reference.

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

Note that the above fragment traverses the `S{+}N` path, that begins with
the corresponding node. Traversing the `SN{+}` path from a node towards the
root node, and testing the parent section of each node along the way, is not
guaranteed to yield accurate results (i.e. false negatives are possible). That
is because, due to associating each node with one section only, type-2 sections
don't necessarily have to appear as the parent section of those nodes.
