
<!-- ======================================================================= -->
# Design (5)

As mentioned before, the last node of a section can not be clearly defined
because any associated node can have any number of descendant nodes. That is,
unless a definition is allowed to force a specific pattern upon the node tree.

**NEXT OPEN QUESTION**
Is it possible to define the end of a section without a clear definition of
the section's last node?

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
A non-empty section can always be said to end with its last top-level node.
If this top-level node has any descendants, then the section's last node is
the last subsequent descendant of this top-level node.

With that in mind, a section can also be seen to end inside of an associated
container, if the last subsequent descendant of that container (e.g. node `E`)
is the section's last node. However, this perspective could be misleading,
because a section can only end with the very last subsequent descendant
(i.e. not some arbitrarily selected descendant).

**CLARIFICATION**
A non-empty section can be said to end with an unrelated container (i.e.
an ancestor), if the section's last node is the container's last subsequent
descendant. Consequently, an unrestricted section can be said to end with
the tree's initial root node.

**CLARIFICATION**
The last node of a non-empty section will always be a leaf (either by strict,
or by loose association). Put differently, the last node of a section will
never be a parent node.

That is, because the last descendant entered will always be a leaf. After all,
a section's last node would not be the section's last node, if it were a parent.

No such clarification can be derived for the first node of a section. That is,
because the first node of a section depends on the definition of the section's
sectioning node. In addition to that, such a definition should in general be
independent of the structure of a tree.

**CLARIFICATION**
It is in general not possible to clearly identify and, because of that, to
clearly define the last node of a section. Obviously, the same also applies to
the relationship between a section's first and last node.

That is, because any associated node can have any number of descendant nodes.
It is therefore not possible, from a definition's point of view, to clearly
define a section's last node. That is, unless a certain structure is forced
upon the nodes of a section. Obviously, the latter must be avoided.

<!-- ======================================================================= -->
## intervals of real numbers

The answer to that question is similar to the definition of intervals on the
set of real numbers. That is, because in between any two real numbers, there
always is an infinite amount of additional numbers.

Apart from a specific and included upper boundary, it is possible to define
an interval of real numbers by exclusion: `r in [a,b)`. The meaning of this
definition is that `r` may have any value in between `a` (inclusive) and `b`
(exclusive). Put differently, any number from `a` to `(b - e)` is included
(with `e` representing an infinitesimal small positive number).

The initial question can therefore be rephrased:

Is it possible to define the end of a section in terms of an event, beginning
with which no more association is allowed (i.e. definition by exclusion)?

<!-- ======================================================================= -->
## set of open sections

As mentioned earlier, and without the ability to limit a section's scope, a
tree's last subsequent node would have to be associated with all the known
sections. Obviously, authors need the means to tell an algorithm when it is no
longer allowed to associate any nodes with a given section. Once these kind of
statements are detected, an algorithm must mark the corresponding section, or
multiples thereof, as being "closed".

Consequently, and at any given point in time, any section within the set of
known sections is "initialized", "open" or "closed". Because of that, the set
of known sections `S` can be broken apart into three disjunct sets of sections
(with each set containing only those sections that are marked with the
corresponding state):

* the set of initialized sections `IS`
* the set of open sections `OS`
* the set of closed sections `CS`.

With regards to associations, a section's "initialized" and "closed" states
appear to be semantically equivalent. That is, because no associations are
allowed for as long as a section's state is not "open".

<!-- ======================================================================= -->
## available events

The first events possible, that can be used to end a given section are the exit
events of the last node's ancestors.

<!-- ======================================================================= -->
## Sectioning nodes (3) - last nodes

Consequently, the general definitions mentioned below define the default scope
for certain types of sectioning nodes. However, it is still allowed to define
additional characteristics (e.g. rank of a heading) which further limit the
scope of a presequent sectioning node.

<!-- ======================================================================= -->
## Sectioning nodes

```
r x ... x n1 x ... x n2:s
        x n3 x ... x n4:s
--- (includes)
<n1>
  <n2:s> ... </n2:s>
</n1>
<n3>
  <n4:s> ... </n4:s>
</n3>
```

<!-- ======================================================================= -->

```
r x ... x n2:s
        x n4:s
--- (includes)
<n2:s> ... </n2:s>
<n4:s> ... </n4:s>
```

<!-- ======================================================================= -->

```
r x ... x n2:s
        x n3 x ... x n4:s
--- (includes)
<n2:s> ... </n2:s>
<n3>
  <n4:s> ... </n4:s>
</n3>
```

<!-- ======================================================================= -->

```
r x ... x n1 x ... x n2:s
        x n4:s
--- (includes)
<n1>
  <n2:s> ... </n2:s>
</n1>
<n4:s> ... </n4:s>
```
