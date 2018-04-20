
# The bigger picture

* There is no easy way out.

Now, where do I start? I guess, at the very end (seems as good a starting point
as any): The whole problem we are facing is tremendously complex - simply
because so many people are involved. Literally everybody who uses or has to rely
on heading elements is affected. So, no matter how hard you might want to try,
no matter how good your intentions might be, there simply is no easy way out.

And even if you might find a way to scientifically proof, beyond any shred of
doubt, each and every single step from start to finish, a trust issue will still
remain. After all, many years have already passed without any real change.

* We need an officially maintained specification.

**TODO**

* We need an officially maintained reference implementation.

The next design must therefore have an open source, completely free to use,
extensively documented implementation. One that allows to experiment with it
and see that, what is to become the next design, truly does what it is supposed
to do (Obviously, this also applies to any possible future change). And because
of that, the next design must be accompanied by an officially maintained
proof-of-concept reference implementation.

Without such an implementation, you will always have difficulties trying to
convince anyone to adopt it. No matter how good your intentions might be, if
the design turns out to have even the slightest issues, then why should anyone
adopt or even fix a single error in an existing implementation?

* Ironically, the core problem isn't that complex, it can be solved.

Since the very moment people chose to use the mathematical concept of a node
tree to convey a HTML document, HTML itself is no longer what it used to be.
Ever since, there is a discrepancy between what HTML truly is and what we think
it is. For whatever reason, the perception of what we think it is didn't change
with that transition. And we are still trying to catch up.

For the most part, we are used to seeing a HTML document as a single "flat
something" where we should actually be seeing a single "hierarchy of many
things" simply because a node tree is a structure which holds many "flat
things": A parent node may contain any number of child nodes. And as a flat
list of nodes, these child nodes represent a "flat thing". In essence, each
parent node represents a "flat thing" that exists because of its child nodes.

But, and that is at the very center of it all, each child node may itself be
a parent node. And as such, each child node may represent its very own "flat
thing", which happens to be embedded into the "flat thing" of its parent node.

Because of that, a node tree reflects a core design paradigm used extensively
in computer science: "Divide and conquer" (take a large problem, break it apart
into similar smaller problems, and solve each one of them separately).

* What we need to do is this: We need to reinvent the wheel.

Backtrack to HTML-4 and from that point on, meticulously figure out how exactly
HTML changed when we started to use node trees. But, before you begin, (and
that is the most difficult thing to truly do for any expert) forget whatever
you think you know and act as if you had to start from scratch:

* "There is no spoon." (The Matrix 1999)

(Don't get it wrong: I'm the "Spoon boy", you are "Neo".)
