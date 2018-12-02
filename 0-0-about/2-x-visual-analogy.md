
<!-- ======================================================================= -->
# An easy 3D analogy

- a 2D analogy might be easier to follow?

<!-- ======================================================================= -->
## 3D objects

- imagine some 3 dimensional (3D) volume
- i.e. an object of sorts
- e.g. a cube

atoms

- any object consists of a set of fundamental elements, its atoms
- imagine these atoms to all be aligned such that any atom has 6 neighbors
- i.e. forward, backward, up, down, left, right
- any atom has 6 atoms to which it is directly connected

voxels in computer graphics

- the atoms of an object are analogous to 3D points space
- i.e. each atom represents a single, indivisible unit, a voxel
- as such, any object is understood as a 3D grid of atoms/voxels

siblings

- any atom has additional 8 atoms that are close
- e.g. move to the next right neighbor, and then to the next upper neighbor
- two atoms that are close to each other are similar to the nodes in a tree
- such nodes aren't directly next, but still close to each other
- i.e. move to the parent, and then to the next sibling

<!-- ======================================================================= -->
## slices and cubes

sets of slices

- cut the whole object into a set of parallel slices
- e.g. horizontally (1), vertically (2) and in depth (3)
- pick a set and rejoin all the slices in it
- you will get the initial object

consistency

- any set of slices allows to reconstruct the initial object
- you won't get object-1 from set-1 and some distinct object-2 from set-2
- you will always get the exact same object
- that is consistency

set of cubes

- pick one slice from each set and take the intersection
- the intersection of these three slices is a cube
- i.e. provided that all slices have the same thickness
- do this for every possible combination
- you will get a set of cubes (4)
- rejoin all the cubes in that set
- you will get the initial object

in general

- each such set represents a complete description of the initial object
- these representations must all accurately describe the exact same object
- i.e. it must be possible to reconstruct the object from any such set

<!-- ======================================================================= -->
## groups of atoms

groups of atoms

- any of the above sets consists of elements (slices/cubes)
- any such element represents a group of atoms

the groups in a set

- all the elements in a set are disjoint
- i.e. any atom belongs to one and only one group
- any of the above sets is a partition of all the atoms

subgroups of atoms

- any slice in sets (1) to (3) represents a group of cubes from set (4)
- like any cube, the cubes in a slice represent groups of atoms
- i.e. a slice is a group of cubes
- i.e. the cubes in a slice act as the atoms of a slice
- i.e. the cubes act as the smallest, indivisible units of a slice
- atoms-to-cube like atoms-to-molecule
- cube-to-slice like molecule-to-cell

the cubes in a slice

- any cube in a slice is entirely inside of its slice
- i.e. every atom in a cube is also an atom within the slice
- any cube belongs to one and only one slice in a set of slices
- i.e. a cube either belongs entirely to a slice, or it does not
- i.e. disjoint ex-or related, i.e. no overlap
- any set of slices is a partition of all the cubes

subgroups of a group

- any cube in a slice is a subgroup of atoms to the slice
- the cubes in a slice can be joined into even larger groups
- note - can only join adjacent cubes - i.e. must be connected
- like the cubes, these groups are also subgroups to the slice

<!-- ======================================================================= -->
## node trees are similar

nodes in a tree

- the leaf nodes of a tree are its atoms
- the internal nodes of a tree are its molecules

sets of elements

- the hierarchy of sets represents a tree
- the hierarchy of subtrees represents a tree
- the hierarchy of rooted paths represents a tree
- the hierarchy of sections must represent the initial tree
- all of these must accurately describe the initial tree
