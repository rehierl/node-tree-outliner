
<!-- ======================================================================= -->
# Properties of binary relations (2)

<!-- ======================================================================= -->
## wikipedia, set-like/local relation

* relation R over a set X
* for every (x in X), the class of all (y in X) such that yRx is a set
* e.g. the usual ordering (<) on the class of ordinal numbers is set-like
* i.e. the elements less than a given element form a set

<!-- ======================================================================= -->
## wikipedia, well-founded relation

* relation over a set X is well-founded, if
* every non-empty subset S has a minimal element in R
* i.e. an element m unrelated by sRm

remarks

* a poset is well-founded, if the strict order is well-founded
* if the order is total, then it is called a well-order

induction and recursion

* given a well-founded relation (X,R) and some property P(x)
* goal is to - prove that P(x) holds for all (x in X)
* show that - P(y) is true for all yRx, then P(x) holds for all (x in X)
* aka. well-founded or Noetherian induction

<!-- ======================================================================= -->
## wikipedia, quasitransitive

* a weaker version of transitivity
* a relation that is symmetric for some elements, and transitive elsewhere

definition

* aRb and !bRa and bRc and !cRb => aRc and !cRa
* R is transitive, if R is anti-symmetric

example

* person p indifferent between 7 and 8
* and indifferent between 8 and 9
* but prefers 9 over 7

remarks

* R must be a disjoint union of
* a symmetric relation J and
* a transitive relation P

<!-- ======================================================================= -->
## wikipedia, euclidean relation

* magnitudes which are equal to the same are equal to each other

```
right-euclidean   left-euclidean
---------------   --------
  c               a
 /                 \
a |               | c
 \                 /
  d               b
```

right-euclidean, euclidean

* if `aRc` and `aRd`, then also `cRd`
* e.g. "equality"

left-euclidean

* if `aRc` and `bRc`, then also `aRb`

remarks

* right-euclidean, reflexive => symmetric => equivalence
* left-euclidean, reflexive => equivalence
* quasitransitive if right/left-euclidean
