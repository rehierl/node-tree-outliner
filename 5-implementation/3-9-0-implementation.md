
<!-- ======================================================================= -->
# Implementation specific aspects

The following content is intended to clarify implementation specific aspects.

<!-- ======================================================================= -->
## general statements

**CLARIFICATION**
The sectioning node of a node's parent section
never is identical to the corresponding node itself.

```
(node.parentSection.sectioningNode !== node)
```

That is obviously true for any node which is not a sectioning node.
However, this expression is also true if the node is a sectioning node.
That is, because no such node is associated with the section it declares.

Note that, if sectioning nodes would have to be associated with their
own section, then the first part of the above expression would be a
self-reference, if the node in question would be a sectioning node.

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

Note that the above fragment traverses the `S{+}N` path,
which ends in the given node.

Note that an implicit association is not guaranteed to be verified correctly
(i.e. false negatives are possible), if only the ancestor nodes of node `n`
are tested. That is, because type-2 sections can be hidden by that rooted
path of nodes.
