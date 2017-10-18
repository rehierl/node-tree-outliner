
# Notes

<!-- ======================================================================= -->
## Open/Closed Sections

A section is considered open, if it is still allowed to associate entities
(nodes, a heading and subsections) with it. A section is closed (has ended),
if that is no longer allowed.

Similar to binary streams, certain resources (e.g. memory) will be associated
with a section. These must be allocated (locked) when a section is opened and
released (freed, unlocked) when it is closed.

Once created, a new section object is automatically opened for associations.
As this step will allocate resources, there needs to be a point for each section
at which a section's resources can be released.

Ultimately, that point is reached for any section when tree traversal ends. But,
at that point, certain sections might no longer be accessible. In such a case,
resources allocated for sections that are no longer accessible will remain
locked (e.g. memory leaks).

<!-- ======================================================================= -->
## The current/active section - TODO

* At any given time, multiple sections may be open.
* Only one open section is considered to be the current/active section.

<!-- ======================================================================= -->
## Implied headings

During tree traversal, the following states can be observed:

0. A section object is created and automatically opened for associations
   (i.e. `(section.heading == null)` is true).
1. A section is still open, but no heading was associated with it
   (i.e. `(section.heading == null)` is still true).
2. The first heading element within an open section was entered and associated
   with that section (i.e. `(section.heading != null)` is true - step F.1.1).
3. A section has ended and *a heading* element was associated with it
   (i.e. `(section.heading != null)` remains to be true).
4. A section has ended and *no heading* element was associated with it
   (i.e. `(section.heading == null)` remains to be true).

From these states, the following statements can be derived:

1. The expression `(section.heading == null)` is true for sections that
   have *no heading* and that are either *open or closed*.
2. The expression `(section.heading != null)` is true for sections that
   have *a heading* and that are either *open or closed*.

Note that both expressions are ambiguous with regards to a section's
is-open-or-closed state.

Obviously, it would be preferable to have a dedicated is-open-or-closed state
property for each section. But, such a property would only have a use for as
long as tree traversal has not finished. Once tree traversal is done, all
sections are closed and such a property would hold the exact same value for any
section (i.e. such a state property would be wasting memory).

The current algorithm will therefore associate a non-null pseudo heading
(aka. implied heading) with a section that has ended and that has no heading.
This allows to make the following statements:

1. The expression `(section.heading == null)` is true for sections that
   have *no heading* and that are *still open*.
2. The expression `(section.heading != null)` is true for sections that
   have *a heading* (implied or not) and that are either *open or closed*.

Therefore, if expression (1) (i.e. `section.hasNoHeading()`) evaluates to true,
a heading can still be associated with the corresponding section because that
section is still open. -- This is at least the intention behind implied headings.

Obviously, it would be an error to associate an implied heading with an open
section that has no heading (because a heading element could still follow). As
a result, the expression `section.setImpliedHeading()` implicitly states, that
the corresponding section has no heading *and* that it has ended.

Overwriting an implied heading would also be an error, because this would
represent an attempt to continue a section that has already ended. Once a
section ends, any resources associated with it can be released. After that,
those resources can no longer be accessed because any such attempt would
inevitably trigger an access violation error.

**TODO** - Each heading element has a rank.
Is it necessary to associate a rank (highest or lowest) with an implied heading?
Does the algorithm implicitly associate a rank with an implied heading?
