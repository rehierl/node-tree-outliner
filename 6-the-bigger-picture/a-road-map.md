
# A road map

The whole issue we are facing is complex - for the most part because many
people with different needs are involved. Literally everybody who comes in
contact with "headings" is, one way or another, affected.

To make things even worse, we need to find an answer for a "thing" that is
already in widespread use. We can not simply flesh out "a new thing", proof
that it works, and be done with it. It isn't that simple.

There already is a huge amount of content out there. By far too much for a
single human being to screen though it all. And even if you attempted to give
it a go, each and every second old content gets removed and new content is
added to that pile of content. In some ways, that "thing" we are dealing with
is alive - it never stops to change, not even for a second. It is like trying
to shake hands with every other human being on this planet ... a futile attempt.

And here is where a neglected participant comes into play: Computers. We need
them to help us deal with the huge amoung of content we have because they are
incredibly fast. The catch with that however is: First we need to teach them
how we humans use "headings" to organize our content. And that is where it
starts to get tricky: Computers are, at least for the time being, dumb by
nature. The only language they understand is ... mathematics.

So no matter how hard you might want to try to find a solution,
no matter how good your intentions might be, there is no easy way out.

## Ironically, the core problem isn't even that complex.

Since the very moment people chose to use the mathematical concept of a node
tree to store and transmit documents, they no longer are what they used to be.
Ever since, there is a discrepancy between what documents are and what we think
they are. For whatever reason, the perception of what we think they are didn't
change with that transition ... And here we are, still trying to catch up.

For the most part, we are used to seeing a document as a single "flat thing"
where we should be seeing a "hierarchy of many things". Simply because a node
tree is on its own a structure of "many things".

A parent node may contain any number of child nodes. And, as a flat list of
nodes, these child nodes represent a "flat thing". In essence, each parent
node represents a "flat thing" that exists because of its child nodes.

But, and that is at the very center of it all, each child node may itself be
a parent node. As such, each child node represents its very own "flat thing"
that is embedded into the "flat thing" of the child's parent node.

As abstract as it may be, that is what could provide us with a good solution:
A node tree reflects a core design paradigm which is used extensively in
computer science: "Divide and conquer" (take a large problem, break it apart
into similar smaller problems, and solve each one of them separately).

## And here is where it starts to get tricky.

**TODO**

We need to figure out how the node tree of a document can be used to teach
computers the meaning of "headings" and what they stand for.

What we need to do is to literally reinvent the wheel.

Backtrack to HTML-4 and from that point on, meticulously figure out how exactly
HTML changed when we started to use node trees. But, before you begin, (and
that is the most difficult thing to truly do for any expert) forget whatever
you think you know and act as if you had to start from scratch.

## The self-inflicted trust issue.

Even if you find a way to scientifically proof, beyond any shred of doubt,
each and every single step from start to finish, a trust issue will still
remain.

Trust takes years to build, seconds to break, and forever to fix.

After all, many years have already passed without any substantial improvement.

So, why is anyone supposed to believe that what you end up with, is what it
needs to be?

**DONE**

## We need a separate, officially maintained specification.

No matter how good your intentions might be, if the design turns out to have
the slightest issue, then no one will support it. Even worse, and even if you
could end up solving all of the design's remaining issues and thus end up with
*the perfect design*, it would be almost impossible to recover from a slight
unintentional mishap ... yes, the trust issue again.

The next design therefore needs to be accompanied by explanations that describe
in great detail why the design is what it needs to be. Those explanations will
then provide the necessary information which people need to understand, based on
which data specific decisions were made in order to deal with certain problems.
That seems to be the only way to build up trust that can withstand some amount
of friction.

In addition to that, these explanations will help to decide in the future,
which changes and/or additions can be made, and which will have to be rejected.

## We need officially maintained reference implementations.

The next design must have an open source, free to use, well documented
proof-of-concept reference implementation. One that allows to experiment
with and see that, what is to become the next design, fulfills its promise.

And because there are many people affected which all have different needs,
dedicated implementations will help even more to prove that the next design
can be implemented with regards to different use cases.

Without these implementations, it will remain difficult to convince anyone
to adopt. After all, if you can't implement your own design, then why should
anyone adopt, or even fix a single "issue" in an existing implementation?

## There won't be any change without an "opt-in".

And even if we could somehow manage to end up with *a perfect design*, there
still is the issue of how we can drag us out of the mess we are in. It will
certainly help to have a design everyone can agree with. But, there is no
switch we can simply flip to make the whole issue disappear.

For quite some time, authors will continue to misuse those elements that are
critical to the design. They need to be informed and they need to learn how to
use them properly. The same goes with developers (of content management systems,
search engines, browsers, etc.) - All of this will take a lot of time and a lot
of convincing effort.

Unfortunately, and even if everybody could be reached, not even that will turn
out to be sufficient. There always are those who simply can not, or don't even
want to be convinced because the mess we are in does seem to work ... somehow.
There simply is no way to force everyone to adopt short of invalidating the
products (content, implementations, etc.) those people produce. For obvious
reasons, that is a no-go.

**TODO**
