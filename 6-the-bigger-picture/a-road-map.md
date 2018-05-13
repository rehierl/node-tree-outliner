
# A road map

The issue we are facing is complex - for the most part because many people
with different needs are involved. Literally everybody who comes in contact
with "headings" is, one way or another, affected.

To make things even worse, we need to find an answer for a "thing" which is
in widespread use. We can not simply flesh out "a new thing", proof that it
works, and be done with it. It just isn't that simple.

The world wide web can be understood to represent an enormous amount of content.
By far too much for a single human being to screen through it all. And even if
you would attempt to give it a go, each and every second content gets removed
and new content is added. In some ways, that "thing" we are dealing with is
alive - it never stops to change, not even for a second. It is like trying to
shake hands with every other human being on this planet ... a futile attempt.

And here is where a largely ignored participant comes into play: Computers. We
need them to help us deal with the tremendous amount of content we have. But,
before we can make use of their speed, we first need to figure out how we humans
organize our content and then what we have to do in order to teach computers
what we have learned. And here is where it gets tricky: Computers are, at least
for the time being, dumb by nature. The only language they understand is ...
mathematics.

And because mathematics is what it is, it will not change to make it easy for
us. All we can do is formalize the methods we use to organize our content and
try to translate those methods into a model which computers can understand. It
goes without saying that this step, will require changes. Which is because we
developed our methods "the natural way" without formalizing them up front. That
is, there is no guarantee that we will be able to translate all of our methods
into a formal model.

And, to make things even worse, the different methods we use which could even
be translated, might turn out to be in conflict with each other. This will be
the biggest challenge: Mathematics does not allow any conflict. If a model turns
out to have even one conflict that can not be resolved (i.e. is inconsistent),
then that model has no value.

So no matter how hard you might want to try to find a solution,
no matter how good your intentions might be, there is no easy way out.

## Ironically, we are already half way there.

Since the very moment people chose to use the concept of a node tree to store
and transmit content, our documents no longer are what they used to be. Ever
since, there is a discrepancy between what documents are and what we think they
are. For whatever reason, the perception of what we think they are didn't change
with that transition ... And here we are, still trying to catch up.

For the most part, we are used to seeing a document as a single "flat thing"
where we should be seeing a "hierarchy of many things" because a node tree is
on its own a structure of "many things":

A parent node may contain any number of child nodes. And, as a flat list of
nodes, these child nodes represent a "flat thing". In essence, each parent node
represents a "flat thing" that exists because of its child nodes. But, and that
is at the very center of it all, each child node may itself be a parent node,
which is why each child node may represent its own "flat thing" that is embedded
into the "flat thing" of it's parent node.

As abstract as that might seem, that is what will allow us to find a solution
because node trees are a construct of graph theory and graph theory is a
discipline of mathematics. In other words, we already have a basic model which
computers understand and which we can build upon to formalize our methods.

Furthermore, graph theory comes with a set of tools which we can use to prove
if the model we end up with has conflicts or not.

Note that a node tree reflects a core design paradigm which is used extensively
in computer science: "Divide and conquer" (take a large problem, break it apart
into similar smaller problems, and solve each one of them separately).

## And here is where it starts to get tricky.
**TODO**

What needs to be done first is to figure out how the methods we use to organize
content can be used in combination with the underlying node trees.

## The self-inflicted trust issue.
**TODO**

Even if you find a way to scientifically proof, beyond any shred of doubt,
each and every single step from start to finish, a trust issue will still
remain.

Trust takes years to build, seconds to break, and forever to fix.

After all, many years have already passed without any substantial improvement.

So, why is anyone supposed to believe that what you end up with, is what it
needs to be?

## We need a separate, officially maintained specification.

No matter how good your intentions might be, if the design turns out to have
the slightest issue, then no one will support it. Even worse, and even if you
could end up solving all of the remaining issues and thus end up with *the
perfect design*, it could turn out to be almost impossible to recover from
a minor unintentional mishap ... yes, the trust issue again.

The next design therefore needs to be accompanied by explanations that describe
in great detail why the design is what it needs to be. Those explanations will
then provide the necessary information which people need to understand, based
on which data certain decisions were made in order to deal with specific aspects.
That seems to be the only way to build up trust that can withstand some amount
of friction.

In addition to that, these explanations will help in the future, to decide
which changes and/or additions can be made, and which will have to be rejected.

## We need officially maintained reference implementations.

The next design must have an open source, free to use, well documented
proof-of-concept reference implementation. One that allows to experiment
with and see that, what is to become the next design, fulfills its promise.

And because there are many people affected which all have different needs,
dedicated implementations are needed in order to prove that the next design
can be implemented with regards to different use cases.

Without these implementations, it will remain difficult to convince anyone
to adopt. After all, if you can't implement your own design, then why should
anyone adopt, or even fix a single "issue" in an existing implementation?

## There won't be any change without an opt-in flag.

And even if we could somehow manage to end up with *a perfect design*, there
still is the issue of how we can drag us out of the mess we are in. It will
certainly help to have a design everyone can agree with and implementations
which prove that it does indeed work. But, there is no switch we can flip to
make the whole issue simply disappear.

For quite some time, authors will continue to look at elements, which are
critical to the design, how they are used to. That is, users have a certain
perception of what the semantics of those elements are. To make things worse,
and because the current element definitions lack clarity, different people
look at the same elements from different perspectives.

In addition to that, the options available to define new elements which (e.g.)
can be used as headings are limited. The definition of new elements that match
the semantics which the design will need is not feasible. The new design will
therefore not be able to read existing elements as they are perceived.

Again, mathematics is what it is, it won't change. If we want to make computers
help us with the huge amounts of content we have, then we are the ones who will
have to change.

Users therefore need to be informed and they need to learn how to use those
elements according to the design. The same goes with developers (of content
management systems, search engines, browsers, etc.) - All of that will take
time and a lot of convincing effort. Unfortunately, and even if everybody could
be informed, not even that will turn out to be sufficient. There always are
those who simply can not, or don't even want to be convinced because the mess
we are in does seem to work ... somehow. There is no way to force everyone to
adopt short of invalidating the products (content, implementations, etc.) those
people produce. For obvious reasons, that is not an option.

Hence, there does not seem to be any other way than to give users the means
to tell an implementation, that elements within a given context, need to be
understood a certain way. Users will have to choose the appropriate set of
semantics and store a message with their content. That message will then
allow an implementation to detect how to properly read the elements.

As a straightforward method, such a message could be represented by a simple
policy or version flag within the document's global scope. And because a common
practice is to inject content from some source into another context, such a
flag will also have to be supported on a local, sub-document level. That is,
the global scope needs to be understood to set a document's default policy and
the local scope as a policy override. Obviously, such a flag did not exist in
the past, which is why a missing flag needs to be understood as a message that
states "Read the content as if we were still in the pre-flag era".

That is, users will have to use such flags in order to opt-in to the new
semantics for at least until those semantics are used by a overwhelming
majority.
