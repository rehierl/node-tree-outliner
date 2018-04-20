
<!-- ======================================================================= -->
# node-tree-outliner

The purpose of this repository is to flesh out a design that can be used to
implement a general-purpose outliner for any rooted ordered tree of nodes.

This repository is **in a state of flux**.
It may and will change considerably without further notice
(Direct links to files within this repository may break at any time).

<!-- ======================================================================= -->
## Overview

* [0-introduction](./0-introduction): A general introduction.
* [1-basics](./1-basics): A recap of mathematical definitions.
  (Skim it to get an impression of the contents and the style of notation)
* [2-tree-of-nodes](./2-tree-of-nodes): A recap of the formal definition of
  node trees. In addition to that, the definition of important sequences.
  (Skim it to get an impression of the contents)
* [3-basic-design](./3-basic-design): The designs default definitions:
  a tree's node sequence, sectioning nodes, parent containers, ...
* [4-extensions](./4-extensions): The definition of extensions to the
  default definitions: close modifiers (such as rank values), a role-based
  perspective (sectioning-node, end-marker-node), ...
* [5-implementation](./5-implementation): A discussion of how to implement
  certain critical aspects.
* [6-the-bigger-picture](./6-the-bigger-picture): General thoughts targeted
  at explaining the bigger picture.

**Note** (to self) -
Each folder should contain a "readme" file.

<!-- ======================================================================= -->
## Notes

**Note** -
I can not guarantee that I didn't make an error. All I can do is to try to be a
thorough as I can. So I need to ask this: If you spot a conceptual problem, then
(by all means) please point it out.

**Note** -
The whole issue is quite abstract. It is anything but easy to wrap my head
around certain aspects and derive even the simplest of conclusions without
introducing a conflict. Until I have reached a state that I can call "stable",
I will have to respectfully decline any offer for full-blown cooperation.

**Note** -
I write in pure text form. This means that I don't pay much attention to
what it will look like, if the contents are displayed inside of a browser.
If documents are hard, if not impossible to read in a browser, then try
the source view.

**Note** -
I will most probably have to rename this repository in order to make place for
a proof-of-concept implementation: "node-tree-outliner" may, at some point in
the future, be used to hold a such an implementation and "note-tree-outliner-design",
or something similar, will hold the future version of this design description.

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
