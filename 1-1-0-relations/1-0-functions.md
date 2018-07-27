
<!-- ======================================================================= -->
# A functional perspective

functions are special types of binary relations

* for a functional relation R := (A,B,...,G)
* e.g. `(A × B)` => `(f: A -> B)`
* e.g. `×T^n` => e.g. `(f: ×T^(n-1) -> Tn)`

characteristics

* function - right-unique and left-total
* injective, one-to-one - unique and left-total
* surjective, onto - right-unique and total
* bijection - unique and total

partial, total

* partial function - undefined for some (a in A)
* total function - defined for any (a in A)
* if partial, then total with regards to some strict-subset-of A
* surjective => (image == codomain)

<!-- ======================================================================= -->
## wikipedia, identity function

* aka. identity relation/map/transformation
* returns its argument as its value
* (f: X -> X) such that f(x) = x

remarks

* denoted as `id_X` (i.e. `X` as subscript), or short `idX`
* (f: M -> N) => ((f ¤ idM) = f = (idN ¤ f))

<!-- ======================================================================= -->
## wikipedia, inverse function (°)

* (f: X -> Y) and (g: Y -> X)
* (f(x) = y) <-> (g(y) = x)
* i.e. g is an inverse function of f
* if g exists, then g is unique to f
* i.e. a function has no more than one inverse
* denoted as `g := f^(-1)` alternatively `f'` or `f°`
* note - derivations are no subject of this discussion
* (f) must be bijective for (g) to exist
* (g) is automatically bijective

relations

* a function, as a relation R:=(X,Y,G), has an inverse,
* iff the converse relation S:=(Y,X,G) is a function on Y
* i.e. the converse relation is the inverse function

compositions

* if (f) is invertible, then
* f°(f(x)) = x for any (x in X)
* i.e. an identity function on set X
* (f° ¤ f) = idX, (f ¤ f°) = idY, f = (f°)°
* (g ¤ f)° = (f° ¤ g°) - note the flipped order!

<!-- ======================================================================= -->
## wikipedia, composition (¤)

* the pointwise application of one function to the result of another
* if (z is a function of y) and (y is one of x), then (z is one of x)
* i.e. for (f: X -> Y) and (g: Y -> Z)
* (g ¤ f: X -> Z) - i.e. (g ¤ f)(x) = g(f(x))
* (g ¤ f) is referred to as "g composed with f"
* synonymous - circle, round, about, after, following, of, on
* the output of one function becomes the input of the other

properties

* associative: f ¤ (g ¤ h) = (f ¤ g) ¤ h
* not necessarily commutative: (f ¤ g) <=!=> (g ¤ f)
* injective functions => injective composition
* surjective functions => surjective composition
* bijective functions => bijective composition

<!-- ======================================================================= -->
## wikipedia, monotonic functions

* aka. monotone function
* an order-preserving or order-reversing function between two ordered sets
* order-preserving - increasing, monotonically increasing, non-decreasing
* if (x <= y), then f(x) <= f(y)
* order-reversing - monotonically decreasing, decreasing, non-increasing
* if (x <= y), then f(x) >= f(y) - decreasing
* strictly increasing if (<) instead of (<=)
* strictly decreasing if (>) instead of (<= and >=)
* if strictly increasing/decreasing, then one-to-one

in order theory

* isotone, monotone - i.e. order-preserving
* antitone, anti-monotone - i.e. order-reversing
* the composition of two monotone mappings is monotone
* a constant function is both monotone and antitone
* e.g. order-embedding, order-isomorphism (surjective order-embedding)
