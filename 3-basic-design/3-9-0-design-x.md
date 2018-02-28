
<!-- ======================================================================= -->
# Design - type-2 sections

**QUESTION**
Would it be reasonable to allow a subsequent type-2 sectioning node to close an 
open presequent type-2 section before the end of its default scope is reached?

Note that the injection of inactive parent containers can not answer that
question. That is, because only the default scope of an affected section is
changed, which is why any section will still end with its default scope and
not any sooner. In addition to that, the subsequent type-2 sectioning node
won't be the node that closes the corresponding presequent section.

Note that the following considerations focus on type-2 sectioning nodes only.
That is, they do not cover the question whether a type-1 sectioning node should
be allowed to close a type-2 section, nor if an inner type-2 sectioning node
should be allowed to close a type-1 section.

<!-- ======================================================================= -->
## parent containers

As mentioned before, a section's parent container isn't a parent container
because the definition of the corresponding node has certain characteristics.

Any parent node is a parent container, if it is a type-1 sectioning node, or
if it has type-2 sectioning nodes as child nodes. Consistent dynamic support
could otherwise not be guaranteed (i.e. sections can not be allowed to reach
past their parent containers). In short: Any parent node can become a section's
parent container, regardless of its specific definition.

Because of that, such parent containers exist whether they are manually
injected (explicit), or due to structural circumstances (implicit).

Note that a node can be defined to never be a section's parent container, if
(and only if) the node is not allowed to have type-2 sectioning nodes as child
nodes (e.g. type-2 sectioning nodes). However, a general purpose implementation
is unaware of these kind of additional definitions. That is, in case of input
errors, an implementation will still treat these nodes as parent containers.

**case 1: (node level 1 >> node level 2)**

```
      n0
 ------------
 n1        n2
----
 n3
```

* `n1` is an inactive container node
* `n2, n3` are type-2 sectioning nodes

If a presequent sectioning node `n3` has a higher node level than the next
subsequent sectioning node `n2`, then the default scope of `s3` ends before
`n2` is entered. That is, `s3` and `s2` are, by structural relationship,
independent from each other. Consequently, `n2` can not have any effect on
`s3`. That is, `s2` can not be a subsection to `s3` and `n2` can no longer
close `s3` (as it is already closed when `n2` is being entered).

Note that, from the perspective of this design, this case is a non-issue. That
is, because sections will be ignored by subsequent operations as soon as they
are closed. Because of that, any such modified definition (with regards to `n2`)
is not understood to be with regards to `n3/s3`, but with regards to some other
open presequent section. Consequently, modified definitions may yield unexpected
results, if the above structural aspect is not correctly taken into account.

However, certain conditions may still yield a seemingly identical result. If
that is the case, the reasons for those matching results differ none the less.

**case 2: (node level 1 << node level 2)**

```
      n0
 ------------
 n1        n2
          ----
           n3
```

* `n2` is an inactive container node
* `n1, n3` are type-2 sectioning nodes

If, in contrary to that, the next subsequent sectioning node `n3` has a higher
node level than a presequent sectioning node `n1`, then `n3` has an ancestor
that is a top-level node of `s1`. Consequently, `s3` is by implicit association
a subsection to `s1`. Because of that, and in order to avoid conflicting
statements, any attempt to close `s1` when `n3` is being entered, must be
ignored. That is, `s3` can not be independent of `s1` (e.g. a sibling section
to it).

**case 3: (node level 1 == node level 2)**

```
      n0
 ------------
 n1        n3
----      ----
 n2        n4
```

* `n1, n3` are inactive container nodes
* `n2, n4` are type-2 sectioning nodes

Note that this case can be understood to contain two subsequent subtrees that
have `n1` and `n3` as their root nodes. Because of that, this case is similar
to case 1: `s2` will be closed before `n4` is even entered.

Note that the node levels of the corresponding sectioning nodes don't have to be
identical for as long as both nodes are located within two different subtrees.
The effect will still be covered by case 1: `s2` will be closed before `n4` is
entered.

**case 4: (same parent container)**

```
      n0
 ------------
 n1        n2
```

* `n1, n2` are type-2 sectioning nodes

However, `n2` is in principle free to close the open presequent section `s1`,
if (and only if) both type-2 sectioning nodes have the same parent node (i.e.
the same parent container).

Note that the actual parent section of `s2` can then only be one of the
remaining open sections, which all are presequent to `s1` (i.e. ancestor
sections of `s1`).

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
Parent containers have significant impact on the use of extended definitions.

Note that the above considerations have precedence over any extended definition.
That is, such non-default definitions must be ignored, if they are in conflict
with structural dependencies. Hence, the use of such definitions is limited.

Note that this can be understood as an indication that, in principle, the
default definitions have precedence over any non-default definition. That
is, such definitions must not be in conflict with the default definitions.

**CLARIFICATION**
In order for non-default definitions to not yield any conflict, or an
unexpected result, the corresponding type-2 sectioning nodes must have
the same parent container.

**Mind hook**
The placement of sectioning nodes is significant.

<!-- ======================================================================= -->

**TODO**
"extended" rather than "modified" definitions -
just a naming related aspect

**TODO**
default definitions are rank-less

**TODO**
difference between type-1 and -2 sections -
type-1 is always rank-less? -

could be allowed to close presequent type-2 sections -
as such, they would have an outer rank associated with them
