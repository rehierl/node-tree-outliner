
<!-- ======================================================================= -->
# Morphisms

* idX, 1x - same/identity element x in set X

<!-- ======================================================================= -->
## wikipedia, morphism

* a structure-preserving map from one structure to another of the same type
* morphisms are functions (source/target, domain/codomain)
* hom-set := hom(X,Y) = the collection of all morphisms from X to Y
* locally small category := all hom(X,Y) are sets
* function (f) is idempotent, if 

idempotence

* f can be applied multiple times without changing the result

monomorphism

* (f: X -> Y) is a monomorphism (aka. mono/monic), if
* ((f × g1) = (f × g2)) -> (g1 = g2) where (g1,g2: Z -> X)
* retraction or left inverse - (g: Y -> X) exists such that (g × f = 1x)
* has left-inverse => monomorphism

epimorphism

* (f: X -> Y) is a epimorphism (aka. epi/epic), if
* (g1 × f = g2 × f) -> (g1 = g2) where (g1,g2: Y -> Z)
* section or right inverse - (g: Y -> X) exists such that (f × g = 1y)
* has right-inverse => epimorphism

bimorphism

* has left- and right-inverse

isomorphism

* (f: X -> Y) is an isomorphism, if
* (g: Y -> X) exists such that (g1 × f = 1x) and (f × g2 = 1y)
* g1 and g2 don't necessarily have to both exist
* if they do, then (g1 == g2)
* g is called the inverse of f, and f an inverse of g
* an isomorphism exists => both objects are said to be isomorphic/equivalent

endo-morphism, auto-morphism

* (f: X -> X) is an endomorphism of X
* automorphism - a morphism that is an endomorphism and an isomorphism

<!-- ======================================================================= -->
## wikipedia, isomorphism

* a mapping that can be reversed by an inverse morphism
* two objects are isomorphic, if an isomorphism exists
* isomorphic objects appear to be "essentially equal"
* isomorphic objects may even be considered the same
