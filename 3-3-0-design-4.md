
<!-- ======================================================================= -->
# Design (4)

As mentioned before, the last node of a section can not be clearly defined
because any associated node can have any number of descendant nodes.

The next question therefore is: Is it possible to define the end of a section
without a clear definition of the section's last node?

<!-- ======================================================================= -->
## intervals of real numbers

The answer to the above question is similar to the definition of intervals
on the set of real numbers. That is, because in between any two real numbers,
there always is an infinite amount of additional numbers.

Apart from a specific and included upper boundary, it is possible to define
an interval of real numbers by exclusion: `r in [a,b)`. This definition's
meaning is that `r` may have any value in between `a` (inclusive) and `b`
(exclusive). Put differently, any number from `a` to `(b - e)` is included
(with `e` representing an infinitesimal small positive number).

The initial question can therefore be rephrased: Is it possible to clearly
define the end of a section in terms of an event, beginning with which no more
associations with a given section are allowed (i.e. definition by exclusion)?

<!-- ======================================================================= -->
## set of open sections

As mentioned earlier, and without the ability to limit a section's scope, a
tree's last subsequent node would have to be associated with all the known
sections. Obviously, authors need the means to tell an algorithm when it is no
longer allowed to associate any nodes with a given section. Once these kind of
statements are detected, an algorithm must mark the corresponding section, or
multiples thereof, as being "closed".

Consequently, and at any given point in time, any section within the set of
known sections are "initialized", "open" or "closed". Because of that, the set
of known sections `S` can be broken apart into three disjunct sets of sections
(with each set containing only those sections that are marked with the
corresponding state):

* the set of initialized sections `IS`
* the set of open sections `OS`
* the set of closed sections `CS`.

With regards to associations, a section's "initialized" and "closed" states
appear to be semantically equivalent, because no associations are allowed
for as long as a section's state is not "open".

<!-- ======================================================================= -->
## available events

The first events possible, that can be used to end a given section are the exit
events of the last node's ancestors.

<!-- ======================================================================= -->
## Sectioning nodes - last nodes (3)

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

<!-- ======================================================================= -->
## TODOs

**TODO**
a section's reduced sequence allows transformations -
how to determine the top-level nodes of a section

**TODO**
complete and reduced sequences are unique to their section -
no other section has the exact same sequences -
depends on the definitions of sectioning nodes

**TODO** -
can a node be allowed to have any effect on itself
(e.g. associate with its own section)?
