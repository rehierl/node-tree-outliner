
<!-- ======================================================================= -->
# Design - outline depth/height

Note that there is no formal definition for the width of a node/section tree. In
addition to that, this metric does not seem to have any substantial application.
Hence, a proper definition is not available.

<!-- ======================================================================= -->
## outline depth/height

**CLARIFICATION**
The outline depth of a section is "1 + the number of its ancestor sections"
(not counting the universal section). That is, starting with an outline depth
value of 1, the higher the value, the deeper within the section hierarchy a
section is located.

That is, the root section has an outline depth value of 1, its child sections
an outline depth value of 2, and their child sections an outline depth value
of 3.

In other words, the outline depth of a section is the length (in terms of the
number of sections involved) of the rooted path of sections that ends in the
corresponding section. Note the edge case of a rooted path of length 1 (i.e.
restricted to the root section only).

Note that the node level of a node is defined as "1 + the number of edges in
between the node and the tree's root" (In short: "1 + the number of ancestors
that a node has"). Because of that, the term "outline depth" is, in the context
of a section tree, synonymous to "node level". Consequently, the outline depth
of a section can also be referred to as the section's "outline/node level".

**CLARIFICATION**
The outline depth (or level) of a node is the outline depth of its parent
section (with regards to one association per node).

Note that the outline depth of the root node is 0. That is, because the root
node does not have such a parent section (not counting the universal section).
Likewise, the outline depth of any unassociated node is 0.

**CLARIFICATION**
The outline height of a section is the distance to its furthest descendant
leaf section. That is, the number of jumps/edges between that leaf and the
corresponding section.

Because of that, the height of a leaf (or empty) section is 0, the height of a
section which only contains a single empty child section is 1, and the height
of a section which only contains has such a subtree (i.e. a child section that
itself only has one empty child section) is 2.

Note that, similar as above, and in the context of a section tree, the term
"outline height of a section" is synonymous to the "height of a node".

Note that, in contrary to the outline depth of a node, a node in the node tree
can not have an "outline height". That is, because a node does not strictly
have a descendant section (although declared sections can be understood to be
subordinate to their sectioning nodes).

**CLARIFICATION**
The outline height of a section tree is the outline height of its root section.

<!-- ======================================================================= -->
## height map

```
            n0
============================
n1 n2                  n8 n9
   ------------------
      n3 n4        n7
         --------
            n5 n6
```

* `n0` is a type-1 sectioning node
* `n2,n4` are inactive parent containers
* `n1,n3,n5-6,n7,n8-9` are type-2 sectioning nodes
* `s6,s7,s9` are empty sections

Processing this fragment according to the default definitions
will result in the following section tree:

```
s0 - s1 -|- s3 -|- s5 - s6
         |      |- s7
         |
         |- s8 - s9
```

The associations of the tree's nodes with these sections are as follows:

```
y-axis
4 |                   ==            - s5
3 |             ===========    ==   - s3, s8
2 |       =======================   - s1
1 |    ==========================   - s0
0 | =============================   - u(niversal)
  --------------------------------- x-axis
    n0 n1 n2 n3 n4 n5 n6 n7 n8 n9
```

Note that the x-axis represents the corresponding node (e.g. via its index
within the node sequence) and the y-axis the outline level of that node.

As such, the outline level can be understood to shift a node into the next
dimension by associating a height value with it. That is, the outline level
allows to turn a one-dimensional (short: 1D) ordered listing of nodes into
a 2D graph, which can be referred to as the node tree's 2D height map.

Note that the 2D height map could be displayed e.g. instead of a textual,
low resolution overview, which some editors allow to use in addition to,
or instead of a scrollbar (i.e. a self-contained representation).

Note that, with the exception of the root node, each node has a well defined
outline level. Because of that, the above relation (i.e. `R := "index x level`)
is left-total. That is, if the root node is defined to have an outline level
value of 0.

Similar to that, and if the nodes of a node tree are drawn onto a flat, 2D
surface (the node level on the x-axis, the node's level internal width index
on the y-axis), then the node's outline level can be used to shift the nodes
into the 3rd dimension (the node's outline level on the z-axis). This can
then be understood as the 3D height map of the corresponding node tree.

Another way to display the outline depth, and therefore to visually indicate
the associations, is to indent the textual definition of the node tree by the
display of an inner border (i.e. an integrated representation):

```
outline depth      node tree
 1 2 3 4
================   ================
                   <n0>
 |                   <n1/>
 | |                 <n2>
 | |                   <n3/>
 | | |                 <n4>
 | | |                   <n5/>
 | | | |                 <n6/>
 | | |                 </n4>
 | | |                 <n7/>
 | |                 </n2>
 | |                 <n8/>
 | | |               <n9/>
                   </n0>
```

Note that this border represents the node tree's transposed 2D height map.

<!-- ======================================================================= -->
## derived statements

Question: Could a metric be defined in order to classify node trees?
If so, this metric could be used to estimate a document's "quality".

* How much content (in terms of nodes per section)?
* Are document's sections in general overloaded, or barely filled?
* Few sections with almost all content, or evenly distributed?
* Is the tree's height map smooth or steep?

**Memory hook**
(2D) The height map is similar to stacking wood planks: The greater the
value, the shorter the wood plank. (3D) Similar to that, the horizontal
cross sections of a mountain decreases in size/surface the higher that
cross section is located.
