
<!-- ======================================================================= -->
# Category Theory

* (x) is used as the composition operator

<!-- ======================================================================= -->
## wikipedia, category theory

* category - structures in terms of labeled directed graphs
* vertices represent objects and the arrows between them morphisms
* category theory - also used as an axiomatic foundation for mathematics
* the arrows can be composed associatively
* the identity arrow exists

basic concept

* a category represents other mathematical concepts
* arrows - visualize that one object can be processed/transformed into another
* category theory allows to proof results based on simpler objects

functor

* functors transform one category into another
* i.e. a category of categories in which morphisms are functors
* i.e. study the relationships between classes of structures
* natural transformation - map one functor to another

categories, objects, morphisms

* a class is a collection of sets
* obj(C) - a class whose elements are objects
* hom(C) - a class whose elements are morphisms

morphisms

* (f: a -> b), (ab: a -> b), (ba: b -> a), (ca: c -> a), (bc: b -> c)
* 1x - identity in x - i.e. yields the same x
* mono-morphism - (f x ca1 = f x ca2) => (ca1 = ca2)
* epi-morphism - (bc1 x f = bc2 x f) => (bc1 = bc2)
* bi-morphism - a morphism that is a mono- and epi-morphism
* iso-morphism - a ba exists such that (f x ba = 1b) and (ba x f = 1a)
* endo-morphism - (f: a -> a)
* auto-morphism - morphism that is a endo- and iso-morphism
* retraction - a ba exists such that (f x ba = 1b) - right inverse
* section - a ba exists such that (ba x f = 1a) - left inverse

clarification

* every retraction is an epi-morphism
* every section a mono-morphism
* isomorphism <=> (mono- and retraction) <=> (epi- and section)

higher-dimensional categories

* process/transform objects into other objects
* generalize such a process by considering "higher-dimensional processes"
* e.g. 2-category - a category together with morphisms between morphisms
