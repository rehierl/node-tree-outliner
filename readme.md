
<!-- ======================================================================= -->
# node-tree-outliner

The purpose of this repository is to flesh out a design that can be used to
implement a general-purpose outline algorithm for any rooted ordered tree of
nodes.

This repository is **in a state of flux**.
It may and will change considerably without further notice.
(Direct links to files within this repository may break at any time).

<!-- ======================================================================= -->
## Overview

* [introduction](./0-introduction): A general introduction.
* [basics](./1-basics): A recap of basic mathematical definitions.
  (Skim it to get an impression of its contents and my style of notation).
* [node-trees](./2-0-node-trees): A recap of the formal definition of
  node trees. In addition to that, the definition of important sequences.
  (Skim it to get an impression of its contents).
* [hierarchies](./2-1-hierarchies): About the equivalency between node trees
  and hierarchies of sets and sequences.
* [basic-design](./3-basic-design): The designs default definitions:
  a tree's node sequence, sectioning nodes, parent containers, ...
* [extensions](./4-extensions): The definition of extensions to the
  default definitions: close modifiers (such as rank values), a role-based
  perspective (sectioning-node, end-marker-node), ...
* [implementation](./5-implementation): A discussion of how to implement
  certain critical aspects.
* [bigger-picture](./6-bigger-picture): My thoughts on the bigger picture.

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
