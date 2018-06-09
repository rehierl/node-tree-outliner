
# A road map

The issue we are facing is complex - for the most part because many people
with different needs are involved. Literally everybody who comes in contact
with "headings" is, one way or another, affected.

To make things even worse, we need to find an answer for a "thing" that is in
widespread use. We can not simply flesh out "a new thing", proof that it works,
and be done with it. It isn't that simple.

The world wide web can be understood to represent an enormous amount of content.
By far too much content for a single human being to screen through it all. And
even if you would attempt to give it a go, each and every second content gets
removed and new content is added. In some ways, that "thing" we are dealing
with is alive - it never stops to change, not even for a second. It is like
trying to shake hands with every other human being on this planet ... a futile
attempt.

And here is where a largely ignored participant comes into play: Computers.
We need them to help us deal with the tremendous amount of content we have.
However, in order to make better use of computers, we first need to figure
out how we humans organize our content and then what we have to do in order
to teach them what we have learned.

And here is where it gets tricky: For the time being, the only language
computers understand is ... mathematics. And because mathematics is what it is,
it will not change to make it easy for us. All we can do is to formalize the
methods we use to organize our content and try to translate those methods into
a model which computers can process.

It goes without saying that this step, will require changes. Which is because
we developed our methods "the natural way" without formalizing them from the
start. There is no guarantee that we will be able to translate all of our
methods into one consistent model because the different methods we use could
turn out to be in conflict with each other.

And that will be the biggest challenge: Mathematics does not allow any
contradictions. If a model turns out to have conflicts which can not be
resolved (i.e. the model is inconsistent), then that model has no value.

## A design will have to build upon node trees as a formal basis.

Since the very moment people chose to use the mathematical concept of node trees
to store and transmit content, our documents no longer are what they used to be.
Ever since, there is a discrepancy between what documents are and what we think
they are. For whatever reason, the perception of what we think they are did not
completely change with that transition ... And here we are, still trying to
catch up.

For the most part, we are used to seeing a document as a single "flat thing"
where we should be seeing a "hierarchy of many things". That is because a node
tree is by its very own definition a structure of "many things":

A parent node may contain any number of child nodes. And, as a flat list of
nodes, the combination of these child nodes represents a "thing". In essence,
each parent node represents a "thing" that exists because of its child nodes.
But, and that is at the very center of it all, each child node may itself be
a parent node, which is why each child node may represent its own "thing" that
is embedded into the "thing" of its parent node.

Note that a node tree reflects a core design paradigm which is used extensively
in computer science: "Divide and conquer" (take a large problem, break it apart
into similar smaller problems, and solve each one of them separately).

As abstract as it might seem, that is what will allow us to find a solution
because node trees are a construct of graph theory and graph theory is a
discipline of mathematics. In other words, we already have a basis which
computers understand and which we can build upon to transform our methods
into a model.

Furthermore, graph theory comes with a set of tools which we can use to see
whether the model we end up with is in conflict with the underlying node tree.
That is, these tools will allow us to prove that the final model is consistent.

The question that a design therefore needs to answer is:
How do we get our methods to work with a document's node tree?

## We need a separate, officially maintained specification.

No matter how good your intentions might be, if the new design turns out to
have the slightest issue, then no one will support it. Even worse, and even if
you could end up solving all of the remaining issues and thus end up with *the
perfect design*, it could turn out to be almost impossible to recover from an
unintentional mishap.

The next design therefore needs to be accompanied by detailed explanations
which describe why the design is what it needs to be. That seems to be the only
method available to build up trust which can withstand some amount of friction.

In addition to that, these explanations will help to decide which future 
changes and/or additions can be made, and which will have to be rejected.

## We need officially maintained reference implementations.

The next design must have an open source, free to use, well documented
proof-of-concept reference implementation. One that allows to experiment
with and see that, what is to become the next design, fulfills its promise.

And because many people are affected which all have different needs, dedicated
implementations are needed in order to prove that the design can be implemented
with regards to different use cases.

Without these implementations, it will remain difficult to convince people
to adopt. After all, if you can't implement your own design, then why should
anyone adopt, or even fix a single "issue" in an existing implementation?

## There won't be any change without an opt-in flag.

(Assumed that an implementation could even support conflicting semantics by
dynamically switching between different modes of operation ... Even if, the
results will still have to be combined/merged at some point.)

And even if we could somehow manage to end up with *a perfect design*, there
still is the issue of how we intend to resolve the situation we are in. It will
certainly help to have a design everyone can agree with and proof-of-concept
implementations that do indeed work. Unfortunately, there is no switch we can
flip to make the whole issue simply disappear.

For quite some time, authors will continue to look at elements, which are
critical to the design, how they are used to. That is, users have a certain
perception of what the semantics of those elements are. And because the current
element definitions lack clarity, different people look at the same elements
from different perspectives.

In addition to that, the options available to define new elements which (e.g.)
can be used as headings are limited. The definition of new elements, that match
the semantics which the design will need, is not feasible. The new design will
have to reuse existing elements and therefore won't be able to read those as
they are currently perceived. That is, the semantics of existing elements will
have to change.

Users therefore need to be informed and they need to learn how to use these
elements according to the new design. The same goes with developers (of content
management systems, search engines, browsers, etc.) - All of that will take
time and a lot of convincing effort.

Unfortunately, and even if everybody could be informed, not even that will turn
out to be sufficient. There always are those who simply can not, or don't even
want to be convinced, because what we currently have does seem to work ...
somehow. There is no way to force anyone to adopt short of invalidating the
products (content, implementations, etc.) these people produce. For obvious
reasons, that must be avoided if at all possible.

As a matter of consequence, there does not seem to be any other way than to
give users the means to tell implementations, that elements within a given
context, need to be understood a certain way. Users will have to choose the
appropriate set of semantics and store a message alongside with their content.
That message will then allow implementations to detect how to deal with the
corresponding elements.

As a straightforward method, such a message could be represented by a simple
policy or version flag within the document's global scope. And because a common
practice is to inject content from some source into another context, such a
flag will also have to be supported on a local, sub-document level. That is,
the global scope needs to be understood to set a document's default policy and
the local scope as a context dependent policy override.

Obviously, such a flag did not exist in the past, which is why a missing flag
needs to be understood as a message that states "Read the content as if we are
still in the pre-flag era". And because of that, users will have to explicitly
use such a flag in order to opt-in to the new semantics for at least until
those semantics are used by a significant majority.
