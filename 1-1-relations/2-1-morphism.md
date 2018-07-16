
<!-- ======================================================================= -->
# Morphisms

<!-- ======================================================================= -->
## wikipedia, morphism

* a structure-preserving mapping
* morphisms are functions (source/target, domain/codomain)
* hom-set := hom(X,Y) = the collection of all morphisms from X to Y
* locally small category := all hom(X,Y) are sets
* function (f) is idempotent, if 

idempotence

* f can be applied multiple times without changing the result

monomorphism, epimorphism

* (f: X -> Y) is a monomorphism, if
* ((f x g1) = (f x g2)) -> (g1 == g2) where (g1,g2: Z -> X)

isomorphism

* (f: X -> Y) is an isomorphism, if (g: Y -> X) exists such that
* (g1 x f = idX) and (f x g2 = idY)
* g1 and g2 don't necessarily have to both exist
* if the do, then (g1 == g2)
* g is called the inverse of f, and f an inverse of g
* if an isomorphism exists, then both objects are said to be isomorphic

endo-morphism, auto-morphism

* (f: X -> X) is an endomorphism of X
* automorphism - a morphism that is an endomorphism and an isomorphism
