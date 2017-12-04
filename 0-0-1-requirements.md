
<!-- ======================================================================= -->
# General goals and requirements

The most fundamental goal of an outline algorithm is to allow the generation
of an accurate listing of sections (aka. table of contents, TOC) that can be
found within a given node tree. As such, a TOC provides a static overview of
the tree's contents.

However, the more sections there are, the less helpful such a listing becomes.
A design must therefore allow to support dynamic behavior.

*dynamic support*

A design must allow to change the display of a TOC based on actions
executed on the display of a tree (i.e. tree -> toc):

* Allow to determine the context of any given node in order to display and
  update the display of the current location (e.g. bread crumbs).
* Allow to dynamically change the TOC of a tree based upon any given node.
  It must be possible to show/unfold those parts of a tree that are within
  a given context and to hide/fold parts that are outside of it.

A design must allow to change the display of a tree based on actions
executed on the display of a TOC (i.e. toc -> tree):

* Allow to focus on a section depending on which TOC entry was selected.
* Allow to dynamically change the display of a tree depending on which TOC
  entry was selected. It must be possible to show/unfold those parts of a
  TOC that are within the current context and to hide/fold parts that are
  outside of it.

A design must allow to manually change the display of a tree depending
on actions executed on the display itself (i.e. tree -> tree):

* Allow to show/unfold and to hide/fold a section, if the corresponding
  event was triggered on a section's representative.

In order to support these dynamic goals, certain requirements must be met:

* Any node within a tree must effectively belong to exactly one section.
  This is needed to uniquely determine the context of any node.
* It must be possible to determine the location of a section, even if that
  section turns out to be empty. This is needed to focus on any given section.
* It must be possible to treat any section as a single entity.
  This is needed to fold/unfold whole sections via a single operations.

*efficient implementation*

In addition to the above dynamic goals, it must be possible to efficiently
implement a TOC generator. Such an implementation represents a reduced/limited
version of an outline algorithm that has one purpose only:
To efficiently generate a TOC for any tree.

The first step of a fully functional outline algorithm is to read the contents
of a tree and to create a structure of sections that accurately represents the
tree's contents. After that, this structure can be used to generate a TOC. As
such, the generation of a TOC is, in general, a two-step process that has a
fully functional temporary result (i.e. the structure of sections).

If a TOC generator would have to be implemented in terms of such a two-step
process, it would end up having to generate and then keep more information in
memory than it actually needs. Because of that, a design must allow to extract
the required information and then drop a section object as soon as it is fully
specified. That is, unless this section has no effect on another section.

This essentially means, that a design must allow to create a TOC on the fly.
