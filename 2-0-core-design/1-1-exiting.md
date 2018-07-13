
<!-- ======================================================================= -->
# Associate nodes while exiting

( Note that the following considerations are based upon the common practice
to not end a section with its parent container element. However, associating
nodes while they are being exited would still have issues, even if any section
would have to end with its parent container element (i.e. end with its parent
container, but still associate nodes while exiting them). In that case, an
issue would be to not have any guarantee with regards to the first node being
associated with a section. )

If nodes would have to be associated while they are being exited,
the following associations would have to be established:

```
                         strict associations
example fragment         (while exiting)
----------------         ------------
<body>
  <h1>A</h1>             => body
  B                      => A
  <div>
   C                     => A
   <h2>D</h2>            => A
   E                     => D
   <h3>F</h3>            => D
   G                     => F
  </div>                 => F
</body>                  => F
```

In this case, the above `div` container must be associated with section `F`.
Because of that, any node within the `div` container automatically loosely
belongs to section `F`.

The above example therefore has multiple conflicts ...

* The `div` container is associated with a section that is undefined
  in the `div` container's context. That is because section `F` is
  declared by a subsequent sectioning node (i.e. heading `F`).
* Nodes `C` through `E` are obviously affected in a similar fashion.
* Heading `F` is implicitly associated with its own section.
* Section `F` can be understood to declare itself and, as such,
  to be a subsection of itself (i.e. cyclic hierarchy).
* Section `D` (a superordinate section) is declared by a node that
  implicitly belongs to section `F` (a subordinate section). Because
  of that, section `D` can be understood to be a subsection of its
  inner section `F` (i.e. a subsection of its subsection). 
* In general: Section/heading `F` has an effect on presequent nodes.

Again, these kind of loose associations can not be undefined, because they
will be established as soon as any ancestor node is associated with a section.

```
                         strict associations
example fragment         (while entering)
----------------         ------------
<body>                   => universe
  <h1>A</h1>             => body
  B                      => A
  <div>                  => A
   C                     => A
   <h2>D</h2>            => A
   E                     => D
   <h3>F</h3>            => D
   G                     => F
  </div>
</body>
```

Clearly, associating nodes while they are being entered will not produce these
kind of conflicts. However, this does by itself not guarantee that there are
no further issues:

```
                         strict associations
example fragment         (while entering)
----------------         ------------
<body>                   => universe
  <h1>A</h1>             => body
  B                      => A
  <div>                  => A
   C                     => A
   <h2>D</h2>            => A
   E                     => D
  </div>
  F                      => D
</body>
```

Because of that, section `D` can not be treated as a single entity. That is,
the content nodes of that section can not be grouped together without changing
the structure of the node tree.
