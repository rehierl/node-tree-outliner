
<!-- ======================================================================= -->
# The h1-h3 issue

With regards to stevefaulkner's and bkardell's question, and with regards to
annevk's proposal: It would effectively build in a pattern that would create
something we historically advise authors not to write manually.

* [stevefaulnker's comment](https://github.com/whatwg/html/issues/83#issuecomment-360977496)
* [bkardell's comment](https://github.com/whatwg/html/issues/83#issuecomment-369437548)
* [annevk's comment](https://github.com/whatwg/html/issues/83#issuecomment-359871505)

```
lines    fragment-1      fragment-2          toc-1     toc-2
=====    ==========      ==========          =====     =====
1:       <h1> A </h1>    <h1> A </h1>        1. A      1. A
2:       <h3> C </h3>    <section>           1.1. C    1.1. B/Untitled
3:                         <!-- h2:B -->               1.1.1. C
4:                         <section>
5:                           <h3> C </h3>
6:                         </section>
7:                       </section>
```

The above mentioned advice can be summarized into: Don't use "h1-h3", instead
use "h1-h2-h3". It essentially assumes that the table-of-contents listing of
fragment-2 needs to be toc-1, but without answering the question whether toc-1
best represents the fragment's structure.

So, which listing best represents the above fragments? Do they have the same
listing, or are both listings different? If, out of some initial reaction,
you chose a listing, then is that listing accurate, or some generally accepted
approximation that was chosen based on some common practice (e.g. "reality")?

If only for a moment, visit the lower levels: Assume that some highly efficient
web-crawler (short: WC - will be used as a name) would be in the process of
indexing a document and that, at some point, it encounters one of the above
fragments.

Note that the following content needs to be understood with regards to a concept
of "sections". Also note that annevk's proposal completely drops this very
concept.

<!-- ======================================================================= -->
## How an implementation sees fragment-1

```
lines    fragment-1      toc-1     toc-2
=====    ==========      =====     =====
1:       <h1> A </h1>    1. A      1. A
2:       <h3> C </h3>    1.1. C    1.1. B/Untitled
3:                                 1.1.1. C
```

### Line 1:

No issue here: The `h1` element instructs to create an object which needs to
be understood to represent a top-level section. In addition to that, the
section object has a title property with text content "A" and a rank-like
property with a value of 1. Assume that, by now, WC has created the following
object:

```
section: {name:"A", title:"A", rank:1}
```

Note that the "rank" property of a section object does not exist as a "real
thing". These properties act as a visual representation of the section's
outline depth.

### Line 2:

WC then visits the next heading element and notices that it has "C" as title
and a rank value of 3. Also, no issue here: WC simply creates another section
object and initializes its properties:

```
section: {name:"C", title:"C", rank:3}
```

Now, and because WC has to connect both section objects, it grabs "A" and "C",
and compares both rank values with each other. Obviously, there is a problem:
`(A.rank < C.rank-1)` (Note `<` instead of `<=`). That is, the sequence of rank
values is interrupted because WC does not know of any section that has rank 2.

### Option 1: An input error.

If WC would be implemented to be strict, then it would have to take each rank
value as an absolute instruction which it has to execute by the letter. Because
of that, it could not continue to process the current document as it contains
an input error:

WC can not add "C" as subsection to a section that has rank 2. In WC's current
context, such a section does not exist because WC was never instructed to create
it. Likewise, WC can not add "C" as subsection to "A" because both rank values
don't match. That is, the combination of both rank values are non-conformant
under such a pedantic perspective.

And because the sequence of instructions, which the current fragment represents,
has input errors, WC has no other option than to throw an exception. That is, WC
can only cancel to process the current document. As a consequence, no one will
be able to find that document by using WC's search engine.

In essence, and if each web crawler would act the same pedantic way, then most
of the World Wide Web could no longer be found. The World Wide Web as we know
it would cease to exist. Poof, just like that.

### Option 2: Resolve it during runtime.

Obviously, WC has no means to simply contact the document's author because
WC's timescale is in milliseconds (if not in micro- or even nanoseconds).
WC can therefore not wait for any response. And even it could:

WC: "Wait, what do you mean? The author is not responsible? The CMS is?"

That is, WC must itself choose a way to resolve this issue during runtime.

### Option 3: Toc-1, an acceptable approximation.

If WC sees the rank value of 3 as a relative instruction to add "C" as
subsection to the next closest section of higher importance, then all
WC would have to do is add "C" as subsection to "A".

```
section: {name:"A", title:"A", rank:1, subsections:[ C ]}
section: {name:"C", title:"C", rank:2, subsections:[]}
```

Problem solved, the loose/relative way.

Note that, in order to end up with a consistent result, WC also has to change
"C"'s rank value from 3 to 2. Because of the deviation in rank, that solution
is not accurate and only represents a best-effort approximation.

### Option 4: Toc-2, an acceptable approximation.

If WC sees "C"'s rank value of 3 as a strict and absolute instruction to create
a section which does have a rank value of 3, then WC first has to create an
implicit intermediate section with rank 2:

```
section: {name:"B", title:None, rank:2}
```

WC can now add "B" as subsection to "A", and "C" as subsection to "B":

```
section: {name:"A", title:"A", rank:1, subsections:[ B ]}
section: {name:"B", title:None, rank:2, subsections:[ C ]}
section: {name:"C", title:"C", rank:3, subsections:[]}
```

Problem solved, the strict/absolute way.

Note that the result of this option does also not accurately represent the
initial fragment because that fragment does not have an `h2` element. That
is, there is no definition for an intermediate section. Similar as before,
the result of this option only represents a best-effort approximation.

### Option 3 or 4: But which one?

Because fragment-1 holds an input error, WC is not in the position to produce
an accurate result for fragment-1. But, as WC has to choose an option in order
to produce a result, and provided that there is no other option, WC can only
choose between options 3 and 4.

So here is the thing: Can WC freely choose an option? No, it can't, because
both of those will result in different results. Although any result is still
better than no result at all, being able to freely choose an option would be
just as bad: The very same document would end up getting indexed based on
someone's personal preference.

The problem with option 4 is, that section "B" will end up having identical
content as section "C". And because implementations tend to be inefficient if
they need to support such redundancy, this aspect alone represents a reason
not to choose option 4.

Furthermore, option 4 represents a fragment that is in conflict with "any
section always has its own sectioning node". That is, there could not be a
1:1 relationship between the set of sectioning nodes and the set of sections.

Note that this can be understood that the existence of sectioning nodes has
in general precedence over rank values. This should not be too surprising as
rank values can not exist without sectioning nodes because rank values can not
be specified without a corresponding sectioning node.

Note that HTML 3.2, 4.01, 5.0, 5.1 and 5.2 do not define heading content
elements to hold absolute rank values. They always are introduced as relative
values in terms of a "level of importance", or as "higher or lower rank values".
That is, rank values were at no point defined to be absolute, but always as
relative to one another.

Unless there is irrefutable proof that option 3 will yield invalid results if
additional aspects are taken into account, then option 3 is what WC must choose.
That is, because option 4 would result in reinterpreting existing content.

### Summary: fragment-1/toc-1

Obviously, WC needs to produce a result. It can not reject a document just
because it has input errors (i.e. is non-conformant). WC can therefore only
produce a best-effort result. Furthermore, WC can not freely choose which
result it has to return. Different implementations would otherwise end up
producing different results for the same document. That is, there must be
an agreement on what the result of such a fragment has to be.

For historical reasons, and until proven otherwise, toc-1 is what WC must
return in case of fragment-1. The point however is to not forget that
fragment-1 represents an input error and that toc-1 is an inaccurate, but
generally accepted best-effort approximation.

If issues arise with another fragment, then that fragment-1/toc-1 approach can
not be used as basis to choose which result has to be returned. It depends on
which results the other fragment supports. That is, if it supports only one
solution, then that solution is what the result has to be. But if the other
fragment offers multiple different approximations instead of a precise result,
then an agreement is needed on which result to return for that fragment.

<!-- ======================================================================= -->
## How an implementation sees fragment-2

```
lines    fragment-2          toc-1     toc-2
=====    ==========          =====     =====
1:       <h1> A </h1>        1. A      1. A
2:       <section>           1.1. C    1.1. B/Untitled
3:         <!-- h2:B -->               1.1.1. C
4:         <section>
5:           <h3> C </h3>
6:         </section>
7:       </section>
```

### Line 1:

As before, there is no issue here. Which is why WC needs to first create the
following section object:

```
section: {name:"A", title:"A", rank:1}
```

### Line 2:

WC enters the section element and therefore has to next create the following
section object:

```
section: {name:"B", title:None, rank:2}
```

Note that section elements, if no explicit rank value is available, declare
a new subsection to the current section. With regards to fragment-2, that
perspective is not much different to the current official definition of
sectioning content elements.

And because there is no explicit rank value associated with the current section
element, WC can only add "B" as subsection to "A" and set "B"'s rank value to 2:

```
section: {name:"A", title:"A", rank:1, subsections:[ B ]}
section: {name:"B", title:None, rank:2, subsections:[]}
```

### Line 3:

Obviously, comments must not have any effect on semantics,
which is why WC has to skip line 3.

### Line 4:

As before, WC has to create a new section object ...

```
section: {name:"C", title:None, rank:3}
```

... and add it as subsection to "B".

```
section: {name:"A", title:"A", rank:1, subsections:[ B ]}
section: {name:"B", title:None, rank:2, subsections:[ C ]}
section: {name:"C", title:None, rank:3, subsections:[]}
```

### Line 5:

Now, WC has to process heading element `h3`. But, as that element is the very
first element of heading content within "C"'s sectioning node, it is defined to
be re-used to hold the section's title. WC must therefore change "C"'s title to
"C":

```
section: {name:"A", title:"A", rank:1, subsections:[ B ]}
section: {name:"B", title:None, rank:2, subsections:[ C ]}
section: {name:"C", title:"C", rank:3, subsections:[]}
```

Note that, with regards to the official specification, the rank value specified
by the `h3` element may have a section-internal effect: If that section element
had another heading element with rank 1/2/or/3, then WC would, according to the
official specification, have to create a sibling section to "C". But, with
regards to fragment-2, that aspect is a non-issue. Fragment-2 has no such inner
subsequent heading content element.

### Line 6:

In general, any number of operations, which WC would have to execute, may be
associated with the enter and/or exit event of a node. However, and with regards
to the "h1-h3" issue:

WC can be understood to have nothing else to do when exiting "C".

### Line 7:

As before, WC has nothing more to do when exiting "B".

Note that there is no instruction to set or change "B"'s title. The author of
that fragment did not specify a title for "B". WC therefore has no other option
than to leave "B" as is.

### Summary

So the answer with regards to fragment-2 is that toc-2 represents the structure
of its contents. But, in contrary to fragment-1, toc-2 is not an approximation:
toc-2 accurately represents the structure of fragment-2.

You: Hold on a sec, what just happened?
Me: Nothing, fragment-2 is by itself perfectly fine ...
Me: ... There is no issue, none at all.

Sure, it is bad practice to specify a section with no heading - just as it is
bad practice to specify `<hX></hX>` (i.e. a heading with no content), or even
`h1-h3` fragments. But, there is nothing WC can do. Once WC could even realize
that "B" has no title (i.e. when exiting the section element of "B"), it is
already too late: All objects have been created and the section hierarchy is
established. That issue can therefore not be resolved on the abstraction level
of a web crawler.

<!-- ======================================================================= -->
## An overall summary

### The perspective of a low-level implementation.

*fragment-1/toc-1:*
The issue with this fragment is bound to an element that does not properly
fit into the fragment's logical structure. And because of that, a low-level
implementation can (and even has to) resolve the fragment's input error with
a commonly accepted approximation.

*fragment-2/toc-2:*
The "issue" with this fragment is based upon multiple elements that combined,
do not represent an input error. Because of that, an implementation can and
must return the only solution possible. As bad-practice as it may be, toc-2
accurately represents the fragment's structure.

### With regards to "building in a pattern we advise not to use".

The difference is that with fragment-1, a low-level implementation can and must
resolve the author's input error with an approximation. After all, it is better
to return some result rather than no result at all. In contrary to that, and
with regards to fragment-2, a low-level implementation has no other choice but
to return an accurate result.

No, the response does not promote a pattern we advise not to use. It reflects
the author's fragment/document (i.e. the algorithm's input) as is.

Note that this does not mean that the lack of a heading will be promoted as
good practice. A low-level implementation is simply not in the position to do
anything about that "issue".

Yes, a section without a "heading" can and should still be declared as being
bad practice.

### Any other "result" will add complexity to low-level implementations.

Again, the above considerations are with regards to the abstraction level of
a low-level, highly optimized web crawler. Any attempt to re-define the (on
a formal level perfectly fine) result of fragment-2 by specification, will
needlessly add complexity to low-level implementations.

A low-level implementation would for example have to include heuristics, which
it would have to apply as an additional post-section, or post-process operation.
That is, because there is an infinite number of combinations of sections with
content and "seemingly empty" sections possible.

The "issue" with fragment-2 can therefore only be resolved on a higher level
of abstraction; e.g. via the means of "best practices" guidelines targeted at
authors, and/or transformation rules addressed at implementors of user agents.

### Questions that would have to be clearly answered:

If, on a higher layer of abstraction, seemingly empty sections would have
to be skipped, then there would have to be clear instructions of how an
implementation could decide whether or not a given section would have to
be skipped:

* What is the precise meaning of "empty"? Does whitespace content count towards
  empty or non-empty? (Note that parsers will implicitly generate these kind of
  non-element nodes; e.g. in between the tags of lines 6 and 7 in fragment-2).
  Do comments count? Does a hierarchy that only consists of `<div>` containers
  only count?
* What is supposed to happen in case of whole hierarchies of "empty" sections
  which still have sparse, deeply-nested but still non-empty inner sections?
* Won't the removal of "empty" sections change an intended logical layout?
  (e.g. a structure intended for documentational purposes that gets filled
  with content over time).

In other words: There are many questions that need to be answered, if seemingly
empty sections would have to be left out.

### The big struggle.

One aspect of the whole issue is that information gathering and display must
use the same perspective on a document's logical structure:

Assumed that a search engine knows that the information a user seeks can be
accessed via the in-document as-is logical path-of-sections "A", and assumed
that the path the user could follow via some visual display is the in-document
as-displayed logical path-of-sections "B". Under these kind of circumstances,
the user won't be able to follow path "A", if the only path he can follow is
path "B", and if that path is (e.g. for display reasons) different from path
"A".

All in all, this aspect reflects a core issue: Different levels of abstraction
must have the exact same perspective on a document's logical structure.
