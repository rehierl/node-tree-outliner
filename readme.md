
node-tree-outliner
===============

The purpose of this repository is to flesh out a design that can be used to
implement a general-purpose outliner for any rooted ordered tree of nodes.

Note that this repository is in a state of flux.
It may still change considerably.

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

Note that each folder should have a "readme" file.

## Upload log

* 2018-04-04 - commit 1740f4f - roles: sectioning-node, end-marker-node
* 2018-03-26 - commit c6729ba - overall revisions
* 2018-03-15 - commit 54580c1 - implementation specific aspects
* 2018-03-05 - commit ea0b721 - hierarchy, close modifiers
* 2018-02-19 - commit ef94c42 - current section
* 2018-02-04 - commit 55cc8a7 - clarifications
* 2018-01-31 - commit 19abbd2 - first public upload

## PRELIMINARY LICENSE

§1 Free for science and discussions.

* Including free open-source proof-of-concept implementations.

§2 Non-free (i.e. unlicensed) for anything else.

* Including commercial purposes of any sorts.
* Including software patents, trademarks, etc.

§3 General goals

The ultimate goal is to end up with a royalty-free, free-for-all design.
Any use that is in conflict with this general goal is prohibited.

The reason for this restricted preliminary license is to have a clear, in
itself consistent design, that is not in any conflict with any node tree.
That is, in order to prevent widespread use of an "unfinished" design.
