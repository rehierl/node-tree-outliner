
<!-- ======================================================================= -->
# node-tree-outliner

The purpose of this repository is to flesh out a design that can be used to
implement a general-purpose outline algorithm for any rooted ordered tree of
nodes.

This repository is **in a state of flux**. It may and will change considerably
over time. (Direct links to files within this repository will break without
further notice).

<!-- ======================================================================= -->
## Overview

[0. about](./0-0-about): This folder holds general background information.

[1. mathematics](./1-0-mathematics) - Basic mathematical definitions:
values, variables, sets, sequences, types/domains, etc.

* [1.1. relations](./1-1-relations) - Definitions with regards to relations
  and ordered sets.
* [1.2. node trees](./1-2-node-trees) - Definitions related to node trees:
  paths, traversal, sequences of (nodes, paths, tags, tokens).
* [1.3. hierarchies](./1-3-hierarchies) - Hierarchies of sets/sequences
  and their meaning with regards to node trees.
* [1.4. computing](./1-4-computing) - Aspects related to computer science:
  (currently in its infant stages).

[2. core design](./2-0-core-design) - The designs default definitions:
a tree's node sequence, sectioning nodes, parent containers, ...

* [2.1. extensions](./2-1-extensions) - The definition of extensions to the
  default design: close modifiers (rank values), a role-based perspective
  (sectioning-node, end-marker-node), ...
* [2.2. implementation](./2-2-implementation) - A discussion of critical,
  implementation-specific aspects.

**Note (to self)** -
Each folder should contain a "readme" file.

<!-- ======================================================================= -->
## Notes

**Note** -
Most links (if not all) in this repository reference pages on
[en.wikipedia.org](https://en.wikipedia.org/).
The main intention behind these links is to provide pointers to further
reading material, which is literally available to anyone on this planet.

**Note** -
I write in pure text form. This means that I currently do not pay much attention
to what it will look like, if the contents are displayed (e.g. inside of a web
browser). If documents are difficult, if not impossible to read, then try the
source view.

**Note** -
The whole issue is quite abstract. It is anything but easy to wrap my head
around certain aspects and derive even the simplest of conclusions without
introducing a conflict. Because of that, my focus is on the overall content,
rather than on flawless notation.

**Note** -
I can not guarantee that I did not make any mistake. All I can do is to try to
be as thorough as I can. If you spot a conceptual problem, then (by all means)
please point it out.

**Note** -
I use **CLARIFICATION** markers to mark important statements. These statements
can be clarifications and even definitions. That is, once the time has come,
these kind of markers will have to be edited to properly reflect what kind of
statement the corresponding sections contain. Until then, they should be read
as "something important" and understood to only support visual navigation from
one important statement to another.

**Note** -
In the end, I will most probably have to rename this repository in order to
make place for a proof-of-concept implementation: "node-tree-outliner" may,
at some point in the future, be used to hold such an implementation and
"note-tree-outliner-design", or something similar, will hold the future
version of this design description. If that happens, links will be added that
point to the new location.

<!-- ======================================================================= -->
## PRELIMINARY LICENSE

§1 Free for science and discussions.

* Including free open-source proof-of-concept implementations.

§2 Non-free (i.e. unlicensed) for anything else.

* Including commercial purposes of any sorts.
* Including software patents, trademarks, etc.

§3 General goals

The ultimate goal is to end up with a royalty-free, free-for-all design.
Any use that is in conflict with this general goal is prohibited.

The reason for this restricted preliminary license is to have a clear,
in itself consistent design, that does not have any conflict whatsoever.
This to prevent widespread use of an "unfinished" design.
