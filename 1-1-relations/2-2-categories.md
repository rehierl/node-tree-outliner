
<!-- ======================================================================= -->
# Categories

* (x) is used as the composition operator

<!-- ======================================================================= -->
## wikipedia, category of sets (Set)

* has sets as objects and functions as morphisms

<!-- ======================================================================= -->
## wikipedia, category of relations (Rel)

* has sets as objects and binary relations as morphisms
* functional relation - (F subset-of X x Y) - (xFy <=> f(x)=y)

<!-- ======================================================================= -->
## wikipedia, category of preordered sets (Ord)

* has preordered sets as objects and order-preserving functions as morphisms
* the composition of two order-preserving functions is order-preserving
* the empty set is considered to be a preordered set
* Ord is a concrete category

<!-- ======================================================================= -->
## wikipedia, (abstract) category

* aka. abstract category
* objects and arrows may be abstract entities of any kind
* seek to generalize mathematics in terms of categories
* often reveals further insights and similarities
* an alternative foundation to set theory
* describe mathematical entities and their relationships

a category C consists of

* a class obj(C) of objects
* a class hom(C) of morphisms
* (f: a -> b) maps object a to b
* hom(a,b) - denote the hom-class of all morphisms from a to b
* composition: hom(a,b) x hom(b,c) -> hom(a,c)

small/large category

* small - obj(C) and hom(C) are sets - large otherwise
* locally small - for all objects a, b, the hom-class hom(a,b) is a set (homset)
* categories, if not small, may still be locally small

examples

* Set - category of sets
* Rel - category of relations
* any preordered set (P,<=) - a small category
* any directed graph - a small category
* Ord - category of preordered sets

<!-- ======================================================================= -->
## wikipedia, concrete category

* a category equipped with a faithful functor to the category of sets
* allows to think of the objects as sets with additional structure
* and of its morphisms as structure-preserving functions

without the notion of category

* a class of objects, each equipped with an underlying set
* for any two objects x and y, a set of functions/morphisms exist

definition

* C is a category and (U: C -> Set)
* U assigns to every object in C its "underlying set"
* U assigns to every morphism in C its "underlying function"

remarks

* concretizable - if a concrete category exists (for a cat of sets)
* all small categories are concretizable
* concreteness - is not a property, but a structure with which a cat is equipped
* several concrete categories (C,U) may exist which correspond to C
