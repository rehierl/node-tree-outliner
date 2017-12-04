
<!-- ======================================================================= -->
# Associate nodes while entering

If nodes would have to be associated while they are being exited, the following
associations would have to be made:

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
  </div>                 => D
</body>
```

Note that the above `div` container would have to be strictly associated with
section `D`. Because of that, any node within that container would automatically
loosely belong to section `D`. Consequently, node `C` also loosely belongs to
section `D`.

Obviously, this implicit relationship of node `C` with section `D` violates the
fundamental rule that a sectioning node must only affect subsequent nodes. In
addition to that, section `D` is undefined while node `C` is being entered and
while it is being exited.

Again, these kind of implicit associations can not be undefined because they
will be established as soon as any ancestor node is strictly associated with
a section.

**CLARIFICATION** Any node must be associated while it is being entered.

```
                         strict associations
example fragment         (while entering)
----------------         ------------
<body>
  <h1>A</h1>             => body
  B                      => A
  <div>                  => A
   C                     => A
   <h2>D</h2>            => A
   E                     => D
  </div>
</body>
```

Clearly, associating nodes while they are being entered will not produce these
kind of conflicts.
