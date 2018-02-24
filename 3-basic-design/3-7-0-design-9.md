
**TODO**
swap design-8 with design-9 -
current-section requires a section-hierarchy

<!-- ======================================================================= -->
# Design (8) - section hierarchy

The following content is intended to clarify that the default
definitions are sufficient to define any section hierarchy.

Note that the definitions of sectioning nodes do not include the characteristic
to close any open presequent section. Consequently, a subsequent section is a
subsection to all sections that are open by the time its sectioning node is
entered. And, because of that, a 

Note also, that any section always ends with its parent container (i.e. with
its default scope).

<!-- ======================================================================= -->
## type-1 sectioning nodes

```
              n0
==============================
n1            n5            n9
-----------   -----------
   n2    n4      n6 n7
   -----            -----
      n3               n8
```

* nodes `n0-9` are type-1 sectioning nodes
* nodes `n0-9` declare sections `s0-9`

Processing this fragment will, according to the default definitions,
result in the following tree of sections:

```
s0 -|- s1 -|- s2 - s3
    |      |- s4
    |
    |- s5 -|- s6
    |      |- s7 - s8
    |
    |- s9
```

<!-- ======================================================================= -->
## type-2 sectioning nodes

<!-- ======================================================================= -->
## combining both types

That is, mixing both types of sectioning nodes.

<!-- ======================================================================= -->
## derived statements

**CLARIFICATION**
The default definitions are consistent with implicit associations.
